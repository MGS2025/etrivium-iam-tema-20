# Tema 20 — Índice

> **Título oficial**: Diseño y programación orientada a objetos. Objetos, clases, herencia, métodos, sobrecarga. Ventajas e inconvenientes. Patrones de diseño y UML.
>
> **Bloque**: Parte II — Técnico (Temas 11-40)
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid

---

## Estructura del tema

1. **Fundamentos de la programación orientada a objetos**
   1.1. Evolución de la ingeniería del software hacia el paradigma OO
   1.2. Pilares fundamentales de la POO: abstracción y encapsulamiento
   1.3. Modularidad y cohesión
   1.4. Principios SOLID de diseño de software

2. **Elementos y componentes software**
   2.1. Clases y objetos; ciclo de vida
   2.2. Atributos, variables, métodos y constructores
   2.3. Visibilidad y control de acceso
   2.4. Mecanismos avanzados en POO: herencia simple y múltiple
   2.5. Sobrecarga y sobrescritura de métodos
   2.6. Polimorfismo y ligadura dinámica
   2.7. Jerarquías y reutilización de código
   2.8. Relaciones de acoplamiento

3. **Ventajas e inconvenientes del paradigma OO**
   3.1. Beneficios en el ciclo de vida del software: reutilizabilidad y mantenibilidad
   3.2. Escalabilidad y aislamiento de errores
   3.3. Limitaciones, costes y penalizaciones técnicas: curva de aprendizaje y complejidad de diseño
   3.4. Sobrecarga en tiempo de ejecución
   3.5. Riesgos de un mal diseño orientado a objetos

4. **Patrones de diseño**
   4.1. Concepto y catálogo (Gang of Four)
   4.2. Patrón, anti-patrón y criterios de aplicabilidad arquitectónica
   4.3. Clasificación técnica: patrones creacionales
   4.4. Patrones estructurales
   4.5. Patrones de comportamiento

5. **Modelado de sistemas con UML (Unified Modeling Language)**
   5.1. Fundamentos y especificación del estándar OMG: origen y evolución
   5.2. Bloques de construcción y mecanismos comunes
   5.3. Diagramas estructurales y estáticos: Diagrama de Clases y Diagrama de Objetos
   5.4. Diagramas de Arquitectura física
   5.5. Diagramas de comportamiento: modelado de requisitos funcionales (Diagrama de Casos de Uso)
   5.6. Interacción temporal: Diagramas de Secuencia y de Comunicación/Colaboración
   5.7. Control de flujo y estados: Diagramas de Máquina de Estados y de Actividades

6. **Tendencias actuales en el diseño orientado a objetos**

---

## Conceptos clave para memorizar

| Concepto | Dato clave |
|---|---|
| Los 4 pilares de la POO | Abstracción, Encapsulamiento, Herencia, Polimorfismo [BOOCH07] |
| SOLID | Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion [MARTIN03] |
| Herencia vs Composición | «Favorece la composición sobre la herencia» — principio de diseño de GoF para reducir acoplamiento [GOF94] |
| Sobrecarga (overloading) | Mismo nombre de método, distinta firma, ligadura en **tiempo de compilación** (estática) [GOSLING-JLS] |
| Sobrescritura (overriding) | Redefinición de un método heredado, ligadura en **tiempo de ejecución** (dinámica) [GOSLING-JLS] |
| Catálogo GoF | 23 patrones: 5 creacionales + 7 estructurales + 11 de comportamiento [GOF94] |
| UML | Estándar OMG, 14 tipos de diagrama: 7 estructurales + 7 de comportamiento [OMG-UML25] |
| Diagrama de Clases | Único diagrama UML de obligada elaboración en casi cualquier diseño OO; 3 compartimentos (nombre, atributos, métodos) [FOWLER-UML] |
| Composición vs agregación | Composición = dependencia de ciclo de vida («todo-parte» fuerte, rombo relleno); agregación = independencia («todo-parte» débil, rombo hueco) [RUMBAUGH05] |

---

*Todos los ejemplos de código de este tema se escriben en **Java** (decisión de Joan, coherente con el Tema 21 — Arquitectura Java EE). Ver `tema-20-contenido.md`, sección «Convenciones», para el detalle de las cuatro cajas callout y el esquema de clases usado en los ejemplos.*
