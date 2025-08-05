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

## 4. Software Design Patterns Guide

## ✅ 4.1. Recognized Software Design Patterns

### 🔧 Creational Patterns
- **Singleton**: Ensures a single global instance.
- **Factory Method**: Delegates object creation to subclasses.
- **Abstract Factory**: Produces families of related objects.
- **Builder**: Step-by-step construction of complex objects.
- **Prototype**: Clones existing objects.

### 🧱 Structural Patterns
- **Adapter**: Converts one interface into another.
- **Bridge**: Separates abstraction from implementation.
- **Composite**: Treats individual objects and groups uniformly.
- **Decorator**: Adds behavior without modifying the original class.
- **Facade**: Provides a unified interface to subsystems.
- **Flyweight**: Shares data for efficiency.
- **Proxy**: Controls access to another object.

### 🎭 Behavioral Patterns
- **Observer**: Event subscription mechanism.
- **Strategy**: Interchangeable algorithms.
- **Command**: Encapsulates an action as an object.
- **State**: Varies behavior based on state.
- **Template Method**: Algorithm skeleton with customizable steps.
- **Chain of Responsibility**: Linked handlers.
- **Mediator**: Centralizes communication.
- **Memento**: Saves/restores state.
- **Visitor**: Adds operations to structures.
- **Interpreter**: Parses simple languages.
- **Iterator**: Traverses structures without exposing internals.

---

## ⚠️ 4.2. Software Design Anti-Patterns

- **God Object**: Classes that do too much (violate SRP).
- **Spaghetti Code**: Tangled and hard-to-follow flow.
- **Lava Flow**: Obsolete code kept due to fear of removal.
- **Shotgun Surgery**: Small changes require multiple edits across files.
- **Golden Hammer**: Using one pattern or tech for everything.
- **Boat Anchor**: Unused but retained code.
- **Reinventing the Wheel**: Rewriting what already exists and works.
- **Magic Numbers / Strings**: Contextless hardcoded values.

---

## 🚫 Common Software Design Mistakes

- ❌ Using patterns without understanding their purpose.
- ❌ Premature or unnecessary abstractions.
- ❌ Adding complexity for the sake of elegance.
- ❌ Ignoring SOLID principles (especially SRP).
- ❌ Mixing responsibilities (e.g., controllers validating, processing, and querying).
- ❌ Poor documentation and naming.
- ❌ Ignoring future maintainability.
- ❌ Adopting architecture trends without real need.

> 📌 A good architecture should be understandable, flexible, and aligned with business goals—not just “technically correct.”

---
<br/>

# 🎓 Recommended Trainings: Software Design Patterns

| Training Title                                         | Platform         | Description                                                                 | Level         | Link                                      |
|--------------------------------------------------------|------------------|-----------------------------------------------------------------------------|---------------|-------------------------------------------|
| **Design Patterns in Java**                            | Udemy            | Learn 23 GoF design patterns with practical Java examples.                  | Intermediate  | [View Course](https://www.udemy.com/course/java-design-patterns-tutorial/) |
| **Design Patterns in .NET**                            | Pluralsight      | Deep dive into design patterns using C# and real-world use cases.           | Intermediate  | [View Course](https://www.pluralsight.com/courses/csharp-design-patterns) |
| **Refactoring & Design Patterns**                      | JetBrains Academy| Practice refactoring code using design patterns interactively.              | Beginner      | [View Course](https://www.jetbrains.com/academy/) |
| **Software Design Patterns – Full Course**             | freeCodeCamp     | Full YouTube course covering all major patterns with examples.              | Beginner      | [Watch](https://www.youtube.com/watch?v=tv-_1er1mWI) |
| **Advanced Design Patterns in Java**                   | Coursera         | Taught by university professors with peer-reviewed assignments.             | Advanced      | [View Course](https://www.coursera.org/learn/design-patterns) |
| **Design Patterns Overview**                           | GeeksforGeeks    | Written explanations and examples for all 23 GoF patterns.                  | All Levels    | [Read Guide](https://www.geeksforgeeks.org/software-design-patterns/) |
| **Clean Architecture & Design Patterns**               | Udemy            | Combines DDD, SOLID principles, and patterns in real projects.              | Intermediate  | [View Course](https://www.udemy.com/course/clean-architecture-dotnet-core/) |
| **Design Patterns in TypeScript**                      | Refactoring.Guru | Visual, interactive explanations of patterns in multiple languages.         | Beginner–Pro  | [Explore](https://refactoring.guru/design-patterns/typescript) |




---
<br/>
<br/>
<br/>

[BACK](README.md)
