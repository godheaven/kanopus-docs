## 3. Propuestas de Arquitectura

- ✔ Arquitectura en Capas (Layered Architecture)
- ✔ Hexagonal Architecture (Ports and Adapters)
- ✔ Clean Architecture (Domain-Centric)
- ✔ Microservicios con Bounded Context
- ✔ Frontend Modular (Angular con Feature Modules y Lazy Loading)


<br/>

### 3.1. 📚 Principios SOLID en Desarrollo de Software

**SOLID** es un conjunto de 5 principios de diseño orientado a objetos que ayudan a construir software más mantenible, extensible y robusto.

**Resumen de los principios SOLID**

| Letra | Principio                              | Descripción breve                               |
|-------|----------------------------------------|--------------------------------------------------|
| S     | Single Responsibility Principle (SRP)  | Una clase debe tener una sola responsabilidad.   |
| O     | Open/Closed Principle (OCP)            | Abierto para extensión, cerrado para modificación. |
| L     | Liskov Substitution Principle (LSP)    | Las subclases deben sustituir correctamente a su clase padre. |
| I     | Interface Segregation Principle (ISP)  | No forzar a las clases a implementar métodos que no usan. |
| D     | Dependency Inversion Principle (DIP)   | Depender de abstracciones, no de implementaciones. |


## 🎯 Beneficios de aplicar SOLID

- Código limpio, modular y fácil de mantener
- Menor acoplamiento
- Facilita testing y refactorización
- Compatible con principios de arquitectura limpia

---


<br/>

### 3.2. 🔧 Patrones generales que refuerzan SRP

| Patrón              | Descripción                        |
|--------------------------|------------------------------------|
| Service Layer                 | Encapsula la lógica de negocio en clases de servicio, separando responsabilidades de control y persistencia.|
| Repository                    | Aísla la lógica de acceso a datos en una capa dedicada, evitando acoplamiento con lógica de negocio   |
| DTO (Data Transfer Object)    | Reduce acoplamiento entre capas, evitando que las entidades se propaguen a otras capas.|
| Factory                       | Encapsula la creación de objetos complejos, evitando lógica de inicialización mezclada en controladores o servicios.|
| Adapter                       | Transforma interfaces externas para que encajen en nuestro dominio sin romper SRP del resto del sistema.|
| Command                       | Encapsula una operación en una clase que tiene una única responsabilidad: ejecutar una acción con parámetros específicos.|
| Strategy                      | Permite cambiar algoritmos o reglas sin modificar la lógica que los utiliza (ej. múltiples formas de validar acceso).|
| Chain of Responsibility       | Encadena manejadores que tienen una única responsabilidad por tipo de evento (ej. validaciones encadenadas, filtros, etc.). |

 
---
<br/>
<br/>
<br/>

[BACK](README.md)