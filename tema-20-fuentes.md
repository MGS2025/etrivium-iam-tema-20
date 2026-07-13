# Tema 20 — Fuentes

> **Título oficial**: Diseño y programación orientada a objetos. Objetos, clases, herencia, métodos, sobrecarga. Ventajas e inconvenientes. Patrones de diseño y UML.
>
> **Criterio**: todo dato del contenido cita un **ID** inline (p. ej. `[GOF94, cap. 1]`). Tier 1 = obras canónicas del paradigma OO, los patrones de diseño y el estándar UML; Tier 2 = especificación oficial del lenguaje usado en los ejemplos (Java, decisión de Joan, coherente con el Tema 21 — Java EE) y documentación de referencia de herramientas de modelado; Tier 3 = marco de calidad e ingeniería del software, no citado como contenido técnico nuclear.

---

## Tier 1 — Canónicas

| ID | Referencia |
|---|---|
| `[BOOCH07]` | Booch, G.; Maksimchuk, R. A.; Engle, M. W.; et al. *Object-Oriented Analysis and Design with Applications* (3.ª ed.). Addison-Wesley. Obra de referencia del análisis y diseño OO: abstracción, clases, jerarquías. |
| `[MEYER97]` | Meyer, B. *Object-Oriented Software Construction* (2.ª ed.). Prentice Hall. Fundamento formal de encapsulamiento, contratos, herencia y polimorfismo; origen del principio abierto/cerrado. |
| `[GOF94]` | Gamma, E.; Helm, R.; Johnson, R.; Vlissides, J. *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. Obra fundacional del catálogo de 23 patrones de diseño (Gang of Four). |
| `[MARTIN03]` | Martin, R. C. *Agile Software Development, Principles, Patterns, and Practices*. Prentice Hall. Formulación y nombrado de los cinco principios **SOLID**. |
| `[MARTIN00]` | Martin, R. C. (2000). *Design Principles and Design Patterns*. objectmentor.com. Artículo original que enuncia SRP, OCP, LSP, ISP, DIP antes de su acrónimo SOLID. |
| `[LISKOV94]` | Liskov, B.; Wing, J. M. (1994). *A Behavioral Notion of Subtyping*. ACM TOPLAS 16(6). Formulación formal del principio de sustitución de Liskov. |
| `[OMG-UML25]` | Object Management Group. *OMG Unified Modeling Language (OMG UML), Version 2.5.1* (formal/2017-12-05). Especificación normativa vigente del estándar UML. |
| `[RUMBAUGH05]` | Rumbaugh, J.; Jacobson, I.; Booch, G. *The Unified Modeling Language Reference Manual* (2.ª ed.). Addison-Wesley. Los «tres amigos» creadores de UML; manual de referencia de la notación. |
| `[FOWLER-UML]` | Fowler, M. *UML Distilled: A Brief Guide to the Standard Object Modeling Language* (3.ª ed.). Addison-Wesley. Guía concisa y muy citada de los diagramas UML de uso práctico. |
| `[LARMAN04]` | Larman, C. *Applying UML and Patterns* (3.ª ed.). Prentice Hall. Puente entre análisis orientado a objetos, UML y patrones GRASP. |
| `[SOMMERVILLE16]` | Sommerville, I. *Software Engineering* (10.ª ed.). Pearson. Modularidad, cohesión, acoplamiento y ciclo de vida del software como marco de ingeniería. |
| `[PRESSMAN14]` | Pressman, R. S.; Maxim, B. R. *Software Engineering: A Practitioner's Approach* (8.ª ed.). McGraw-Hill. Métricas de diseño OO, ventajas/inconvenientes del paradigma. |
| `[GOSLING-JLS]` | Gosling, J.; Joy, B.; Steele, G.; Bracha, G.; Buckley, A. *The Java Language Specification* (SE 21 ed.). Oracle/Addison-Wesley. Especificación normativa de clases, herencia, sobrecarga y ligadura en Java. |

## Tier 2 — Documentación de lenguaje y herramientas (ejemplos e ilustración)

| ID | Referencia |
|---|---|
| `[ORACLE-JTUT]` | Oracle Corporation. *The Java Tutorials — Trail: Learning the Java Language (Classes and Objects, Interfaces and Inheritance)*. docs.oracle.com. Referencia práctica de sintaxis para los ejemplos de código del tema. |
| `[UML-DIAG-TYPES]` | Object Management Group. *UML 2.5.1 §9 — Classification of Diagrams* (formal/2017-12-05). Clasificación oficial de los 14 tipos de diagrama UML en estructurales y de comportamiento. |
| `[REFACTORING-GURU]` | Shvets, A. *Refactoring.Guru — Design Patterns*. Catálogo divulgativo de los 23 patrones GoF con ejemplos multi-lenguaje, usado como referencia de consulta rápida (no como fuente normativa). |

## Tier 3 — Marco de calidad e ingeniería del software (contexto, no contenido técnico nuclear)

| ID | Referencia |
|---|---|
| `[ISO25010]` | ISO/IEC 25010:2011 *Systems and software Quality Requirements and Evaluation (SQuaRE)* — mantenibilidad, modularidad, reutilización aplicadas al diseño OO. |
| `[ISO24765]` | ISO/IEC/IEEE 24765:2017 *Systems and software engineering — Vocabulary*. Definiciones normalizadas de clase, objeto, herencia, polimorfismo. |
| `[BOAM10032]` | BOAM 10.032 (23-dic-2025). Bases específicas TIC C1 Ayto. Madrid — temario oficial. |

---

*Las referencias Tier 1 fijan el fundamento teórico del paradigma OO (Booch, Meyer), los principios de diseño (Martin, Liskov), el catálogo de patrones (GoF) y el estándar de modelado (OMG UML, Rumbaugh/Jacobson/Booch), y son la base de todo el contenido; Tier 2 se cita en los ejemplos de código —escritos en **Java** (decisión de Joan, coherente con que el Tema 21 desarrolla la arquitectura Java EE)— y en la clasificación oficial de diagramas UML; Tier 3 enmarca la calidad y la vocabulario normalizado de ingeniería del software aplicables al puesto TIC del Ayuntamiento de Madrid.*
