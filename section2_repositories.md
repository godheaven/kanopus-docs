[BACK](README.md)

## Table of Contents

- [1. Improving Non-Modularized Projects](section1_projects.md)
- [2. Repository Naming](section2_repositories.md)
- [3. Architecture Proposals](section3_arquitecture.md)
- [4. Software Design Patterns Guide](section4_patterns.md)
- [5. Recommended Architecture for Large Projects (+20 Microservices)](section5_architecture_recommended.md)
- [6. Local Development Setup](section6_local_environment.md)
- [7. CI/CD Recommendation](section7_cicd.md)


<br/>
<br/>

2. Repository Naming

The repository structure for a company with multiple projects should follow a naming convention based on domain or product prefixes, and suffixes by component type. This convention allows for scalability, organizational clarity, module reuse, and efficient CI/CD automation.

Here’s a list of recommended repository names, grouped by component type, with suggestions that combine clarity, consistency, and best naming practices for ecosystems like GitHub or GitLab (especially useful in microservice architectures):

<br/>

### 2.1. 📚 Suggested Naming Convention
```
    [prefix]-[subdomain]-[type]
```

📌 Prefix: Identifies the product, client, business unit, or company:

```
    erp → In-house ERP
    crm → Institutional CRM
    int → Integrations
```

📌 Subdomain (optional but recommended): Identifies the repo’s main functionality:

```
    auth → Authentication
    notif → Notifications
    access → Access control
    core → Shared logic
```

📌 Type: Defines the component type of the repo:

```
    service → Backend microservice
    web → Web frontend
    lib → Shared library
    infra → Infrastructure (docker, terraform, pipelines, etc.)
    docs → Documentation
    cli → Command-line tool
```

### 2.2. 🧩 Shared Libraries
Reusable across microservices or frontends.

- [prefix]-[subdomain]-lib

### 2.3. 🌐 Web / Frontends / Desktop
Angular, React, Vue, JSF apps, etc.

- [prefix]-[subdomain]-web
- [prefix]-[subdomain]-desktop

### 2.4. 🧱 Microservices
Use domain-service pattern to maintain consistency.

- [prefix]-[subdomain]-service

### 2.5. 🔧 Utilities, tools, or scripts
Scripts, loaders, exporters, cron jobs, generators, etc.

- [prefix]-[subdomain]-scripts
- [prefix]-[subdomain]-cli
- [prefix]-[subdomain]-tool

## 📌 Important Notes

> 💡 **Tip 1:** Avoid overly cryptic abbreviations.  
> 🔒 **Tip 2:** Use a common prefix if you’re in an organization (like myproject-, kanopus-, etc.).  
> ⚠️ **Tip 3:** Consistency is key to good organization.

---
<br/>
<br/>
<br/>

[BACK](README.md)
