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

## 5. Recommended Architecture for Large Projects (+20 Microservices)

This document describes a modern, scalable architecture ideal for systems with multiple microservices and distributed development teams.

---

### ✅ 5.1. Recommendation: Microservices + Hexagonal + Event-Driven + DDD

An architecture combining:
- **Microservices aligned to functional domains**
- **Hexagonal Architecture (Ports & Adapters)** in each service
- **Event-driven communication between services**
- **DDD (Domain-Driven Design) principles** for modularity
- Modern infrastructure (API Gateway, Service Discovery, Observability, CI/CD)

---

### 🧭 5.2. Key Components

| Component                | Description                                                 |
|--------------------------|-------------------------------------------------------------|
| Domain-based Microservices | Separation by business context                            |
| Hexagonal Architecture   | Domain logic independent from infrastructure                |
| Event-Driven Architecture| Async communication using Kafka/RabbitMQ                    |
| API Gateway              | Single entry point, security, rate-limiting                 |
| Service Discovery        | Eureka / Consul for dynamic service location                |
| Centralized Configuration| Spring Cloud Config / Consul                                |
| Observability            | Prometheus, Grafana, Zipkin, ELK                            |
| Security                 | JWT + OAuth2 (Google, Azure AD), roles, scopes              |
| CI/CD                    | Jenkins, GitHub Actions, GitLab CI/CD                      |
| Containers + Orchestrator| Docker + Kubernetes                                         |

---

### 🧠 5.3. Benefits

- ✅ Horizontal scalability per domain and team
- ✅ Independent service deployment
- ✅ Low coupling via events and interfaces
- ✅ Professional-grade observability and monitoring
- ✅ High maintainability and testability per service

---

### 🛡️ 5.4. Best Practices for Large Teams

| Practice                  | Description                                                |
|---------------------------|------------------------------------------------------------|
| Separate Repositories     | Individual repos per service or domain                     |
| Versioned API Contracts   | OpenAPI (Swagger) per microservice                         |
| Shared Base Template      | Common scaffold with security, metrics, and logging        |
| Technical Lead per Domain | Ownership division across teams                            |
| Continuous Documentation  | README + Swagger + Confluence                              |
| REST + Events             | REST for reads, events for writes (light CQRS)             |

---

## 📌 Additional Recommendations

- Use **Hexagonal Architecture** in every microservice.
- Consider CQRS/ES for complex event logic.
- Use **GitHub Actions** for simple and effective CI/CD.
- Prefer **Kafka/RabbitMQ** to decouple critical services.
- Set up **Kubernetes** from the beginning if scaling is required.

---
<br/>
<br/>
<br/>

[BACK](README.md)
