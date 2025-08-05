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

## 3. Architecture Proposals

- ✔ Layered Architecture
- ✔ Hexagonal Architecture (Ports and Adapters)
- ✔ Clean Architecture (Domain-Centric)
- ✔ Microservices with Bounded Context
- ✔ Modular Frontend (Angular with Feature Modules and Lazy Loading)

<br/>

### 3.1. 📚 SOLID Principles in Software Development

**SOLID** is a set of 5 object-oriented design principles that help build more maintainable, extensible, and robust software.

**Summary of SOLID Principles**

| Letter | Principle                             | Brief Description                                |
|--------|----------------------------------------|--------------------------------------------------|
| S      | Single Responsibility Principle (SRP)  | A class should have only one reason to change.   |
| O      | Open/Closed Principle (OCP)            | Open for extension, closed for modification.     |
| L      | Liskov Substitution Principle (LSP)    | Subtypes must be substitutable for their base types. |
| I      | Interface Segregation Principle (ISP)  | Do not force classes to depend on unused methods. |
| D      | Dependency Inversion Principle (DIP)   | Depend on abstractions, not on concrete classes.  |

## 🎯 Benefits of Applying SOLID

- Clean, modular, and maintainable code
- Lower coupling
- Easier testing and refactoring
- Compatible with clean architecture principles

---

<br/>

### 3.2. 🔧 General Patterns Supporting SRP

| Pattern               | Description                                                  |
|-----------------------|--------------------------------------------------------------|
| Service Layer         | Encapsulates business logic in service classes.              |
| Repository            | Isolates data access logic in a dedicated layer.             |
| DTO (Data Transfer Object) | Reduces coupling between layers.                         |
| Factory               | Encapsulates complex object creation.                        |
| Adapter               | Adapts external interfaces to fit domain needs.              |
| Command               | Encapsulates an operation in a dedicated class.              |
| Strategy              | Allows dynamic change of algorithms or rules.                |
| Chain of Responsibility | Chains handlers for specialized processing.               |

---
<br/>
<br/>
<br/>

[BACK](README.md)
