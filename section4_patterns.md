## 4. Guía de Patrones de Diseño de Software
	
## ✅ 4.1. Patrones de Diseño de Software Reconocidos

### 🔧 Patrones Creacionales
- **Singleton**: Garantiza una única instancia global.
- **Factory Method**: Delega la creación de objetos a subclases.
- **Abstract Factory**: Produce familias de objetos relacionados.
- **Builder**: Construcción paso a paso de objetos complejos.
- **Prototype**: Clonación de objetos.

### 🧱 Patrones Estructurales
- **Adapter**: Convierte una interfaz en otra.
- **Bridge**: Separa abstracción de su implementación.
- **Composite**: Trata objetos individuales y grupos uniformemente.
- **Decorator**: Añade comportamiento sin modificar la clase original.
- **Facade**: Proporciona una interfaz unificada a subsistemas.
- **Flyweight**: Comparte datos para eficiencia.
- **Proxy**: Controla acceso a otro objeto.

### 🎭 Patrones de Comportamiento
- **Observer**: Subscripción a eventos.
- **Strategy**: Algoritmos intercambiables.
- **Command**: Encapsula una acción como objeto.
- **State**: Comportamiento según estado.
- **Template Method**: Esqueleto de algoritmo con pasos personalizables.
- **Chain of Responsibility**: Manejadores encadenados.
- **Mediator**: Centraliza la comunicación.
- **Memento**: Guarda/restaura estado.
- **Visitor**: Añade operaciones a estructuras.
- **Interpreter**: Analiza lenguajes simples.
- **Iterator**: Recorre estructuras sin exponer su implementación.

---

## ⚠️ 4.2. Antipatrones de Diseño de Software

- **God Object**: Clases que hacen demasiadas cosas (violan SRP).
- **Spaghetti Code**: Flujo de control enredado y difícil de seguir.
- **Lava Flow**: Código antiguo que no se limpia por temor a romperlo.
- **Shotgun Surgery**: Cambios pequeños que requieren muchas modificaciones en distintos lugares.
- **Golden Hammer**: Usar un mismo patrón o tecnología para todo.
- **Boat Anchor**: Código que se mantiene “por si acaso” pero nunca se usa.
- **Reinventing the Wheel**: Reescribir algo que ya existe y es probado.
- **Magic Numbers / Strings**: Valores sin contexto usados directamente en el código.

---

## 🚫 4.3. Errores Comunes en el Diseño de Software

- ❌ Usar patrones sin comprender su propósito real.
- ❌ Crear abstracciones innecesarias o prematuras.
- ❌ Aumentar la complejidad para "ser más elegantes".
- ❌ No aplicar principios SOLID (especialmente SRP).
- ❌ Mezclar responsabilidades (ej. controladores que validan, procesan y consultan).
- ❌ No documentar ni nombrar claramente clases y métodos.
- ❌ Ignorar la mantenibilidad futura al tomar decisiones de diseño.
- ❌ Implementar una arquitectura solo por tendencia, sin necesidad real.

---

> 📌 Una buena arquitectura debe ser entendible, flexible y alineada con el negocio, no solo “correcta” desde el punto de vista técnico.

---
<br/>
<br/>
<br/>

[BACK](README.md)