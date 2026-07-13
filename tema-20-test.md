# Tema 20 — Test de Autoevaluación

> **Título**: Diseño y programación orientada a objetos. Objetos, clases, herencia, métodos, sobrecarga. Ventajas e inconvenientes. Patrones de diseño y UML.
> **Formato**: 60 preguntas tipo test A/B/C (formato oficial oposición)
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid
> **Versión**: v1.0 — Pendiente validación
> **Fecha**: 2026-07-13
> **Fuentes**: ver tema-20-fuentes.md

---

## Instrucciones

- Cada pregunta tiene **3 opciones** (A, B, C). Solo una es correcta.
- Penalización en examen real: respuesta incorrecta descuenta **1/3** del valor de una correcta.
- Tiempo orientativo: 1 minuto por pregunta.
- Distribución: Fundamentos y pilares de la POO (P1-P8), Clases, objetos, herencia, sobrecarga y polimorfismo (P9-P20), Ventajas e inconvenientes (P21-P30), Patrones de diseño (P31-P42), UML (P43-P56), Tendencias (P57-P60).

---

### Pregunta 1

**¿Qué teorema demuestra que cualquier algoritmo puede expresarse combinando secuencia, selección e iteración, marcando la transición hacia la programación estructurada?**

A) Teorema de Böhm-Jacopini
B) Teorema de Church-Turing
C) Teorema de Codd

<details><summary>Respuesta</summary>

**Correcta: A) Teorema de Böhm-Jacopini** Este teorema (1966) demuestra que cualquier programa puede escribirse con solo tres estructuras de control, fundamento de la programación estructurada que precede históricamente a la POO.

*Referencia: §1.1 [BOOCH07]*
</details>

---

### Pregunta 2

**¿Qué lenguaje se considera el primero en introducir el concepto de clases y objetos, orientado a la simulación de sistemas?**

A) Smalltalk
B) Simula 67
C) C++

<details><summary>Respuesta</summary>

**Correcta: B) Simula 67** Dahl y Nygaard lo crearon en 1967 para simular sistemas complejos; introduce por primera vez clases y objetos, raíz histórica del paradigma OO.

*Referencia: §1.1 [BOOCH07]*
</details>

---

### Pregunta 3

**¿Qué lenguaje populariza el término "orientado a objetos" y el envío de mensajes como mecanismo de interacción entre objetos?**

A) Java
B) Simula 67
C) Smalltalk

<details><summary>Respuesta</summary>

**Correcta: C) Smalltalk** Desarrollado en Xerox PARC en los años 70, consolida el vocabulario y la filosofía de la POO —incluido el envío de mensajes— antes de que C++ y Java la popularizasen en la industria.

*Referencia: §1.1 [BOOCH07]*
</details>

---

### Pregunta 4

**¿Qué pilar de la POO responde a la pregunta "qué hace un objeto", materializándose en su interfaz pública?**

A) Abstracción
B) Encapsulamiento
C) Herencia

<details><summary>Respuesta</summary>

**Correcta: A) Abstracción** Identifica las características esenciales de una entidad ignorando detalles irrelevantes, y se expresa en el conjunto de operaciones que el objeto ofrece al exterior.

*Referencia: §1.2 [MEYER97]*
</details>

---

### Pregunta 5

**¿Qué mecanismo oculta el estado interno de un objeto y restringe el acceso a él a través de una interfaz controlada?**

A) Polimorfismo
B) Encapsulamiento
C) Modularidad

<details><summary>Respuesta</summary>

**Correcta: B) Encapsulamiento** Protege los invariantes del objeto y permite cambiar la implementación interna sin romper el código cliente, siempre que la interfaz pública se mantenga.

*Referencia: §1.2 [MEYER97]*
</details>

---

### Pregunta 6

**Una clase cuyos atributos y métodos están fuertemente relacionados entre sí, contribuyendo todos a una única responsabilidad, tiene:**

A) Alto acoplamiento
B) Baja cohesión
C) Alta cohesión

<details><summary>Respuesta</summary>

**Correcta: C) Alta cohesión** El objetivo de diseño es alta cohesión combinada con bajo acoplamiento entre clases distintas.

*Referencia: §1.3 [SOMMERVILLE16]*
</details>

---

### Pregunta 7

**¿Qué principio SOLID establece que una clase debe tener una única razón para cambiar?**

A) Single Responsibility
B) Open/Closed
C) Liskov Substitution

<details><summary>Respuesta</summary>

**Correcta: A) Single Responsibility** Si una clase acumula más de una responsabilidad, tiene más de una razón para cambiar y debería dividirse.

*Referencia: §1.4 [MARTIN03]*
</details>

---

### Pregunta 8

**El principio de sustitución de Liskov exige que:**

A) Una clase dependa siempre de implementaciones concretas
B) Un objeto de una subclase pueda sustituir a uno de la superclase sin alterar la corrección del programa
C) Una interfaz agrupe todos los métodos posibles de un dominio

<details><summary>Respuesta</summary>

**Correcta: B) Un objeto de una subclase pueda sustituir a uno de la superclase sin alterar la corrección del programa** Formulado por Liskov y Wing (1994); si una subclase devuelve valores o lanza excepciones no esperadas por el código que trata con la superclase, se viola LSP.

*Referencia: §1.4 [LISKOV94]*
</details>

---

### Pregunta 9

**La plantilla que define atributos y métodos comunes a un conjunto de entidades se denomina:**

A) Objeto
B) Instancia
C) Clase

<details><summary>Respuesta</summary>

**Correcta: C) Clase** Una clase no ocupa memoria de datos en tiempo de ejecución; es una definición. Un objeto, instancia concreta de una clase, sí.

*Referencia: §2.1 [BOOCH07]*
</details>

---

### Pregunta 10

**¿Qué mecanismo libera automáticamente la memoria de un objeto en Java cuando ya no existe ninguna referencia alcanzable a él?**

A) El recolector de basura (garbage collector)
B) El destructor explícito
C) El operador delete

<details><summary>Respuesta</summary>

**Correcta: A) El recolector de basura (garbage collector)** A diferencia de C++, Java gestiona automáticamente la destrucción de objetos; el programador no invoca `delete`.

*Referencia: §2.1 [GOSLING-JLS]*
</details>

---

### Pregunta 11

**Un atributo declarado como `static` en Java:**

A) Tiene una copia distinta por cada objeto de la clase
B) Tiene una única copia compartida por todos los objetos de la clase
C) Solo existe dentro de un método

<details><summary>Respuesta</summary>

**Correcta: B) Tiene una única copia compartida por todos los objetos de la clase** Se accede sin instancia, con el nombre de la clase (p. ej. `Expediente.getTotalAbiertos()`).

*Referencia: §2.2 [GOSLING-JLS]*
</details>

---

### Pregunta 12

**El constructor de una clase en Java se caracteriza por:**

A) Ser siempre estático
B) Ejecutarse solo una vez para toda la clase
C) Tener el mismo nombre que la clase y no declarar tipo de retorno

<details><summary>Respuesta</summary>

**Correcta: C) Tener el mismo nombre que la clase y no declarar tipo de retorno** Se invoca automáticamente al crear un objeto con `new`, y su responsabilidad es dejarlo en un estado inicial válido.

*Referencia: §2.2 [GOSLING-JLS]*
</details>

---

### Pregunta 13

**Un atributo `private` de una clase Java es accesible desde:**

A) Únicamente la propia clase
B) Cualquier clase del mismo paquete
C) Cualquier subclase, esté o no en el mismo paquete

<details><summary>Respuesta</summary>

**Correcta: A) Únicamente la propia clase** Es el nivel de visibilidad más restrictivo de los cuatro que define Java.

*Referencia: §2.3 [GOSLING-JLS]*
</details>

---

### Pregunta 14

**Un método `protected` es visible desde:**

A) Solo la propia clase
B) La propia clase, el mismo paquete y las subclases de otros paquetes
C) Cualquier clase del programa, sin restricción

<details><summary>Respuesta</summary>

**Correcta: B) La propia clase, el mismo paquete y las subclases de otros paquetes** Es el nivel pensado para que las subclases reutilicen o sobrescriban el miembro, sin exponerlo públicamente.

*Referencia: §2.3 [GOSLING-JLS]*
</details>

---

### Pregunta 15

**Java resuelve el problema del diamante de la herencia múltiple:**

A) Permitiendo herencia múltiple de clases con reglas de precedencia
B) Obligando a declarar todas las clases como abstractas
C) Prohibiendo la herencia múltiple de clases, pero permitiendo implementar varias interfaces

<details><summary>Respuesta</summary>

**Correcta: C) Prohibiendo la herencia múltiple de clases, pero permitiendo implementar varias interfaces** `extends` admite una única superclase; `implements` admite varias interfaces, evitando el conflicto de estado del diamante.

*Referencia: §2.4 [GOSLING-JLS; MEYER97]*
</details>

---

### Pregunta 16

**La relación que modela la herencia entre dos clases se describe habitualmente como:**

A) "es un" (is-a)
B) "tiene un" (has-a)
C) "usa un" (uses-a)

<details><summary>Respuesta</summary>

**Correcta: A) "es un" (is-a)** `ExpedienteLicencia` **es un** `Expediente`. La relación "tiene un" (has-a) corresponde a composición o agregación, no a herencia.

*Referencia: §2.4 [BOOCH07]*
</details>

---

### Pregunta 17

**La sobrecarga (overloading) de métodos se resuelve:**

A) En tiempo de ejecución, según la clase real del objeto
B) En tiempo de compilación, según los tipos de los argumentos de la llamada
C) De forma aleatoria según el orden de declaración

<details><summary>Respuesta</summary>

**Correcta: B) En tiempo de compilación, según los tipos de los argumentos de la llamada** Es ligadura estática: el compilador decide qué versión del método invocar antes de ejecutar el programa.

*Referencia: §2.5 [GOSLING-JLS §8.4]*
</details>

---

### Pregunta 18

**La sobrescritura (overriding) de un método exige que la subclase declare:**

A) Un método con distinto número de parámetros
B) Un atributo con el mismo nombre que un método heredado
C) Un método con la misma firma que el de la superclase

<details><summary>Respuesta</summary>

**Correcta: C) Un método con la misma firma que el de la superclase** Se marca opcionalmente con `@Override`; si la firma difiere, no hay sobrescritura, sino sobrecarga (o un error si no coincide con ningún método heredado).

*Referencia: §2.5 [GOSLING-JLS §8.4]*
</details>

---

### Pregunta 19

**El mecanismo por el cual la JVM decide, en tiempo de ejecución, qué versión de un método invocar según la clase real del objeto se llama:**

A) Ligadura dinámica
B) Ligadura estática
C) Sobrecarga

<details><summary>Respuesta</summary>

**Correcta: A) Ligadura dinámica** También llamada tardía (*late binding*); es la base técnica del polimorfismo.

*Referencia: §2.6 [BOOCH07]*
</details>

---

### Pregunta 20

**El principio de diseño de GoF "favorece la composición sobre la herencia" advierte principalmente contra:**

A) El uso de interfaces en Java
B) El uso indiscriminado de herencia para reutilizar código cuando la relación real es "tiene un"
C) La sobrecarga de constructores

<details><summary>Respuesta</summary>

**Correcta: B) El uso indiscriminado de herencia para reutilizar código cuando la relación real es "tiene un"** La herencia crea un acoplamiento muy fuerte (problema de la clase base frágil); la composición permite reconfigurar comportamiento en tiempo de ejecución.

*Referencia: §2.7 [GOF94, cap. 1]*
</details>

---

### Pregunta 21

**¿Qué afirmación describe correctamente el coste del software a lo largo de su ciclo de vida?**

A) El coste total del software se concentra siempre en la fase de análisis de requisitos
B) El mantenimiento del software orientado a objetos es gratuito gracias al encapsulamiento
C) La mayor parte del coste total del software corresponde históricamente al mantenimiento, no al desarrollo inicial

<details><summary>Respuesta</summary>

**Correcta: C) La mayor parte del coste total del software corresponde históricamente al mantenimiento, no al desarrollo inicial** Esta es la justificación económica última de perseguir mantenibilidad mediante encapsulamiento y modularidad.

*Referencia: §3.1 [PRESSMAN14, cap. 20]*
</details>

---

### Pregunta 22

**¿Qué ventaja de la POO facilita la comunicación entre el equipo técnico y los expertos del dominio de negocio?**

A) La correspondencia directa entre las clases del modelo y las entidades del mundo real del problema
B) La ausencia de documentación en el código
C) La eliminación completa de las pruebas unitarias

<details><summary>Respuesta</summary>

**Correcta: A) La correspondencia directa entre las clases del modelo y las entidades del mundo real del problema** Clases como `Expediente` o `Ciudadano` reducen la distancia conceptual entre modelo y sistema.

*Referencia: §3.1 [PRESSMAN14]*
</details>

---

### Pregunta 23

**Cuando un fallo en la implementación interna de una clase no altera su interfaz pública ni sus invariantes, y por tanto no se propaga en cascada, se dice que el sistema logra:**

A) Herencia múltiple
B) Aislamiento de errores
C) Sobrecarga de operadores

<details><summary>Respuesta</summary>

**Correcta: B) Aislamiento de errores** Es una consecuencia directa del encapsulamiento y facilita las pruebas unitarias por clase.

*Referencia: §3.2 [PRESSMAN14]*
</details>

---

### Pregunta 24

**La escalabilidad del equipo de desarrollo en un proyecto OO se ve favorecida principalmente por:**

A) El uso exclusivo de variables globales compartidas
B) La ausencia de una jerarquía de herencia
C) La división en clases con responsabilidades delimitadas e interfaces bien definidas

<details><summary>Respuesta</summary>

**Correcta: C) La división en clases con responsabilidades delimitadas e interfaces bien definidas** Permite que distintos desarrolladores trabajen en paralelo con interferencia mínima.

*Referencia: §3.2 [SOMMERVILLE16]*
</details>

---

### Pregunta 25

**Uno de los principales costes formativos de la POO frente a la programación estructurada básica es:**

A) Una curva de aprendizaje más larga, al exigir dominar simultáneamente abstracción, encapsulamiento, herencia y polimorfismo
B) La imposibilidad de reutilizar código entre proyectos
C) La obligación de usar siempre herencia múltiple

<details><summary>Respuesta</summary>

**Correcta: A) Una curva de aprendizaje más larga, al exigir dominar simultáneamente abstracción, encapsulamiento, herencia y polimorfismo** Errores conceptuales tempranos suelen arrastrarse y ser costosos de corregir más adelante.

*Referencia: §3.3 [PRESSMAN14]*
</details>

---

### Pregunta 26

**Un mal diseño OO inicial puede resultar más rígido de modificar que el equivalente estructurado, sobre todo debido a:**

A) La ausencia total de clases en el sistema
B) El acoplamiento fuerte que introduce una jerarquía de herencia extensa y profunda
C) El uso de comentarios en el código fuente

<details><summary>Respuesta</summary>

**Correcta: B) El acoplamiento fuerte que introduce una jerarquía de herencia extensa y profunda** Un cambio en una superclase puede romper subclases: el problema de la clase base frágil.

*Referencia: §3.3 [GOF94]*
</details>

---

### Pregunta 27

**El coste en rendimiento de la ligadura dinámica frente a una llamada resuelta en compilación se debe principalmente a:**

A) La necesidad de recompilar el programa en cada ejecución
B) La ausencia de modificadores de acceso en el lenguaje
C) Una consulta indirecta a la tabla de métodos de la clase real del objeto en cada invocación

<details><summary>Respuesta</summary>

**Correcta: C) Una consulta indirecta a la tabla de métodos de la clase real del objeto en cada invocación** Esta indirección es más costosa que una llamada directa resuelta en compilación.

*Referencia: §3.4 [GOSLING-JLS]*
</details>

---

### Pregunta 28

**La creación y destrucción frecuente de muchos objetos de vida corta en Java incrementa la presión sobre:**

A) El recolector de basura (garbage collector)
B) El compilador estático de tipos
C) El motor de renderizado gráfico

<details><summary>Respuesta</summary>

**Correcta: A) El recolector de basura (garbage collector)** Puede introducir pausas apreciables en sistemas de alto rendimiento o tiempo real.

*Referencia: §3.4 [GOSLING-JLS]*
</details>

---

### Pregunta 29

**Una clase que acumula demasiadas responsabilidades y conoce/controla la mayor parte del sistema, violando el principio de responsabilidad única, se conoce como el anti-patrón:**

A) Factory Method
B) God Object
C) Singleton

<details><summary>Respuesta</summary>

**Correcta: B) God Object** Concentra un acoplamiento extremo y es contrario al SRP (§1.4).

*Referencia: §3.5 [GOF94]*
</details>

---

### Pregunta 30

**¿Qué disciplina de diseño evita que las ventajas teóricas de la POO se conviertan, en la práctica, en un sistema difícil de mantener?**

A) La eliminación de todas las relaciones de herencia del sistema
B) La sustitución completa de las clases por funciones globales
C) La aplicación de SOLID, patrones de diseño y revisión del acoplamiento

<details><summary>Respuesta</summary>

**Correcta: C) La aplicación de SOLID, patrones de diseño y revisión del acoplamiento** No es opcional en sistemas OO de tamaño medio o grande.

*Referencia: §3.5 [MARTIN03]*
</details>

---

### Pregunta 31

**Un patrón de diseño es, según GoF:**

A) Una solución general y reutilizable a un problema de diseño OO recurrente, no código listo para copiar
B) Un fragmento de código que se copia literalmente en cada proyecto
C) Una regla obligatoria del compilador de Java

<details><summary>Respuesta</summary>

**Correcta: A) Una solución general y reutilizable a un problema de diseño OO recurrente, no código listo para copiar** Es una plantilla conceptual que se adapta a cada situación concreta.

*Referencia: §4.1 [GOF94, cap. 1]*
</details>

---

### Pregunta 32

**¿Cuántos patrones componen el catálogo original de Gamma, Helm, Johnson y Vlissides (Gang of Four)?**

A) 12
B) 23
C) 30

<details><summary>Respuesta</summary>

**Correcta: B) 23** Distribuidos en 5 creacionales, 7 estructurales y 11 de comportamiento.

*Referencia: §4.1 [GOF94]*
</details>

---

### Pregunta 33

**Cada patrón GoF documenta, entre otros elementos:**

A) Únicamente el nombre del patrón y su autor
B) El número de líneas de código que ocupa su implementación
C) Intención, aplicabilidad, estructura (mini diagrama de clases) y consecuencias

<details><summary>Respuesta</summary>

**Correcta: C) Intención, aplicabilidad, estructura (mini diagrama de clases) y consecuencias** Este formato da a los equipos un vocabulario común de diseño.

*Referencia: §4.1 [GOF94]*
</details>

---

### Pregunta 34

**Una solución frecuente en la práctica pero contraproducente a medio o largo plazo, que suele surgir de aplicar un patrón fuera de contexto, se denomina:**

A) Anti-patrón
B) Patrón estructural
C) Diagrama de despliegue

<details><summary>Respuesta</summary>

**Correcta: A) Anti-patrón** Ejemplos: God Object, Spaghetti Code orientado a objetos, Golden Hammer.

*Referencia: §4.2 [GOF94]*
</details>

---

### Pregunta 35

**El anti-patrón que consiste en aplicar sistemáticamente un mismo patrón conocido a cualquier problema, por familiaridad del equipo, se llama:**

A) Factory Method
B) Golden Hammer (martillo de oro)
C) Composite

<details><summary>Respuesta</summary>

**Correcta: B) Golden Hammer (martillo de oro)** Se aplica el patrón conocido aunque no encaje realmente con el problema.

*Referencia: §4.2 [GOF94]*
</details>

---

### Pregunta 36

**Usar `extends` únicamente para reutilizar código de una clase con la que no existe una relación "es un" real es un ejemplo de:**

A) Principio de inversión de dependencias
B) Patrón Observer
C) Herencia por conveniencia

<details><summary>Respuesta</summary>

**Correcta: C) Herencia por conveniencia** Genera jerarquías semánticamente falsas y es uno de los anti-patrones más citados en diseño OO.

*Referencia: §4.2 [GOF94]*
</details>

---

### Pregunta 37

**¿Cuántos patrones creacionales componen el catálogo GoF?**

A) 5
B) 7
C) 11

<details><summary>Respuesta</summary>

**Correcta: A) 5** Singleton, Factory Method, Abstract Factory, Builder y Prototype.

*Referencia: §4.3 [GOF94]*
</details>

---

### Pregunta 38

**El patrón creacional que garantiza que una clase tenga una única instancia global y proporciona un punto de acceso a ella es:**

A) Builder
B) Singleton
C) Prototype

<details><summary>Respuesta</summary>

**Correcta: B) Singleton** Útil, por ejemplo, para un gestor de configuración cargado una sola vez.

*Referencia: §4.3 [GOF94]*
</details>

---

### Pregunta 39

**El patrón que define una interfaz para crear un objeto, dejando que las subclases decidan qué clase concreta instanciar, es:**

A) Adapter
B) Observer
C) Factory Method

<details><summary>Respuesta</summary>

**Correcta: C) Factory Method** Desacopla al código cliente de las clases concretas que finalmente se crean.

*Referencia: §4.3 [GOF94]*
</details>

---

### Pregunta 40

**¿Cuántos patrones estructurales componen el catálogo GoF?**

A) 7
B) 5
C) 11

<details><summary>Respuesta</summary>

**Correcta: A) 7** Adapter, Bridge, Composite, Decorator, Facade, Flyweight y Proxy.

*Referencia: §4.4 [GOF94]*
</details>

---

### Pregunta 41

**El patrón estructural que proporciona una interfaz unificada y simplificada a un conjunto de interfaces de un subsistema complejo es:**

A) Decorator
B) Facade
C) Bridge

<details><summary>Respuesta</summary>

**Correcta: B) Facade** Oculta la complejidad interna de un subsistema tras un punto de entrada único.

*Referencia: §4.4 [GOF94]*
</details>

---

### Pregunta 42

**El patrón de comportamiento que encapsula una familia de algoritmos intercambiables tras una interfaz común, seleccionable en tiempo de ejecución, es:**

A) Visitor
B) Memento
C) Strategy

<details><summary>Respuesta</summary>

**Correcta: C) Strategy** Aplicable, por ejemplo, a los distintos canales de notificación a un ciudadano (§1.4).

*Referencia: §4.5 [GOF94]*
</details>

---

### Pregunta 43

**UML surge de la unificación de tres notaciones de modelado OO previas:**

A) El método Booch, la OMT de Rumbaugh y el OOSE de Jacobson
B) El álgebra relacional, el cálculo relacional y SQL
C) Los diagramas de flujo de datos, los flujogramas y los pseudocódigos

<details><summary>Respuesta</summary>

**Correcta: A) El método Booch, la OMT de Rumbaugh y el OOSE de Jacobson** Sus autores, «los tres amigos», unieron sus notaciones en Rational Software a partir de 1994.

*Referencia: §5.1 [RUMBAUGH05, prefacio]*
</details>

---

### Pregunta 44

**¿Qué organismo adopta y mantiene el estándar UML desde 1997?**

A) ISO (International Organization for Standardization)
B) OMG (Object Management Group)
C) W3C (World Wide Web Consortium)

<details><summary>Respuesta</summary>

**Correcta: B) OMG (Object Management Group)** Mantiene desde entonces las sucesivas versiones, hasta la vigente UML 2.5.1 (2017).

*Referencia: §5.1 [OMG-UML25]*
</details>

---

### Pregunta 45

**UML debe entenderse principalmente como:**

A) Una metodología de desarrollo obligatoria
B) Un lenguaje de programación orientado a objetos
C) Una notación gráfica, sin prescribir un proceso de desarrollo concreto

<details><summary>Respuesta</summary>

**Correcta: C) Una notación gráfica, sin prescribir un proceso de desarrollo concreto** Puede usarse en metodologías predictivas o ágiles, según las necesidades del proyecto.

*Referencia: §5.1 [OMG-UML25]*
</details>

---

### Pregunta 46

**Los estereotipos como `«interface»` o `«actor»` son un ejemplo de:**

A) Mecanismo de extensibilidad de UML
B) Un tipo de diagrama de comportamiento
C) Un modificador de acceso de Java

<details><summary>Respuesta</summary>

**Correcta: A) Mecanismo de extensibilidad de UML** Permiten adaptar la notación estándar a necesidades específicas de un dominio sin crear un lenguaje nuevo.

*Referencia: §5.2 [OMG-UML25, §7]*
</details>

---

### Pregunta 47

**El diagrama UML más utilizado en la práctica, y con frecuencia el único elaborado por completo en proyectos pequeños, es el:**

A) Diagrama de Despliegue
B) Diagrama de Clases
C) Diagrama de Temporización

<details><summary>Respuesta</summary>

**Correcta: B) Diagrama de Clases** Representa clases, atributos, métodos y relaciones con una caja de tres compartimentos.

*Referencia: §5.3 [FOWLER-UML, cap. 5]*
</details>

---

### Pregunta 48

**En la notación de un diagrama de clases UML, un rombo relleno en el extremo de una relación representa:**

A) Agregación
B) Asociación simple
C) Composición

<details><summary>Respuesta</summary>

**Correcta: C) Composición** El rombo hueco, en cambio, representa agregación (dependencia de ciclo de vida más débil).

*Referencia: §5.3 [RUMBAUGH05]*
</details>

---

### Pregunta 49

**A diferencia del diagrama de clases, el Diagrama de Objetos UML representa:**

A) Una instantánea de instancias concretas en un momento dado, con sus valores de atributo reales
B) Los nodos de hardware sobre los que se despliega el sistema
C) La secuencia temporal de mensajes entre objetos

<details><summary>Respuesta</summary>

**Correcta: A) Una instantánea de instancias concretas en un momento dado, con sus valores de atributo reales** Útil para ilustrar ejemplos concretos de una relación compleja o depurar un estado del sistema.

*Referencia: §5.3 [FOWLER-UML]*
</details>

---

### Pregunta 50

**El Diagrama de Clases UML se diferencia del modelo Entidad-Relación (Tema 16) principalmente en que:**

A) El E/R incluye siempre métodos y el diagrama de clases nunca
B) El diagrama de clases modela datos y comportamiento juntos (con métodos), mientras que el E/R modela datos persistentes para una base de datos relacional
C) Ambos son exactamente el mismo diagrama con distinto nombre

<details><summary>Respuesta</summary>

**Correcta: B) El diagrama de clases modela datos y comportamiento juntos (con métodos), mientras que el E/R modela datos persistentes para una base de datos relacional** Un mismo concepto del dominio puede aparecer en ambos con contenido distinto.

*Referencia: §5.3 [FOWLER-UML]*
</details>

---

### Pregunta 51

**El diagrama UML que representa la arquitectura física, es decir, los nodos de hardware y sus conexiones de red, es el:**

A) Diagrama de Componentes
B) Diagrama de Paquetes
C) Diagrama de Despliegue

<details><summary>Respuesta</summary>

**Correcta: C) Diagrama de Despliegue** (*deployment*) muestra sobre qué servidores o dispositivos se despliegan los artefactos software.

*Referencia: §5.4 [OMG-UML25]*
</details>

---

### Pregunta 52

**¿Cuántos tipos de diagrama estructural define UML 2.5?**

A) 7
B) 5
C) 14

<details><summary>Respuesta</summary>

**Correcta: A) 7** Clases, Objetos, Componentes, Despliegue, Paquetes, Estructura Compuesta y Perfiles (más 7 de comportamiento = 14 en total).

*Referencia: §5.4 [UML-DIAG-TYPES]*
</details>

---

### Pregunta 53

**En un Diagrama de Casos de Uso, la relación `«include»` indica:**

A) Que un actor puede realizar la acción de forma opcional
B) Que un caso de uso incorpora obligatoriamente la funcionalidad de otro, reutilizada
C) Que dos actores son en realidad el mismo rol

<details><summary>Respuesta</summary>

**Correcta: B) Que un caso de uso incorpora obligatoriamente la funcionalidad de otro, reutilizada** Frente a `«extend»`, que representa funcionalidad opcional bajo ciertas condiciones.

*Referencia: §5.5 [OMG-UML25]*
</details>

---

### Pregunta 54

**En un Diagrama de Secuencia, el tiempo avanza:**

A) De izquierda a derecha, sobre líneas de vida horizontales
B) En sentido circular alrededor de los objetos
C) De arriba abajo, sobre líneas de vida verticales

<details><summary>Respuesta</summary>

**Correcta: C) De arriba abajo, sobre líneas de vida verticales** Los mensajes se dibujan como flechas horizontales entre líneas de vida, en el orden temporal exacto en que se producen.

*Referencia: §5.6 [FOWLER-UML]*
</details>

---

### Pregunta 55

**El Diagrama de Comunicación (o de Colaboración) se diferencia del de Secuencia en que:**

A) Organiza a los objetos espacialmente como un grafo, numerando los mensajes para indicar el orden, en lugar de usar la posición vertical
B) No permite representar el envío de mensajes entre objetos
C) Solo puede usarse para modelar bases de datos relacionales

<details><summary>Respuesta</summary>

**Correcta: A) Organiza a los objetos espacialmente como un grafo, numerando los mensajes para indicar el orden, en lugar de usar la posición vertical** Ambos diagramas son semánticamente equivalentes; difieren en el énfasis visual.

*Referencia: §5.6 [OMG-UML25]*
</details>

---

### Pregunta 56

**El Diagrama de Máquina de Estados es especialmente útil para modelar:**

A) La arquitectura física de red del sistema
B) Los distintos estados por los que pasa un objeto a lo largo de su vida y las transiciones entre ellos
C) La lista de atributos privados de una clase

<details><summary>Respuesta</summary>

**Correcta: B) Los distintos estados por los que pasa un objeto a lo largo de su vida y las transiciones entre ellos** Heredero del *statechart* de Harel; el patrón State (§4.5) es su implementación en código.

*Referencia: §5.7 [OMG-UML25]*
</details>

---

### Pregunta 57

**Las expresiones lambda e interfaces funcionales incorporadas en Java desde la versión 8 permiten, en muchos casos:**

A) Eliminar por completo la necesidad de usar clases en Java
B) Sustituir la herencia múltiple de C++ dentro de Java
C) Sustituir una implementación completa del patrón Strategy por una alternativa más ligera, sin abandonar el modelo de clases y objetos

<details><summary>Respuesta</summary>

**Correcta: C) Sustituir una implementación completa del patrón Strategy por una alternativa más ligera, sin abandonar el modelo de clases y objetos** Reflejan la influencia de la programación funcional sobre los lenguajes OO modernos.

*Referencia: §6 [GOSLING-JLS]*
</details>

---

### Pregunta 58

**El Diseño Dirigido por el Dominio (Domain-Driven Design) extiende explícitamente al diseño de servicios distribuidos:**

A) Conceptos de modelado OO como entidades con identidad, objetos de valor inmutables y agregados como unidad de consistencia
B) La programación no estructurada basada en saltos GOTO
C) La eliminación de todo vocabulario compartido con el negocio

<details><summary>Respuesta</summary>

**Correcta: A) Conceptos de modelado OO como entidades con identidad, objetos de valor inmutables y agregados como unidad de consistencia** DDD refuerza, más que sustituye, los fundamentos de la POO clásica.

*Referencia: §6 [BOOCH07]*
</details>

---

### Pregunta 59

**La inyección de dependencias, hoy sistematizada como mecanismo de plataforma en los grandes frameworks Java, es una forma sistematizada de:**

A) El problema del diamante de la herencia múltiple
B) El principio de inversión de dependencias (DIP) y del patrón Factory
C) El anti-patrón God Object

<details><summary>Respuesta</summary>

**Correcta: B) El principio de inversión de dependencias (DIP) y del patrón Factory** Reduce la necesidad de implementar manualmente Factory Method o Abstract Factory en cada proyecto.

*Referencia: §6 [MARTIN03; GOF94]*
</details>

---

### Pregunta 60

**El modelado ejecutable y la generación de código a partir de diagramas de clases UML, con ida y vuelta entre modelo y código, se conoce como:**

A) Garbage collection
B) Ligadura estática
C) Round-trip engineering

<details><summary>Respuesta</summary>

**Correcta: C) Round-trip engineering** Tendencia actual de las herramientas de modelado, sin renunciar a la semántica formal del estándar OMG.

*Referencia: §6 [OMG-UML25]*
</details>
