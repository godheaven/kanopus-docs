# Pulse Performance Dashboard

A **production-ready monolithic Spring Boot application** that connects to **Jira Cloud and Jira Server/Data Center**, caches issue and worklog data in H2, and generates monthly performance dashboards per user — including a configurable scatter plot.

---

## 🚀 Quick Start

### Prerequisites
- Java 21+
- Maven 3.9+
- Docker (optional)

### Run Locally

```bash
git clone <repo>
cd ktool-pulse
mvn spring-boot:run
```

Access at: **http://localhost:8080**  
Default credentials: `admin` / `admin123`

### Run with Docker

```bash
# Build
docker build -t jira-dashboard .

# Run
docker run -p 8080:8080 \
  -e APP_USERNAME=admin \
  -e APP_PASSWORD=YourSecurePassword \
  -e APP_ENCRYPTION_KEY=YourSecretEncryptionKey32Chars!! \
  -v $(pwd)/data:/app/data \
  jira-dashboard
```

### Docker with persistent data volume

```bash
docker run -d \
  --name jira-dashboard \
  -p 8080:8080 \
  -e APP_PASSWORD=SecurePassword123 \
  -e APP_ENCRYPTION_KEY=MyProductionKey32CharactersOK!! \
  -v jira-dashboard-data:/app/data \
  jira-dashboard
```


### Run As Linux Service

If you prefer to run the application as a standalone service on a Linux server without Docker, you can use the following scripts to manage the process.

#### 1. Create `start.sh`
```bash
#!/bin/bash
# Configuration
APP_NAME="ktool-pulse"
JAR_FILE="./target/ktool-pulse-1.0.1.jar" # Adjust the version

# 1. Memory Settings (JVM Options)
JAVA_OPTS="-Xms512m -Xmx2g"

# 2. Port, Database and License Path
SERVER_PORT="8443"
DB_PATH="./data/pulse-db"
LICENSE_PATH="./license/license.lic"

# 3. HTTPS / SSL Configuration (Optional)
SSL_OPTS="--server.ssl.enabled=true \
--server.ssl.key-store=file:/etc/ssl/keystore.p12 \
--server.ssl.key-store-password=your_password \
--server.ssl.key-store-type=PKCS12"

# Environment Variables
export APP_USERNAME="admin"
export APP_PASSWORD="YourSecurePassword"
export APP_ENCRYPTION_KEY="YourSecretEncryptionKey32Chars!!"
export KTOOL_PULSE_EXPECTED_HASH="YOUR_SHA512_HASH_HERE"

echo "Starting $APP_NAME on port $SERVER_PORT..."

# Execution
nohup java $JAVA_OPTS -jar $JAR_FILE \
  --server.port=$SERVER_PORT \
  --spring.datasource.url=jdbc:h2:file:$DB_PATH \
  --ktool.license.path=$LICENSE_PATH \
  $SSL_OPTS \
  > output.log 2>&1 &

echo $! > app.pid
echo "$APP_NAME started with PID $(cat app.pid)"
```

#### 2. Create `stop.sh`
```bash
#!/bin/bash
APP_NAME="ktool-pulse"

if [ -f app.pid ]; then
    PID=$(cat app.pid)
    echo "Stopping $APP_NAME (PID $PID)..."
    kill $PID
    rm app.pid
    echo "$APP_NAME stopped."
else
    echo "Error: app.pid not found. Is the service running?"
fi
```

#### 3. Permissions
Remember to grant execution permissions to both scripts:
```bash
chmod +x start.sh stop.sh
```

---

## ⚙️ Configuration

### Environment Variables

| Variable | Default | Description |
|---|---|---|
| `APP_USERNAME` | `admin` | Login username |
| `APP_PASSWORD` | `admin123` | Login password |
| `APP_ENCRYPTION_KEY` | (dev key) | 32+ char key for token encryption |
| `SERVER_PORT` | `8080` | HTTP port |
| `JAVA_OPTS` | `-Xmx512m -Xms256m` | JVM options |
| `KTOOL_LICENSE_PATH` | `/opt/ktool-pulse/license/license.lic` | Custom path to the license file |
| `KTOOL_LICENSE_PUBLIC_KEY` | (bundled) | Public key for signature validation (PEM string) |
| `KTOOL_PULSE_LICENSE_INLINE` | (empty) | Full license file content (Alternative to file mount) |

### `application.yml` Key Settings

```yaml
spring:
  datasource:
    url: jdbc:h2:file:./data/jira-dashboard   # H2 file mode
app:
  encryption:
    key: ${APP_ENCRYPTION_KEY}                 # Token encryption key
  jira:
    max-results-per-page: 100                  # Pagination size
```

---

## 🔗 Configuring Jira

### Jira Cloud
1. Go to **Connections** → **New Connection**
2. Enter:
   - **Base URL**: `https://yourorg.atlassian.net`
   - **Email**: Your Atlassian account email
   - **API Token**: Generate at https://id.atlassian.com/manage/api-tokens
3. Click **Test Connection** to verify

### Jira Server / Data Center
1. Go to **Connections** -> **New Connection**
2. Select **Connection Type: Server**
3. Enter:
   - **Base URL**: `https://jira.your-company.com`
   - **Email** (optional):
     - If provided, app uses **Basic Auth** (`email:token`)
     - If empty, app uses **Bearer PAT** (`Authorization: Bearer <token>`)
   - **API Token / PAT**
4. Click **Test Connection** to verify

### Jira API Compatibility Notes
- **Cloud** uses `/rest/api/3`
- **Server/Data Center** uses `/rest/api/2`
- User lookup adapts parameter by type:
  - Cloud: `accountId`
  - Server: `username`

### Pagination and Resilience
- Issue import uses **robust pagination**:
  - Cloud: `nextPageToken` flow via `/search/jql`
  - Server: `startAt`/`maxResults` flow via `/search`
- Import includes loop safety guards (max pages and zero-result protections)
- Jira requests use retry with incremental backoff for transient failures
- Worklogs are fetched page by page until `startAt >= total`

### Example JQL Queries

```jql
# All issues in a project for March 2024
project = MYPROJ AND created >= "2024-03-01" AND created <= "2024-03-31"

# Sprint-based query
project = MYPROJ AND sprint in openSprints()

# Issues assigned to team with worklogs in March
project = MYPROJ AND worklogDate >= "2024-03-01" AND worklogDate <= "2024-03-31"

# Multiple projects
project in (PROJ1, PROJ2) AND created >= "2024-03-01"
```

---

## 📊 Usage Workflow

1. **Add Connection** → Go to Connections, create a Jira connection and test it
2. **Create Snapshot** → Go to Snapshots, define name, period (year/month), and JQL
3. **Import Data** → Click the refresh (↻) button to fetch Jira data into H2
4. **View Dashboard** → Go to Dashboard, select your snapshot, click "Calculate Metrics"
5. **Adjust Settings** → Go to Settings to configure weights, thresholds, and completion statuses

### Data Flow
```
Jira API ──(on import only)──► H2 Database ──(always)──► Dashboard
```
> **IMPORTANT**: The dashboard ALWAYS reads from H2. Jira is NEVER called during dashboard viewing.

---

## 🏗️ Architecture

```
cl.kanopus.tool.pulse
├── config/          # Security, Async, App config
├── domain/          # JPA entities (8 tables)
├── repository/      # Spring Data JPA repositories
├── dto/             # Request/Response DTOs (Java Records)
├── jira/            # Jira REST API client (WebClient Cloud/Server)
├── service/         # ConnectionService, SettingsService, CapacityService, EncryptionService
├── snapshot/        # SnapshotService (async Jira import)
├── metrics/         # MetricsService (performance calculation)
└── web/             # REST controllers + Thymeleaf page controllers
```

### Database Schema

| Table | Purpose |
|---|---|
| `jira_connection` | Jira server configs (tokens encrypted) |
| `jira_snapshot` | Snapshot metadata and status |
| `jira_issue_cache` | Cached issue data per snapshot |
| `jira_worklog_cache` | Cached worklog entries per snapshot |
| `jira_user_cache` | Cached user info per snapshot |
| `monthly_capacity` | Manual capacity hours per user per snapshot |
| `performance_settings` | Configurable weights, thresholds, statuses |
| `monthly_user_metrics` | Calculated performance results |

---

## 📈 Performance Metrics

| Metric | Formula |
|---|---|
| Estimated Hours | `SUM(originalEstimateSeconds) / 3600` |
| Worked Log Hours | `SUM(worklogSeconds in month) / 3600` |
| Spent Time Hours | `SUM(timeSpentSeconds on assigned issues) / 3600` |
| Completed % | `completed_issues / total_issues × 100` |
| Worked Log % | `worked_log_hours / capacity_hours × 100` |
| **Weighted Score** | `completed% × xWeight + worked_log% × yWeight` |

### Scatter Plot Quadrants

|  | Low Worked Log | High Worked Log |
|---|---|---|
| **High Completed** | MEDIUM | **AMAZING** ⭐ |
| **Low Completed** | **LOW** ⚠️ | HIGH |

---

## 🧪 Running Tests

```bash
# All tests
mvn test

# Skip tests (for faster build)
mvn package -DskipTests
```

---

--- 

## 🔑 Commercial Licensing 

ktool-pulse includes a commercial license validation system for enterprise features. Without a valid license, the application runs in **Free Mode**. 

### License Activation 
1. Go to **Configuration** → **License** in the application. 
2. Copy your **System Fingerprint**. 
3. Send the fingerprint to Kanopus Support to receive your .lic file. 
4. Apply the license using one of the methods below. 

### Installation Methods 

#### Method A: Docker Volume (Recommended) 
Mount your license file to the container: 
```bash 
docker run -p 8080:8080 \ 
  -v $(pwd)/license.lic:/opt/ktool-pulse/license/license.lic:ro \ 
  jira-dashboard 
``` 

#### Method B: Environment Variable 
Pass the full license content as an environment variable: 
```bash 
docker run -p 8080:8080 \ 
  -e KTOOL_PULSE_LICENSE_INLINE="$(cat license.lic)" \ 
  jira-dashboard 
``` 

#### Method C: Custom Path
Specify a custom path if the license file is not in the default location:
```bash
docker run -p 8080:8080 \
  -v $(pwd)/my-license.lic:/data/license.lic:ro \
  -e KTOOL_LICENSE_PATH=/data/license.lic \
  jira-dashboard
```

### Feature Gating 
| Feature | Free Mode | Commercial License | 
|---|:---:|:---:| 
| Dashboards & Snapshots | ✅ | ✅ | 
| Organizational Areas & Teams | ✅ | ✅ | 
| Advanced Analytics | ❌ | ✅ | 
| AI-Powered Insights | ❌ | ✅ | 
| Advanced Data Export | ❌ | ✅ | 


## 🔒 Security Notes

- API tokens are **AES-encrypted** before storage using Spring Security Crypto
- Tokens are **never returned** in API responses
- Form-based login with CSRF protection
- H2 console restricted (admin only, not exposed publicly)
- Set `APP_ENCRYPTION_KEY` to a strong 32+ character key in production

---

## 🐳 UI Screenshots

| Page | Description |
|---|---|
| **Login** | Dark glassmorphism login page |
| **Dashboard** | Metrics table + Chart.js scatter plot |
| **Connections** | CRUD with connection test |
| **Snapshots** | Create/refresh with status tracking |
| **Settings** | Configure weights, thresholds, completion statuses |
