# Tema 20 — Changelog

> **Título oficial**: Diseño y programación orientada a objetos. Objetos, clases, herencia, métodos, sobrecarga. Ventajas e inconvenientes. Patrones de diseño y UML.

---

## v1.1 — 2026-09-06 — Ficha de extensión y tiempo de estudio

**Estado**: sin cambios de contenido. Solo se añade información sobre el propio tema.

**Motivo**: petición del IAM (Jesús Cuadrado, 02-09-2026) al validar el Tema 30. Acepta la extensión de los temas «compuestos» a condición de que se informe de «su extensión en palabras y tiempo estimado de estudio». Al revisarlo se vio que ese dato solo aparecía en 16 de los 40 temas, y que faltaba justo en los más largos.

### Alcance

- Ficha bajo la cabecera del tema, y al final de la pestaña Índice donde esa pestaña existe:
  - **Extensión**: ~8.600 palabras · 12 diagramas · 60 preguntas de test
  - **Tiempo estimado de estudio**: 10-12 horas (primera vuelta completa, sin contar repasos)
- La cifra de palabras de la tabla de entregables se sincroniza con la ficha, para que el tema no muestre dos recuentos distintos.
- Las horas salen de una fórmula común a los 40 temas, para que sean comparables entre sí: contenido a 1.500 palabras/hora (ritmo de estudio activo), diagramas a una hora por cada cinco y test a dos minutos por pregunta. Se publica como intervalo de dos horas.
- Generado con `_tools-qa/ficha_estudio.py`, idempotente y reejecutable tras cualquier regeneración con `build_tNN.py`.

---

## v1.0 — 2026-07-13 — Primera versión

**Estado**: pendiente de validación por María y Ana, y de revisión técnica del IAM (Jesús Cuadrado).

**Motivo**: desarrollo del Tema 20, dentro de la serie de temas técnicos generados desde cero (tras T13-T19), replicando la estructura y el formato de los Temas 1, 11, 18 y 19 ya consolidados, con pestaña Índice y listas anidadas correctas desde el inicio.

### Alcance de la v1.0

| Entregable | Cantidad |
|---|---|
| Contenido teórico | ~8.260 palabras · 6 secciones (4 del esqueleto oficial + Elementos/Componentes desglosado + Tendencias) con 29 epígrafes |
| Diagramas SVG inline | 12 (accesibles con `role`/`aria-label`, clases con sufijo único anti-colisión) |
| Banco de preguntas tipo test | 60 preguntas A/B/C con explicación y referencia, balanceadas **20/20/20** por construcción (asignación cíclica de la posición de la opción correcta) |
| Casos prácticos | 3 (diseño de clases con herencia/sobrecarga sobre licencias de obra y terraza; patrones Factory Method + Strategy sobre alta y notificación de expedientes; modelado UML — clases, casos de uso y secuencia — del mismo flujo) · 10 puntos cada uno |
| Fuentes Tier 1 | 13 referencias canónicas (Booch, Meyer, Gang of Four, Martin, Liskov-Wing, OMG UML 2.5.1, Rumbaugh/Jacobson/Booch, Fowler, Larman, Sommerville, Pressman, Gosling — Java Language Specification) |

### Decisiones de generación

1. **Sin material de cliente**: solo el esqueleto `Test_Prompting/temas junio/20.md` (corregida una errata de origen: "Mecansmos avanzadps" → "Mecanismos avanzados"). Desarrollado desde fuentes canónicas del paradigma OO, el catálogo GoF y el estándar UML, todas referenciadas.
2. **Estructura fiel al esqueleto oficial, con aplanado de subniveles H4** (mismo criterio que T18 con "Programación modular"): los epígrafes `####` del borrador (p. ej. los cinco hijos de "Mecanismos avanzados en POO") se promovieron a subsecciones `X.Y` hermanas, evitando un cuarto nivel de numeración no usado en el resto de la serie.
3. **Ejemplos de código en Java** (decisión de Joan, confirmada antes de generar): coherente con que el Tema 21 desarrolla la arquitectura Java EE justo a continuación, y con que Java es el lenguaje OOP más citado en temarios TIC de AAPP españolas. Se usa una única jerarquía de ejemplo (`Expediente → ExpedienteLicencia / ExpedienteTributario`) hilada a través de todo el contenido, los diagramas y los tres casos.
4. **Estándar de alcance idéntico a T18/T19** (decisión de Joan, confirmada antes de generar): 12 diagramas SVG, 60 preguntas de test, 3 casos prácticos.
5. **Diferenciación explícita UML ↔ Tema 16** (decisión de Joan, confirmada antes de generar): se añadió un callout `[REFERENCIA CRUZADA]` en §5.3 y otro en §5.5 aclarando que el Diagrama de Clases UML no sustituye al modelo Entidad-Relación (datos persistentes, Tema 16-17), y que el Diagrama de Casos de Uso cumple un papel análogo pero distinto al de los DFD del análisis estructurado clásico (también Tema 16), para evitar que ambos temas se traten como notaciones intercambiables.
6. **Sección «Tendencias actuales» con marco duradero** (mismo criterio que T18/T19): programación funcional en Java (lambdas), Domain-Driven Design, sistematización de la inyección de dependencias como forma de DIP + Factory, y modelado ejecutable/round-trip engineering — sin números de versión de producto que caduquen.
7. **Contexto Ayuntamiento de Madrid** en casos y ejemplos (expedientes de licencia de obra y terraza, notificaciones a ciudadanos por sede electrónica/correo/SMS, Área de Urbanismo).
8. **Frontera con temas vecinos** cuidada: procedimientos/funciones genéricos y recursividad al Tema 18; SQL, procedimientos almacenados y disparadores (paralelo explícito con el patrón Observer, §4.5) al Tema 19; arquitectura Java EE y contenedores de inyección de dependencias al Tema 21; seguridad en el desarrollo al Tema 25.
9. **Referencias cruzadas validadas contra BOAM 10.032**: T7 (ciclo de vida de un expediente LPACAP, paralelo con el Diagrama de Máquina de Estados), T16, T18, T19, T21, T22, T25. Todas comprobadas.
10. **Anti-colisión de SVG**: las clases CSS de cada diagrama llevan **sufijo numérico único** (`.t1`…`.t12`, `.h1`…`.h12`), evitando el bug sistémico de estilos que leakean entre los 12 SVG embebidos en la misma página (lección de T5).
11. **Balance del test por construcción, no por conteo manual**: la posición de la opción correcta se fijó por una regla cíclica (pregunta *n* → A si *n* mod 3 = 1, B si = 2, C si = 0) en lugar de contar a posteriori, garantizando 20/20/20 exacto desde el primer borrador.

### Pendientes para QA / próxima iteración

- Validación de profundidad por María/Ana/IAM (¿alguna sección a ampliar o recortar, especialmente el bloque UML de §5, el más extenso del tema?).
- Confirmación de si, además de Java, interesa una nota comparativa con otro lenguaje OO si el Ayuntamiento usa otro en producción para algún sistema legado.
- Verificación ortográfica con corrector es_ES (cuidado con falsos positivos por términos técnicos en inglés: overloading, overriding, binding, framework, singleton, facade, timestamp…).

### Origen

Generado el 2026-07-13 en el flujo de trabajo de eTrivium, replicando el patrón de los Temas 1 (v2.1), 11 (v3.2), 18 (v1.0) y 19 (v1.0). `build_t20.py` y `_build_css.txt` persistidos en el repo.
