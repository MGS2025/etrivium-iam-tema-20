# Tema 20 — Contenido Teórico

> **Título oficial**: Diseño y programación orientada a objetos. Objetos, clases, herencia, métodos, sobrecarga. Ventajas e inconvenientes. Patrones de diseño y UML.
>
> **Bloque**: Parte II — Técnico
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid
> **Versión**: v1.0 — Pendiente validación
> **Fecha generación**: 2026-07-13
> **Fuentes**: Ver tema-20-fuentes.md · **Diagramas**: Ver tema-20-diagramas.md · **Cambios**: Ver tema-20-changelog.md
>
> *Extensión: ~8.260 palabras · 12 diagramas SVG embebidos · 4 tipos de callout transversales*

---

## Convenciones del documento

Este tema incluye cuatro tipos de **cajas callout** para facilitar el estudio:

> **[DATO CLAVE EXAMEN]** Información de alta densidad memorística, con alta probabilidad de aparecer en el test oficial.

> **[EJERCICIO RESUELTO]** Problema + solución paso a paso (una clase, una jerarquía, un patrón aplicado).

> **[EJEMPLO AYTO MADRID]** Aplicación real de la teoría al entorno municipal (expedientes, licencias, tributos, notificaciones).

> **[REFERENCIA CRUZADA]** Enlace conceptual a otros temas del temario oficial.

Los ejemplos de código se escriben en **Java** (decisión de Joan, coherente con que el Tema 21 desarrolla la arquitectura Java EE justo a continuación). Cuando un concepto es independiente del lenguaje (p. ej. el problema del diamante en herencia múltiple, presente en C++ pero no en Java) se advierte explícitamente. Las fuentes se citan con etiquetas breves tipo `[GOF94]` o `[BOOCH07, cap. 2]`; el registro completo está en `tema-20-fuentes.md`.

**Jerarquía de ejemplo usada en todo el tema** (contexto Ayuntamiento de Madrid, simplificada, sobre la tramitación de expedientes):

```java
public abstract class Expediente {
    private String idExpediente;
    private String estado;
    protected LocalDate fechaApertura;

    public Expediente(String idExpediente, LocalDate fechaApertura) {
        this.idExpediente = idExpediente;
        this.fechaApertura = fechaApertura;
        this.estado = "ABIERTO";
    }

    public abstract int calcularPlazoResolucion();

    public String getEstado() { return estado; }
    protected void setEstado(String estado) { this.estado = estado; }
}

public class ExpedienteLicencia extends Expediente {
    private String tipoLicencia; // "OBRA_MENOR" | "OBRA_MAYOR" | "ACTIVIDAD"

    public ExpedienteLicencia(String id, LocalDate apertura, String tipoLicencia) {
        super(id, apertura);
        this.tipoLicencia = tipoLicencia;
    }

    @Override
    public int calcularPlazoResolucion() {
        return "OBRA_MAYOR".equals(tipoLicencia) ? 90 : 30;
    }
}

public class ExpedienteTributario extends Expediente {
    private double importe;

    public ExpedienteTributario(String id, LocalDate apertura, double importe) {
        super(id, apertura);
        this.importe = importe;
    }

    @Override
    public int calcularPlazoResolucion() { return 20; }
}
```

`Expediente` es una **clase abstracta**: fija el contrato común (`calcularPlazoResolucion()`) y delega en cada subclase la regla concreta. Este ejemplo se retoma en las secciones 2 y 4 para ilustrar herencia, polimorfismo y patrones de diseño.

---

## 1. Fundamentos de la programación orientada a objetos

### 1.1. Evolución de la ingeniería del software hacia el paradigma OO

La historia de los paradigmas de programación es, en gran parte, la historia de la búsqueda de una unidad de organización del código que **escale** con la complejidad del software. La **programación no estructurada** (años 50-60), basada en saltos incondicionales (`GOTO`), dio paso con el teorema de Böhm-Jacopini a la **programación estructurada**: secuencia, selección e iteración como únicos mecanismos de control de flujo (ver Tema 18, §4.1). La estructurada organiza el programa en **procedimientos y funciones** que operan sobre datos externos a ellos, lo que en sistemas grandes provoca un problema recurrente: los datos compartidos por muchos procedimientos son difíciles de proteger de modificaciones incoherentes, y un cambio en la estructura de un dato obliga a revisar todo el código que lo toca.

La **programación orientada a objetos** (POO) responde a este problema invirtiendo la relación entre datos y funciones: en lugar de procedimientos que operan sobre datos externos, se definen **objetos** que **encapsulan** sus propios datos (estado) junto con las operaciones que los manipulan (comportamiento) [BOOCH07, cap. 1]. Sus raíces se remontan a **Simula 67** (Dahl y Nygaard, 1967), primer lenguaje en introducir clases y objetos para la simulación de sistemas, y se consolida con **Smalltalk** (Xerox PARC, años 70), que populariza el término «orientado a objetos» y el envío de mensajes como mecanismo de interacción. **C++** (Stroustrup, 1983) lleva la POO a la corriente principal añadiéndola sobre C; **Java** (Sun Microsystems, 1995) simplifica el modelo (sin herencia múltiple de clases, con recolección automática de memoria) y lo convierte en el paradigma dominante de la programación empresarial [GOSLING-JLS].

> **[DATO CLAVE EXAMEN]** Orden histórico a memorizar: no estructurada → estructurada (Böhm-Jacopini, procedimientos/funciones) → modular → **orientada a objetos** (Simula 67 → Smalltalk → C++ → Java). La POO no sustituye a la estructurada: la incorpora dentro de los métodos de cada clase.

### 1.2. Pilares fundamentales de la POO: abstracción y encapsulamiento

La literatura clásica [BOOCH07; MEYER97] identifica **cuatro pilares** que definen si un lenguaje o un diseño es verdaderamente orientado a objetos: **abstracción**, **encapsulamiento**, **herencia** y **polimorfismo**. Los dos primeros se tratan en este epígrafe; herencia y polimorfismo, en la sección 2.

La **abstracción** consiste en identificar las características esenciales de una entidad del dominio del problema, ignorando los detalles irrelevantes para el contexto de uso. Una clase `Expediente` abstrae de un expediente real solo lo que el sistema necesita conocer (identificador, estado, fecha), no el papel físico ni el color de la carpeta. La abstracción se materializa en la **interfaz pública** de la clase: el conjunto de operaciones que un objeto ofrece al resto del sistema, sin revelar cómo las implementa [MEYER97, cap. 2].

El **encapsulamiento** (o encapsulación) es el mecanismo que **oculta** el estado interno de un objeto y **restringe** el acceso a él a través de una interfaz controlada (los métodos públicos). Su justificación no es solo de seguridad, sino sobre todo de **mantenibilidad**: si el estado interno solo puede modificarse a través de métodos, el objeto puede garantizar sus **invariantes** (p. ej., que `estado` nunca tome un valor distinto de `"ABIERTO"`, `"EN_TRAMITE"`, `"RESUELTO"` o `"CERRADO"`) y el código que usa la clase puede cambiar de implementación interna sin romper a sus clientes, siempre que la interfaz pública se mantenga [MEYER97, cap. 3]. En el ejemplo de la sección de Convenciones, `idExpediente` y `estado` son `private`; solo se exponen a través de `getEstado()` y de un `setEstado()` protegido que solo las subclases pueden invocar.

> **[DATO CLAVE EXAMEN]** Abstracción responde a **QUÉ** hace un objeto (su interfaz); encapsulamiento responde a **CÓMO** protege su estado (oculta la implementación). Son complementarios, no sinónimos.

### 1.3. Modularidad y cohesión

La **modularidad** es la propiedad de un sistema de estar dividido en unidades (módulos, en OO: clases y paquetes) que pueden diseñarse, compilarse y probarse con relativa independencia [SOMMERVILLE16, cap. 6]. En POO, cada clase es, idealmente, un módulo con una responsabilidad delimitada. La calidad de esa división se mide con dos conceptos complementarios que provienen de la ingeniería del software estructurada (Stevens, Myers y Constantine, años 70) y que se aplican íntegramente al diseño OO:

- **Cohesión**: grado en que los elementos internos de un módulo (los atributos y métodos de una clase) están relacionados entre sí y contribuyen a una única responsabilidad. Una clase con **alta cohesión** hace una sola cosa bien; una clase con baja cohesión —que mezcla, por ejemplo, la lógica de negocio de un expediente con la generación de un PDF y el envío de correos— es difícil de entender, probar y reutilizar.
- **Acoplamiento**: grado de dependencia entre módulos distintos (se desarrolla en profundidad en §2.8, tras presentar herencia y composición, que son sus dos formas principales en OO).

> **[DATO CLAVE EXAMEN]** El objetivo de diseño es **alta cohesión + bajo acoplamiento**: clases centradas en una responsabilidad, con el mínimo de dependencias necesarias entre ellas.

### 1.4. Principios SOLID de diseño de software

**SOLID** es el acrónimo, propuesto por Robert C. Martin a partir de sus artículos de 2000 [MARTIN00] y sistematizado en 2003 [MARTIN03], de cinco principios de diseño orientado a objetos que persiguen sistemas mantenibles y extensibles:

- **S — Single Responsibility Principle** (principio de responsabilidad única): una clase debe tener **una, y solo una, razón para cambiar**. Si `ExpedienteLicencia` calculase también el importe de la tasa asociada, tendría dos razones de cambio (reglas de tramitación y reglas fiscales) y debería dividirse.
- **O — Open/Closed Principle** (principio abierto/cerrado): las entidades deben estar **abiertas a extensión** pero **cerradas a modificación**. Añadir un nuevo tipo de expediente (`ExpedienteSubvencion`) no debería obligar a modificar el código que ya trata con `Expediente`; basta con crear una nueva subclase.
- **L — Liskov Substitution Principle** (principio de sustitución de Liskov): un objeto de una subclase debe poder **sustituir** a un objeto de su superclase sin alterar la corrección del programa [LISKOV94]. Si `ExpedienteTributario.calcularPlazoResolucion()` devolviese un valor negativo o lanzase una excepción no esperada por el código que trata genéricamente con `Expediente`, se violaría LSP.
- **I — Interface Segregation Principle** (principio de segregación de interfaces): es preferible tener **varias interfaces específicas** de cliente antes que una interfaz general y sobrecargada que obligue a implementar métodos irrelevantes.
- **D — Dependency Inversion Principle** (principio de inversión de dependencias): los módulos de alto nivel no deben depender de módulos de bajo nivel; **ambos deben depender de abstracciones** (interfaces), no de implementaciones concretas.

> **[EJEMPLO AYTO MADRID]** Un servicio `NotificadorExpedientes` que dependiera directamente de una clase concreta `EnvioCorreoSMTP` violaría DIP. Si en su lugar depende de una interfaz `CanalNotificacion` (implementada por `EnvioCorreoSMTP`, `EnvioSMS` o `EnvioSedeElectronica`), el Ayuntamiento puede añadir un nuevo canal —por ejemplo, notificación push en la app municipal— sin tocar el servicio existente. Este patrón se retoma en §4.5 (patrón Strategy).

> **[REFERENCIA CRUZADA]** SOLID es un desarrollo de los principios de **modularidad, cohesión y acoplamiento** de la ingeniería del software clásica (Tema 16, modelo conceptual de datos; Tema 25, seguridad en el desarrollo) aplicados específicamente al diseño OO.

---

## 2. Elementos y componentes software

### 2.1. Clases y objetos; ciclo de vida

Una **clase** es la plantilla o molde que define la **estructura** (atributos) y el **comportamiento** (métodos) comunes a un conjunto de entidades. Un **objeto** es una **instancia** concreta de una clase: existe en memoria, tiene un estado propio (los valores particulares de sus atributos) y una identidad que lo distingue de cualquier otro objeto, aunque tenga el mismo estado [BOOCH07, cap. 2]. La relación es la misma que hay entre un plano arquitectónico (la clase) y cada edificio construido con ese plano (los objetos): `ExpedienteLicencia` es la clase; cada expediente real tramitado en el registro es un objeto.

El **ciclo de vida de un objeto** en un lenguaje con recolección automática de memoria como Java consta de las siguientes fases:

1. **Declaración**: se reserva un nombre de variable de un tipo de referencia (`Expediente exp;`), sin que exista todavía objeto alguno.
2. **Instanciación**: el operador `new` reserva memoria en el **montículo** (*heap*) y devuelve una referencia (`exp = new ExpedienteLicencia("EXP-2026-001", LocalDate.now(), "OBRA_MAYOR");`).
3. **Construcción**: se ejecuta el **constructor**, que inicializa el estado del objeto (ver §2.2).
4. **Uso**: el objeto recibe **mensajes** (invocaciones a sus métodos) durante su vida útil.
5. **Destrucción o recolección**: en Java, cuando ya no existe ninguna referencia alcanzable al objeto, el **recolector de basura** (*garbage collector*) libera su memoria automáticamente; en lenguajes sin recolección automática (C++), la destrucción es responsabilidad explícita del programador (`delete`).

> **[DATO CLAVE EXAMEN]** Una **clase** no ocupa memoria de datos en tiempo de ejecución (es una definición); un **objeto**, sí. Dos objetos de la misma clase con idéntico estado son, aun así, entidades distintas (identidad ≠ igualdad de estado).

### 2.2. Atributos, variables, métodos y constructores

Los **atributos** (también llamados campos o propiedades) son las variables que almacenan el estado de un objeto; pueden ser **de instancia** (cada objeto tiene su propia copia, como `idExpediente`) o **de clase** (`static` en Java: una única copia compartida por todos los objetos de la clase, útil por ejemplo para un contador de expedientes abiertos). Los **métodos** son las operaciones que definen el comportamiento; también pueden ser de instancia o **estáticos**, si no dependen del estado de un objeto concreto.

El **constructor** es un método especial, con el mismo nombre que la clase y sin tipo de retorno, invocado automáticamente al crear un objeto con `new`, cuya responsabilidad es dejar el objeto en un **estado inicial válido**. Una clase puede tener **varios constructores sobrecargados** (misma clase, distinta lista de parámetros; ver §2.5) para admitir distintas formas de inicialización. Si una subclase no invoca explícitamente un constructor de su superclase con `super(...)`, Java invoca implícitamente el constructor sin argumentos de la superclase —y si este no existe, se produce un error de compilación—, lo que obliga a razonar con cuidado el orden de inicialización en una jerarquía.

> **[EJERCICIO RESUELTO]** Añadir a `Expediente` un atributo de clase que cuente los expedientes abiertos:
> ```java
> public abstract class Expediente {
>     private static int totalAbiertos = 0;
>     // ... atributos de instancia ...
>     public Expediente(String id, LocalDate apertura) {
>         this.idExpediente = id;
>         this.fechaApertura = apertura;
>         this.estado = "ABIERTO";
>         totalAbiertos++;               // variable de clase: compartida
>     }
>     public static int getTotalAbiertos() { return totalAbiertos; }
> }
> ```
> `totalAbiertos` existe **una sola vez**, independientemente de cuántos objetos `Expediente` se creen; se accede sin instancia, con `Expediente.getTotalAbiertos()`.

### 2.3. Visibilidad y control de acceso

Los **modificadores de acceso** controlan qué otras clases pueden ver y usar un atributo, método o constructor, y son el mecanismo técnico que **implementa** el encapsulamiento (§1.2). Java define cuatro niveles:

| Modificador | Misma clase | Mismo paquete | Subclase (otro paquete) | Cualquier clase |
|---|---|---|---|---|
| `private` | Sí | No | No | No |
| *(sin modificador, package-private)* | Sí | Sí | No | No |
| `protected` | Sí | Sí | Sí | No |
| `public` | Sí | Sí | Sí | Sí |

La **regla de diseño general** es exponer el mínimo nivel de visibilidad necesario: atributos casi siempre `private` (accesibles solo mediante métodos `get`/`set` que pueden validar o transformar el valor), métodos de utilidad interna `private`, métodos pensados para que las subclases los reutilicen o sobrescriban `protected`, y solo la interfaz realmente destinada a otros módulos, `public`. Esta disciplina —conocida como **minimizar la visibilidad**— reduce el acoplamiento y facilita refactorizar la implementación interna sin romper el código cliente.

> **[REFERENCIA CRUZADA]** La visibilidad `protected`/`public` en Java determina qué operaciones aparecen en la **interfaz** de una clase representada en un diagrama de clases UML (§5.3), donde se anotan con los símbolos `-` (private), `#` (protected), `~` (package) y `+` (public).

### 2.4. Mecanismos avanzados en POO: herencia simple y múltiple

La **herencia** es el mecanismo por el cual una clase (**subclase** o clase derivada) adquiere los atributos y métodos de otra clase (**superclase** o clase base), pudiendo añadir nuevos miembros o **redefinir** el comportamiento heredado. Modela relaciones **«es un»** (*is-a*): `ExpedienteLicencia` **es un** `Expediente`. En el ejemplo de Convenciones, `extends` establece la herencia; el constructor de la subclase invoca con `super(...)` al de la superclase para inicializar la parte heredada del estado.

Se distingue:

- **Herencia simple**: una clase hereda de una única superclase. Es el único modelo que admite Java para clases (`class B extends A`), lo que simplifica notablemente el modelo de memoria y de resolución de nombres.
- **Herencia múltiple**: una clase hereda de **varias** superclases simultáneamente. La admiten C++ o Python, pero introduce el conocido **problema del diamante** (*diamond problem*): si las clases `B` y `C` heredan de `A` y redefinen un mismo método, y una clase `D` hereda de `B` y `C`, ¿qué versión del método hereda `D`? Distintos lenguajes lo resuelven con reglas de precedencia distintas (C++ exige desambiguar explícitamente; Python usa el *Method Resolution Order*, MRO).

Java evita este problema **prohibiendo la herencia múltiple de clases**, pero permite que una clase implemente **varias interfaces** (`class X implements InterfazA, InterfazB`), lo que aporta polimorfismo múltiple sin el conflicto de estado del diamante, porque una interfaz (hasta Java 8) no aporta estado ni implementación por defecto de sus métodos.

> **[DATO CLAVE EXAMEN]** Java: herencia simple de clases (`extends`, una sola superclase) + implementación múltiple de interfaces (`implements`, varias). El problema del diamante clásico es un riesgo de C++, **no** de Java.

### 2.5. Sobrecarga y sobrescritura de métodos

Son dos mecanismos frecuentemente confundidos en el examen por su nombre parecido en español, pero con semántica y momento de resolución radicalmente distintos [GOSLING-JLS, §8.4]:

- **Sobrecarga** (*overloading*): definir en la **misma clase** varios métodos con el **mismo nombre** pero **distinta firma** (número, tipo u orden de los parámetros). El compilador decide, en **tiempo de compilación**, qué versión invocar según los tipos de los argumentos de la llamada (**ligadura estática**). No es un mecanismo de POO en sentido estricto —existe también en lenguajes no orientados a objetos que lo soporten— sino de resolución de nombres del lenguaje.
- **Sobrescritura** (*overriding*): redefinir en una **subclase** un método **heredado**, con la **misma firma** que en la superclase, para especializar su comportamiento. La versión que se ejecuta se decide en **tiempo de ejecución**, según la clase real del objeto (**ligadura dinámica**; se desarrolla en §2.6). En Java se marca (opcionalmente, pero recomendado) con la anotación `@Override`, que hace que el compilador verifique que realmente existe un método de igual firma en la superclase.

```java
public class Expediente {
    public void notificar(String mensaje) { /* canal por defecto */ }
    public void notificar(String mensaje, String canal) { /* SOBRECARGA: firma distinta */ }
}

public class ExpedienteLicencia extends Expediente {
    @Override
    public int calcularPlazoResolucion() { /* SOBRESCRITURA: misma firma que en Expediente */
        return 30;
    }
}
```

> **[DATO CLAVE EXAMEN]** Sobrecarga = mismo nombre, **distinta** firma, **misma** clase, ligadura **estática** (compilación). Sobrescritura = **misma** firma, **distinta** clase (herencia), ligadura **dinámica** (ejecución). Es la pregunta más recurrente de este tema en exámenes TIC.

### 2.6. Polimorfismo y ligadura dinámica

El **polimorfismo** (del griego «muchas formas») es la capacidad de que una misma operación —invocada con la misma sintaxis— se comporte de manera distinta según el objeto real sobre el que se ejecuta [BOOCH07, cap. 2]. Es la consecuencia directa de combinar herencia (§2.4) con sobrescritura (§2.5): una variable declarada del tipo de la superclase puede referenciar en tiempo de ejecución a un objeto de cualquier subclase, y al invocar un método sobrescrito se ejecuta la versión de la clase **real** del objeto, no la del tipo declarado de la variable.

```java
List<Expediente> expedientes = List.of(
    new ExpedienteLicencia("EXP-001", LocalDate.now(), "OBRA_MAYOR"),
    new ExpedienteTributario("EXP-002", LocalDate.now(), 312.40)
);
for (Expediente e : expedientes) {
    // Cada iteración invoca calcularPlazoResolucion() de la clase REAL de "e",
    // aunque el tipo declarado de la variable "e" sea siempre Expediente.
    System.out.println(e.calcularPlazoResolucion());  // 90, luego 20
}
```

Este mecanismo se llama **ligadura dinámica** o **tardía** (*late binding*, *dynamic dispatch*): la decisión de qué código ejecutar se pospone hasta el momento de la llamada, en tiempo de ejecución, frente a la **ligadura estática** (*early binding*) de la sobrecarga, resuelta en compilación. En la máquina virtual de Java se implementa mediante una tabla de métodos virtuales asociada a cada clase (mecanismo interno equivalente a la *vtable* de C++), que la JVM consulta para localizar la implementación correspondiente al tipo real del objeto en cada invocación.

> **[EJEMPLO AYTO MADRID]** Un método `generarInformeMensual(List<Expediente> pendientes)` puede recorrer expedientes de licencia y tributarios **indistintamente**, sin necesidad de un `if (exp instanceof ExpedienteLicencia) ... else if (...)` para cada tipo: el polimorfismo delega esa decisión en cada objeto. Esto es precisamente lo que permite cumplir el principio abierto/cerrado (§1.4): añadir `ExpedienteSubvencion` no obliga a tocar `generarInformeMensual`.

> **[REFERENCIA CRUZADA]** El polimorfismo es la base técnica de casi todo el catálogo de patrones de comportamiento (§4.5) y del propio Diagrama de Clases UML, donde una relación de herencia con un método abstracto anuncia visualmente un punto de extensión polimórfico (§5.3).

### 2.7. Jerarquías y reutilización de código

Encadenar relaciones de herencia produce una **jerarquía de clases**: un árbol (en Java, siempre árbol, nunca grafo, por la herencia simple de §2.4) con una superclase raíz —en Java, implícitamente `Object` para toda clase que no declare otra— y subclases cada vez más especializadas. La jerarquía es el mecanismo de **reutilización de código por herencia**: el código común se escribe una sola vez en la superclase (`Expediente.getEstado()`, el constructor que fija `estado = "ABIERTO"`) y todas las subclases lo reciben sin duplicarlo.

Existe, sin embargo, una alternativa a la herencia para reutilizar código: la **composición**, en la que una clase incluye como atributo una **instancia** de otra clase y delega en ella parte de su comportamiento, en lugar de heredar de ella. GoF formula el principio de diseño **«favorece la composición sobre la herencia»** [GOF94, cap. 1]: la herencia crea un acoplamiento muy fuerte entre subclase y superclase (un cambio en la superclase puede romper subclases, el llamado **problema de la clase base frágil**, *fragile base class*), mientras que la composición permite combinar comportamientos en tiempo de ejecución y cambiar la implementación delegada sin alterar la jerarquía. Este principio no descarta la herencia —sigue siendo el mecanismo natural para relaciones «es un» estables y poco cambiantes— pero advierte contra su uso indiscriminado solo para reutilizar código cuando la relación real es «tiene un» (*has-a*).

> **[DATO CLAVE EXAMEN]** Herencia = reutilización por **especialización** («es un»), acoplamiento fuerte, decidido en tiempo de compilación. Composición = reutilización por **delegación** («tiene un»), acoplamiento débil, se puede reconfigurar en tiempo de ejecución. GoF recomienda composición como opción por defecto.

### 2.8. Relaciones de acoplamiento

El **acoplamiento** (introducido en §1.3) mide el grado de interdependencia entre clases. En diseño OO se distinguen, de mayor a menor grado de acoplamiento (y por tanto de peor a mejor, salvo cuando la semántica del dominio exige el más fuerte):

1. **Herencia** (`extends`): la subclase depende de los detalles de implementación de la superclase, incluidos los que no forman parte de su interfaz pública si son `protected`. Es el acoplamiento más fuerte entre dos clases.
2. **Composición**: el objeto contenedor gestiona el **ciclo de vida** del objeto contenido (si se destruye el contenedor, se destruye lo contenido). Relación «todo-parte» fuerte.
3. **Agregación**: el objeto contenedor **referencia** a otro objeto que existe con independencia de él (mismo ciclo de vida separado). Relación «todo-parte» débil.
4. **Asociación**: dos clases se conocen y colaboran (un atributo de una clase es una referencia a otra), sin relación de contención.
5. **Dependencia**: el acoplamiento más débil; una clase usa a otra solo puntualmente (p. ej. como tipo de un parámetro o variable local de un método), sin mantener una referencia permanente.

> **[EJEMPLO AYTO MADRID]** `Expediente` tiene una **composición** con sus `DocumentoAdjunto` (si se elimina el expediente, se eliminan sus documentos); una **agregación** con el `Funcionario` tramitador (el funcionario existe independientemente del expediente y puede tramitar otros); y una **dependencia** puntual con `GeneradorPDF` si solo lo usa como parámetro de un método `exportar(GeneradorPDF gen)`, sin guardar una referencia a él como atributo.

Estas cinco relaciones se representan gráficamente en el Diagrama de Clases UML con notaciones distintas (§5.3): la herencia con una flecha de punta triangular hueca, la composición con un rombo relleno, la agregación con un rombo hueco, y la asociación/dependencia con líneas continuas o discontinuas.

> **[REFERENCIA CRUZADA]** El acoplamiento entre módulos software es también un factor de riesgo de seguridad y de propagación de errores tratado desde la óptica de la arquitectura cliente-servidor y de servicios web en el Tema 22.

---

## 3. Ventajas e inconvenientes del paradigma OO

### 3.1. Beneficios en el ciclo de vida del software: reutilizabilidad y mantenibilidad

La justificación última de la POO no es estética, sino económica: reducir el **coste total** del software a lo largo de su ciclo de vida, donde el mantenimiento —no el desarrollo inicial— representa históricamente la mayor parte del gasto [PRESSMAN14, cap. 20]. Sus beneficios principales:

- **Reutilizabilidad**: clases bien diseñadas (con alta cohesión y bajo acoplamiento) pueden emplearse en distintos proyectos o partes de un sistema sin modificación, especialmente cuando se organizan en bibliotecas o *frameworks*.
- **Mantenibilidad**: el encapsulamiento limita el impacto de un cambio a la clase afectada, siempre que su interfaz pública no varíe; la localización de un fallo se facilita porque el estado y el comportamiento relacionado están en el mismo lugar (la clase), no dispersos.
- **Correspondencia con el dominio**: las clases suelen modelar directamente entidades del mundo real del problema (`Expediente`, `Ciudadano`, `Tributo`), lo que facilita la comunicación entre el equipo técnico y los expertos del dominio (funcionarios, analistas de negocio) y reduce la distancia conceptual entre el modelo y el sistema.

### 3.2. Escalabilidad y aislamiento de errores

- **Escalabilidad del equipo**: al dividir el sistema en clases con responsabilidades delimitadas, distintos desarrolladores pueden trabajar en paralelo sobre clases diferentes con interferencia mínima, siempre que las interfaces estén bien definidas.
- **Aislamiento de errores**: un fallo en la implementación interna de una clase, si no altera el cumplimiento de su interfaz pública ni sus invariantes, queda contenido dentro de esa clase y no se propaga en cascada al resto del sistema, lo que facilita las pruebas unitarias por clase.
- **Extensibilidad controlada**: gracias al polimorfismo (§2.6) y al principio abierto/cerrado (§1.4), el sistema puede crecer añadiendo nuevas clases sin reescribir las existentes, lo que reduce el riesgo de introducir regresiones al añadir funcionalidad.

> **[DATO CLAVE EXAMEN]** Las cuatro ventajas más citadas del paradigma OO en exámenes TIC: **reutilización, mantenibilidad, escalabilidad y aislamiento de errores** — todas ellas consecuencia directa del encapsulamiento y la modularidad, no propiedades independientes.

### 3.3. Limitaciones, costes y penalizaciones técnicas: curva de aprendizaje y complejidad de diseño

La POO no es gratuita. Su primer coste es formativo: dominar simultáneamente abstracción, encapsulamiento, herencia, polimorfismo y los principios de diseño asociados exige una **curva de aprendizaje** notablemente más larga que la de la programación estructurada básica, y errores conceptuales tempranos (jerarquías de herencia mal planteadas, clases con responsabilidades mezcladas) suelen arrastrarse y ser costosos de corregir más adelante.

Además, **diseñar bien** en OO —decidir qué es una clase, dónde trazar los límites de responsabilidad, cuándo usar herencia frente a composición, qué patrón aplicar— requiere experiencia y no tiene una respuesta mecánica; un mal diseño inicial puede resultar **más rígido** de modificar que el equivalente estructurado, precisamente por el acoplamiento fuerte que introduce una jerarquía de herencia extensa y profunda (§2.8).

### 3.4. Sobrecarga en tiempo de ejecución

Existe también un coste en **rendimiento** frente a código puramente procedimental equivalente:

- La **ligadura dinámica** (§2.6) exige, en cada invocación de un método sobrescribible, una consulta indirecta a la tabla de métodos de la clase real del objeto, más costosa que una llamada directa resuelta en compilación.
- Cada objeto conlleva **memoria adicional** de gestión (metadatos de tipo, referencia a la tabla de métodos), sobre la memoria estrictamente necesaria para sus atributos.
- En lenguajes con recolección automática de memoria como Java, la creación y destrucción frecuente de muchos objetos de vida corta incrementa la presión sobre el **recolector de basura**, lo que puede introducir pausas apreciables en sistemas de alto rendimiento o tiempo real.

> **[DATO CLAVE EXAMEN]** El coste en rendimiento de la POO frente a la programación estructurada equivalente proviene, sobre todo, de la **ligadura dinámica** (indirección en cada llamada polimórfica) y de la **gestión de memoria por objeto**, no del hecho de «usar clases» en sí mismo.

### 3.5. Riesgos de un mal diseño orientado a objetos

Un diseño OO deficiente introduce anti-patrones bien documentados (desarrollados en detalle en §4.2): jerarquías de herencia profundas y rígidas que dificultan cualquier cambio (**herencia frágil**), clases enormes que acumulan demasiadas responsabilidades (**God Object**, contrario al SRP), o cadenas de dependencias entre objetos que ocultan el flujo real de control y dificultan las pruebas. La disciplina de diseño (SOLID, patrones, revisión de acoplamiento) no es opcional en sistemas OO de tamaño medio o grande: es la que evita que las ventajas teóricas del paradigma (§3.1-3.2) se conviertan, en la práctica, en un sistema más difícil de mantener que uno estructurado bien escrito.

> **[REFERENCIA CRUZADA]** Los riesgos de un diseño OO deficiente en cuanto a seguridad y confidencialidad del dato manejado en cada clase se desarrollan en el Tema 25 (accesibilidad, usabilidad y conceptos de seguridad en el desarrollo).

---

## 4. Patrones de diseño

### 4.1. Concepto y catálogo (Gang of Four)

Un **patrón de diseño** es una solución **general y reutilizable** a un problema que se presenta habitualmente en el diseño de software orientado a objetos: no es código listo para copiar, sino una **plantilla conceptual** —con nombre propio, problema que resuelve, solución estructural en términos de clases y objetos, y consecuencias de aplicarla— que puede adaptarse a cada situación concreta [GOF94, cap. 1].

El catálogo de referencia es el de **Gamma, Helm, Johnson y Vlissides** (1994), conocidos colectivamente como **Gang of Four** (GoF), que sistematizó **23 patrones** observados de forma recurrente en sistemas OO bien diseñados, agrupados en tres familias según el problema que abordan (desarrolladas en §4.3-4.5): **creacionales** (cómo se crean los objetos), **estructurales** (cómo se componen clases y objetos en estructuras mayores) y **de comportamiento** (cómo colaboran e intercambian responsabilidades los objetos).

Cada patrón GoF documenta, además del nombre, la **intención** (qué problema resuelve), la **aplicabilidad** (cuándo usarlo), la **estructura** (típicamente, un mini diagrama de clases UML) y las **consecuencias** (ventajas e inconvenientes de aplicarlo), lo que da a los equipos de desarrollo un **vocabulario común**: nombrar «vamos a aplicar un Factory Method aquí» comunica en una frase una solución completa que, de otro modo, requeriría explicar en detalle.

> **[DATO CLAVE EXAMEN]** GoF = 23 patrones = **5 creacionales + 7 estructurales + 11 de comportamiento**. Es la cifra más preguntada de esta sección; conviene memorizar la distribución, no solo el total.

### 4.2. Patrón, anti-patrón y criterios de aplicabilidad arquitectónica

Frente al **patrón** (solución probada y recomendable) se define el **anti-patrón**: una solución que, aunque frecuente en la práctica, es **contraproducente** a medio o largo plazo y suele surgir de aplicar un patrón fuera de contexto, o de no aplicar ninguno donde hacía falta. Los anti-patrones OO más citados:

- **God Object** (objeto todopoderoso): una clase que acumula demasiadas responsabilidades y conoce/controla la mayor parte del sistema, violando el SRP (§1.4) y concentrando un acoplamiento extremo.
- **Spaghetti Code** orientado a objetos: uso de clases y objetos sin una estructura de colaboración clara, con dependencias circulares y flujo de control difícil de seguir pese a la apariencia «orientada a objetos» del código.
- **Golden Hammer** (martillo de oro): aplicar sistemáticamente un mismo patrón conocido a cualquier problema, aunque no encaje, por familiaridad del equipo con él.
- **Herencia por conveniencia**: usar `extends` únicamente para reutilizar código de una clase con la que no existe una relación «es un» real, generando jerarquías semánticamente falsas (§2.7).

Un **criterio de aplicabilidad arquitectónica** correcto exige, antes de introducir un patrón: (1) identificar el problema concreto de diseño (¿variabilidad en la creación? ¿necesidad de desacoplar una jerarquía de una funcionalidad transversal? ¿múltiples algoritmos intercambiables?); (2) verificar que el patrón candidato resuelve exactamente ese problema, consultando su sección de aplicabilidad en el catálogo; y (3) valorar el coste de la indirección adicional que casi todo patrón introduce frente al beneficio de flexibilidad, evitando aplicar patrones de forma preventiva sin necesidad real (sobre-ingeniería).

> **[REFERENCIA CRUZADA]** La distinción patrón/anti-patrón se aplica igualmente al diseño de bases de datos (Tema 17, normalización frente a desnormalización mal justificada) y a la arquitectura de sistemas cliente-servidor y de servicios web (Tema 22).

### 4.3. Clasificación técnica: patrones creacionales

Los **patrones creacionales** abstraen y flexibilizan el **proceso de instanciación** de objetos, desacoplando al código cliente de las clases concretas que finalmente se crean. Los cinco del catálogo GoF:

| Patrón | Intención |
|---|---|
| **Singleton** | Garantiza que una clase tenga una única instancia global y proporciona un punto de acceso a ella (p. ej. un `GestorConfiguracionAyuntamiento` con la configuración cargada una sola vez). |
| **Factory Method** | Define una interfaz para crear un objeto, dejando que las subclases decidan qué clase concreta instanciar. |
| **Abstract Factory** | Proporciona una interfaz para crear **familias** de objetos relacionados sin especificar sus clases concretas. |
| **Builder** | Separa la construcción de un objeto complejo (con muchos parámetros opcionales) de su representación final, permitiendo construirlo paso a paso. |
| **Prototype** | Crea nuevos objetos **clonando** un objeto prototipo existente, en lugar de instanciar desde cero. |

> **[EJERCICIO RESUELTO]** Aplicar **Factory Method** a la jerarquía `Expediente`: en lugar de que el código cliente escriba `new ExpedienteLicencia(...)` o `new ExpedienteTributario(...)` directamente (lo que le acopla a las clases concretas), se delega la creación en una fábrica:
> ```java
> public class ExpedienteFactory {
>     public static Expediente crear(String tipo, String id, LocalDate apertura, Object datoExtra) {
>         return switch (tipo) {
>             case "LICENCIA"   -> new ExpedienteLicencia(id, apertura, (String) datoExtra);
>             case "TRIBUTARIO" -> new ExpedienteTributario(id, apertura, (Double) datoExtra);
>             default -> throw new IllegalArgumentException("Tipo no soportado: " + tipo);
>         };
>     }
> }
> ```
> Si el Ayuntamiento añade `ExpedienteSubvencion`, solo se modifica `ExpedienteFactory`; el código cliente que llama a `ExpedienteFactory.crear(...)` no cambia.

### 4.4. Patrones estructurales

Los **patrones estructurales** resuelven cómo componer clases y objetos en estructuras más grandes, manteniendo esas estructuras flexibles y eficientes. Los siete del catálogo GoF:

| Patrón | Intención |
|---|---|
| **Adapter** | Convierte la interfaz de una clase existente en otra interfaz que el cliente espera, permitiendo colaborar a clases incompatibles. |
| **Bridge** | Desacopla una abstracción de su implementación, de modo que ambas puedan variar independientemente. |
| **Composite** | Compone objetos en estructuras de árbol para representar jerarquías «todo-parte», tratando de manera uniforme objetos individuales y composiciones. |
| **Decorator** | Añade responsabilidades a un objeto dinámicamente, como alternativa flexible a la herencia para extender funcionalidad. |
| **Facade** | Proporciona una interfaz unificada y simplificada a un conjunto de interfaces de un subsistema complejo. |
| **Flyweight** | Comparte eficientemente objetos de grano fino con estado común, para reducir el consumo de memoria. |
| **Proxy** | Proporciona un objeto sustituto (representante) que controla el acceso a otro objeto, p. ej. para carga diferida o control de permisos. |

> **[EJEMPLO AYTO MADRID]** Un `ExpedienteProxy` podría interponerse entre el módulo de tramitación y el `Expediente` real, comprobando —antes de reenviar cada llamada— que el funcionario autenticado tiene permiso sobre ese distrito, sin modificar la clase `Expediente` original. Es una aplicación directa del patrón **Proxy** con fines de control de acceso.

### 4.5. Patrones de comportamiento

Los **patrones de comportamiento** se ocupan de cómo se **comunican y reparten responsabilidades** los objetos entre sí, especialmente cuando existen algoritmos o flujos de control intercambiables. Los once del catálogo GoF:

| Patrón | Intención |
|---|---|
| **Strategy** | Encapsula una familia de algoritmos intercambiables (p. ej. distintos canales de notificación, ver §1.4) tras una interfaz común, seleccionable en tiempo de ejecución. |
| **Observer** | Define una dependencia uno-a-muchos: cuando un objeto (sujeto) cambia de estado, notifica automáticamente a todos sus observadores registrados. |
| **Command** | Encapsula una petición como un objeto, permitiendo parametrizar, encolar o deshacer operaciones. |
| **State** | Permite que un objeto altere su comportamiento cuando cambia su estado interno, como si cambiase de clase. |
| **Template Method** | Define el esqueleto de un algoritmo en la superclase, delegando pasos concretos a las subclases (aplicado ya, de facto, en `calcularPlazoResolucion()` de `Expediente`). |
| **Chain of Responsibility** | Encadena objetos receptores de una petición, hasta que uno de ellos la procesa. |
| **Iterator** | Proporciona acceso secuencial a los elementos de una colección sin exponer su representación interna. |
| **Mediator** | Centraliza la comunicación compleja entre un conjunto de objetos en un único objeto mediador. |
| **Memento** | Captura y externaliza el estado interno de un objeto para poder restaurarlo después, sin violar su encapsulamiento. |
| **Visitor** | Separa un algoritmo de la estructura de objetos sobre la que opera, permitiendo añadir operaciones nuevas sin modificar las clases visitadas. |
| **Interpreter** | Define una representación gramatical de un lenguaje y un intérprete para evaluar sentencias de ese lenguaje. |

> **[EJEMPLO AYTO MADRID]** Aplicar **Observer** para que, cuando un `Expediente` cambie de estado (`EN_TRAMITE → RESUELTO`), se notifique automáticamente al ciudadano (por el canal que prefiera, resuelto a su vez con **Strategy**) y se actualice un panel de indicadores del Área de Gobierno correspondiente, sin que la clase `Expediente` conozca los detalles de cada suscriptor.

> **[REFERENCIA CRUZADA]** El patrón Observer es, conceptualmente, el mismo problema que resuelven los **disparadores** (*triggers*) en un SGBD relacional (Tema 19, §4): reaccionar automáticamente a un cambio de estado sin acoplar la lógica de reacción al código que provoca el cambio.

---

## 5. Modelado de sistemas con UML (Unified Modeling Language)

### 5.1. Fundamentos y especificación del estándar OMG: origen y evolución

**UML** (*Unified Modeling Language*) es el lenguaje de modelado gráfico estándar para especificar, visualizar, construir y documentar los artefactos de un sistema de software orientado a objetos [OMG-UML25]. Nace de la unificación, a mediados de los años 90, de tres notaciones de modelado OO previas y competidoras: el **método Booch**, la **OMT** (*Object Modeling Technique*) de Rumbaugh y el **OOSE** (*Object-Oriented Software Engineering*) de Jacobson, cuyos autores —conocidos como «los tres amigos»— unieron sus notaciones en Rational Software a partir de 1994 [RUMBAUGH05, prefacio]. El estándar se entregó al **Object Management Group** (OMG), consorcio que lo adopta como estándar en 1997 y mantiene desde entonces sus sucesivas versiones: UML 1.x (1997-2003), **UML 2.0** (2005, revisión mayor que introduce, entre otros, el diagrama de estructura compuesta y reformula el de actividades) y la versión vigente **UML 2.5.1** (2017) [OMG-UML25].

Es importante distinguir UML de un **método de desarrollo**: UML es **solo una notación** —un lenguaje gráfico— y no prescribe un proceso de desarrollo concreto (a diferencia, p. ej., del Proceso Unificado, con el que históricamente se ha combinado). Puede usarse en metodologías predictivas o ágiles, de forma más o menos exhaustiva, según las necesidades del proyecto.

> **[DATO CLAVE EXAMEN]** UML nace de la unión de tres notaciones (Booch + OMT de Rumbaugh + OOSE de Jacobson), estandarizada por **OMG**. UML es una **notación**, no una metodología de desarrollo.

### 5.2. Bloques de construcción y mecanismos comunes

La especificación UML define tres categorías de **bloques de construcción** [OMG-UML25, §7]:

- **Elementos** (*things*): las abstracciones de primera clase del modelo — estructurales (clase, interfaz, componente, nodo), de comportamiento (interacción, máquina de estados), de agrupación (paquete) y de anotación (nota).
- **Relaciones**: los mecanismos que conectan elementos entre sí — dependencia, asociación, generalización (herencia) y realización (implementación de una interfaz).
- **Diagramas**: representaciones gráficas de un conjunto de elementos y relaciones, cada uno centrado en un aspecto del sistema (desarrollados en §5.3-5.7).

Además, UML define **mecanismos comunes** aplicables a cualquier diagrama: las **especificaciones** (semántica textual detrás de cada símbolo gráfico), las **adornos** (detalles visuales opcionales, como la multiplicidad de una asociación), las **divisiones comunes** (p. ej. clase/instancia, interfaz/implementación) y los **mecanismos de extensibilidad** — estereotipos (`«interface»`, `«actor»`), valores etiquetados y restricciones (entre llaves, `{restricción}`) — que permiten adaptar la notación estándar a necesidades específicas de un dominio sin crear un lenguaje nuevo.

### 5.3. Diagramas estructurales y estáticos: Diagrama de Clases y Diagrama de Objetos

UML clasifica sus 14 tipos de diagrama en dos grandes familias [UML-DIAG-TYPES]: **estructurales** (7 tipos: qué existe) y **de comportamiento** (7 tipos: qué ocurre). Esta sección desarrolla los dos diagramas estructurales estáticos centrales para el diseño OO.

El **Diagrama de Clases** es el diagrama UML más utilizado en la práctica y, con frecuencia, el único elaborado de forma completa en proyectos pequeños: representa las clases del sistema, sus atributos y métodos, y las relaciones entre ellas. Cada clase se dibuja como un rectángulo con **tres compartimentos**: nombre de la clase (centrado, en negrita), atributos (con su visibilidad `-`/`#`/`~`/`+`, nombre y tipo) y métodos (igual notación de visibilidad, nombre, parámetros y tipo de retorno). Las relaciones entre clases (§2.8) se representan con líneas cuya terminación indica el tipo: flecha triangular hueca para **generalización**/herencia, rombo relleno para **composición**, rombo hueco para **agregación**, línea continua simple para **asociación** (con multiplicidad en los extremos, p. ej. `1..*`) y línea discontinua con flecha abierta para **dependencia** [FOWLER-UML, cap. 5].

El **Diagrama de Objetos** es un «pariente» del de clases que muestra, en cambio, una **instantánea** (*snapshot*) de instancias concretas en un momento dado, con sus valores de atributo reales (`exp001: ExpedienteLicencia`), útil para ilustrar ejemplos concretos de una relación compleja del diagrama de clases o para depurar un estado del sistema difícil de entender en abstracto.

> **[REFERENCIA CRUZADA]** El Diagrama de Clases UML **no sustituye** al modelo Entidad-Relación del Tema 16: ambos son diagramas estructurales estáticos, pero el E/R modela datos persistentes con vistas al diseño de una base de datos relacional (Tema 16-17), mientras que el Diagrama de Clases modela el diseño de software (datos **y comportamiento** juntos, con métodos) con vistas a la implementación orientada a objetos. Un mismo concepto del dominio (`Expediente`) puede aparecer en ambos diagramas con contenido distinto: como entidad con atributos en el E/R, como clase con atributos y métodos en UML.

### 5.4. Diagramas de Arquitectura física

Completan la familia estructural los diagramas centrados en la organización física y de despliegue del sistema, más allá del diseño de clases:

- **Diagrama de Componentes**: muestra la organización del sistema en componentes software (módulos, bibliotecas, servicios) y las interfaces que exponen y consumen entre sí.
- **Diagrama de Despliegue** (*deployment*): representa la **arquitectura física**, es decir, los nodos de hardware (servidores, dispositivos) sobre los que se despliegan los artefactos software y las conexiones de red entre ellos.
- **Diagrama de Paquetes**: agrupa elementos del modelo (típicamente, clases) en paquetes y muestra las dependencias entre paquetes, útil para visualizar la organización modular de un sistema grande.
- **Diagrama de Estructura Compuesta** (introducido en UML 2.0): detalla la estructura interna de una clase o componente complejo, mostrando cómo colaboran sus partes internas.

> **[DATO CLAVE EXAMEN]** Los 7 diagramas **estructurales** de UML 2.5: Clases, Objetos, Componentes, Despliegue, Paquetes, Estructura Compuesta y Perfiles. De ellos, el de **Clases** es el más preguntado y el único de elaboración casi siempre obligada.

### 5.5. Diagramas de comportamiento: modelado de requisitos funcionales (Diagrama de Casos de Uso)

Los **diagramas de comportamiento** modelan cómo interactúan los elementos del sistema entre sí y con sus usuarios, a diferencia de los estructurales, que fijan una fotografía estática del «qué existe».

El **Diagrama de Casos de Uso** es, de los siete diagramas de comportamiento, el orientado a **capturar requisitos funcionales** desde la perspectiva del usuario, no del diseño interno. Sus elementos son los **actores** (roles externos que interactúan con el sistema, representados con una figura de palotes: un ciudadano, un funcionario tramitador, un sistema externo) y los **casos de uso** (elipses con el nombre de una funcionalidad completa que el sistema ofrece al actor, p. ej. «Presentar solicitud de licencia»), conectados por líneas de asociación. Las relaciones entre casos de uso (`«include»` para funcionalidad obligatoria y reutilizada, `«extend»` para funcionalidad opcional que amplía otro caso de uso bajo ciertas condiciones) permiten estructurar requisitos complejos evitando la duplicación.

> **[EJEMPLO AYTO MADRID]** El caso de uso «Presentar solicitud de licencia de obra» (actor: Ciudadano) puede incluir (`«include»`) el caso de uso «Autenticarse en sede electrónica» (paso obligatorio y común a otros muchos casos de uso), y extenderse (`«extend»`) opcionalmente con «Adjuntar plano técnico» solo cuando la licencia solicitada sea de obra mayor.

> **[REFERENCIA CRUZADA]** El Diagrama de Casos de Uso cumple, en el diseño OO orientado a UML, un papel análogo al de los diagramas de flujo de datos (DFD) del análisis estructurado clásico visto en el Tema 16: ambos capturan **requisitos funcionales** de alto nivel antes de entrar en el diseño detallado, pero con notación y enfoque distintos — el DFD describe **flujos de datos** entre procesos y almacenes en un sistema estructurado, mientras que el Caso de Uso describe **interacciones actor-sistema** en un sistema orientado a objetos. No deben confundirse ni tratarse como notaciones intercambiables.

### 5.6. Interacción temporal: Diagramas de Secuencia y de Comunicación/Colaboración

Dentro de los diagramas de comportamiento, los **diagramas de interacción** muestran cómo colaboran varios objetos concretos para completar un escenario, con énfasis en el **intercambio de mensajes**:

- **Diagrama de Secuencia**: organiza a los participantes (objetos o actores) en **líneas de vida verticales**, con el **tiempo avanzando de arriba abajo**; los mensajes entre ellos se dibujan como flechas horizontales entre líneas de vida, en el orden temporal exacto en que se producen. Es el diagrama de interacción más utilizado por su claridad temporal explícita, especialmente útil para documentar un flujo de negocio concreto paso a paso.
- **Diagrama de Comunicación** (llamado **de Colaboración** en UML 1.x): representa la misma información de colaboración entre objetos, pero organizada **espacialmente** en torno a los objetos participantes (como un grafo), con los mensajes numerados secuencialmente sobre las líneas de conexión para indicar el orden, en lugar de mediante la posición vertical.

Ambos diagramas son **semánticamente equivalentes** —UML permite, en herramientas de modelado, derivar automáticamente uno del otro— y difieren solo en el énfasis visual: el de secuencia prioriza el **orden temporal**; el de comunicación, la **topología de colaboración** entre objetos.

> **[EJERCICIO RESUELTO]** Escenario «Ciudadano presenta solicitud de licencia» en Diagrama de Secuencia (descripción textual del intercambio de mensajes, de arriba abajo): `Ciudadano → PortalWeb: enviarSolicitud(datos)` · `PortalWeb → ExpedienteFactory: crear("LICENCIA", ...)` (§4.3) · `ExpedienteFactory → ExpedienteLicencia: new` (mensaje de creación) · `PortalWeb → ExpedienteLicencia: calcularPlazoResolucion()` · `ExpedienteLicencia --> PortalWeb: 30` (mensaje de retorno, flecha discontinua) · `PortalWeb --> Ciudadano: confirmación con plazo`.

### 5.7. Control de flujo y estados: Diagramas de Máquina de Estados y de Actividades

Cierran la familia de comportamiento los diagramas centrados en el **control interno**, más que en la colaboración entre objetos:

- **Diagrama de Máquina de Estados** (*state machine*, heredero del diagrama de estados o *statechart* de Harel): modela los distintos **estados** por los que puede pasar un objeto a lo largo de su vida (en el ejemplo del tema: `ABIERTO`, `EN_TRAMITE`, `RESUELTO`, `CERRADO`) y las **transiciones** entre estados, cada una disparada por un evento y, opcionalmente, condicionada por una guarda (`[condición]`) y acompañada de una acción. Es especialmente útil para objetos cuyo comportamiento depende fuertemente de su estado actual — el propio patrón de comportamiento **State** (§4.5) es, de hecho, la forma de implementar en código lo que este diagrama modela gráficamente.
- **Diagrama de Actividades**: modela el **flujo de control** de un proceso o algoritmo mediante nodos de acción, decisiones (rombos), bifurcaciones y uniones de flujos paralelos (barras de sincronización) y **carriles** (*swimlanes*) que asignan cada actividad a un actor o componente responsable. Es el diagrama UML más parecido, en apariencia, a un diagrama de flujo clásico, pero añade semántica de concurrencia y de responsabilidad por carril que el diagrama de flujo tradicional no tiene.

> **[DATO CLAVE EXAMEN]** Los 7 diagramas de **comportamiento** de UML 2.5: Casos de Uso, Secuencia, Comunicación, Máquina de Estados, Actividades, Interacción General y Temporización (*Timing*). De ellos, Casos de Uso (requisitos), Secuencia (interacción temporal) y Máquina de Estados (ciclo de vida de un objeto) son los tres más preguntados.

> **[REFERENCIA CRUZADA]** El Diagrama de Máquina de Estados formaliza, con notación UML, el mismo concepto de «estados y transiciones» que aparece en el ciclo de vida de un expediente administrativo (Tema 7, procedimiento LPACAP) o en la clasificación de disparadores por cambio de estado (Tema 19, §4.2): distintas disciplinas, mismo patrón conceptual subyacente.

---

## 6. Tendencias actuales en el diseño orientado a objetos

> **Material complementario.** El enunciado oficial de este tema no nombra este apartado. Se mantiene porque esta materia envejece deprisa y conviene conocer su estado actual, pero lo exigible es lo que enumera el título del tema.

El paradigma OO, treinta años después de su consolidación con Java, convive hoy con corrientes que lo complementan o lo cuestionan parcialmente, sin sustituirlo. La **programación funcional** (inmutabilidad, funciones puras, funciones de orden superior) ha influido notablemente en los lenguajes OO modernos: Java incorpora desde la versión 8 expresiones lambda e interfaces funcionales, que en muchos casos ofrecen una alternativa más ligera que un patrón de comportamiento clásico (una lambda sustituye, a menudo, a una implementación completa del patrón Strategy) sin abandonar el modelo de clases y objetos subyacente. Los lenguajes contemporáneos más influyentes (Kotlin, Scala, incluso el propio Java reciente) son, en este sentido, **híbridos multiparadigma**, no puramente OO en el sentido clásico de Smalltalk.

En arquitectura de sistemas, el auge de los **microservicios** y del **diseño dirigido por el dominio** (*Domain-Driven Design*, DDD) ha reforzado, más que sustituido, los fundamentos de este tema: DDD extiende explícitamente conceptos de modelado OO —entidades con identidad, objetos de valor inmutables, agregados como unidad de consistencia transaccional— al diseño de servicios distribuidos, y sitúa el **Diagrama de Clases** y el vocabulario compartido con el negocio (el «lenguaje ubicuo») como herramientas de primer nivel también en arquitecturas modernas basadas en contenedores y APIs.

En el propio catálogo de patrones, la práctica ha ido depurando cuáles siguen siendo imprescindibles y cuáles se han vuelto menos frecuentes al estar ya resueltos por el propio lenguaje o el *framework*: la inyección de dependencias (una forma sistematizada del principio DIP, §1.4, y del patrón Factory) se ha convertido en un mecanismo de plataforma en los grandes *frameworks* empresariales Java (desarrollado en el Tema 21), reduciendo la necesidad de implementar manualmente Factory Method o Abstract Factory en cada proyecto. En el modelado, las herramientas actuales tienden hacia el **modelado ejecutable** y la **generación de código** a partir de diagramas de clases UML (ida y vuelta entre modelo y código, *round-trip engineering*), y hacia notaciones ligeras derivadas de UML —como los diagramas de clases en formato texto de herramientas como PlantMermaid o Mermaid— integradas directamente en la documentación versionada del código, sin renunciar a la semántica formal que fija el estándar OMG.

> **[REFERENCIA CRUZADA]** Los *frameworks* de inyección de dependencias y los contenedores de componentes que sistematizan varios patrones GoF a nivel de plataforma se desarrollan en el Tema 21 (arquitectura Java EE).
