# Tema 20 — Casos Prácticos

> **Título oficial**: Diseño y programación orientada a objetos. Objetos, clases, herencia, métodos, sobrecarga. Ventajas e inconvenientes. Patrones de diseño y UML.
>
> **Formato**: 3 casos prácticos sobre supuestos reales del Ayuntamiento de Madrid. Cada caso suma **10 puntos**.
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid

Los tres casos recorren el tema sobre la jerarquía `Expediente / ExpedienteLicencia / ExpedienteTributario` (ver tema-20-contenido.md, «Convenciones»), en **Java**: el **Caso 1** trabaja el **diseño de clases** (herencia, encapsulamiento, sobrecarga y sobrescritura); el **Caso 2**, la **aplicación de patrones de diseño** (Factory Method y Strategy) al mismo dominio; y el **Caso 3**, el **modelado UML** (diagrama de clases y diagrama de secuencia) del flujo de tramitación.

---

## Caso 1 — Diseño de clases para la tramitación de licencias

### Enunciado

El Área de Urbanismo necesita digitalizar la tramitación de licencias. Se pide diseñar en **Java** una pequeña jerarquía de clases sobre el dominio `Expediente(idExpediente, estado, fechaApertura)` que represente dos tipos de expediente: **licencias de obra** (con un atributo `tipoLicencia` de valores `"OBRA_MENOR"`, `"OBRA_MAYOR"` o `"ACTIVIDAD"`) y **licencias de terraza** (con un atributo `metrosCuadrados`), cada una con su propia regla de cálculo del plazo de resolución.

### Cuestiones

**Cuestión 1 — Clase base y encapsulamiento (3 puntos).** Diseñe la clase abstracta `Expediente`, con los atributos `idExpediente` y `estado` correctamente encapsulados (visibilidad adecuada), un constructor que inicialice el expediente en estado `"ABIERTO"`, y un método abstracto `calcularPlazoResolucion()`.

**Cuestión 2 — Herencia y sobrescritura (3 puntos).** Diseñe las subclases `ExpedienteLicenciaObra` y `ExpedienteLicenciaTerraza`, cada una con su atributo propio y su implementación de `calcularPlazoResolucion()`: para obra, 90 días si `tipoLicencia` es `"OBRA_MAYOR"` y 30 en el resto de casos; para terraza, 15 días si `metrosCuadrados` es menor o igual a 20, y 30 en caso contrario.

**Cuestión 3 — Sobrecarga (2 puntos).** Añada a `Expediente` dos versiones **sobrecargadas** del método `notificar`: una que reciba solo un `String mensaje` (usa el canal por defecto) y otra que reciba además un `String canal`.

**Cuestión 4 — Razonamiento de diseño (2 puntos).** ¿Por qué `Expediente` debe ser una clase **abstracta** y no una clase concreta con una implementación por defecto de `calcularPlazoResolucion()` que devuelva, por ejemplo, 30 días? Razone la respuesta en términos de los principios SOLID vistos en §1.4.

### Solución orientativa

- **C1**: atributos `private`, constructor que fija `estado = "ABIERTO"`, método abstracto sin cuerpo (§2.1-2.3).

```java
public abstract class Expediente {
    private String idExpediente;
    private String estado;

    public Expediente(String idExpediente) {
        this.idExpediente = idExpediente;
        this.estado = "ABIERTO";
    }

    public abstract int calcularPlazoResolucion();

    public String getEstado() { return estado; }
    public String getIdExpediente() { return idExpediente; }
}
```

- **C2**: cada subclase invoca `super(idExpediente)` y sobrescribe el método abstracto con `@Override` (§2.4-2.5).

```java
public class ExpedienteLicenciaObra extends Expediente {
    private String tipoLicencia;

    public ExpedienteLicenciaObra(String id, String tipoLicencia) {
        super(id);
        this.tipoLicencia = tipoLicencia;
    }

    @Override
    public int calcularPlazoResolucion() {
        return "OBRA_MAYOR".equals(tipoLicencia) ? 90 : 30;
    }
}

public class ExpedienteLicenciaTerraza extends Expediente {
    private double metrosCuadrados;

    public ExpedienteLicenciaTerraza(String id, double metrosCuadrados) {
        super(id);
        this.metrosCuadrados = metrosCuadrados;
    }

    @Override
    public int calcularPlazoResolucion() {
        return metrosCuadrados <= 20 ? 15 : 30;
    }
}
```

- **C3**: mismo nombre, distinta firma, resuelto en tiempo de compilación (§2.5).

```java
public void notificar(String mensaje) {
    notificar(mensaje, "SEDE_ELECTRONICA");  // canal por defecto
}

public void notificar(String mensaje, String canal) {
    System.out.println("[" + canal + "] " + mensaje);
}
```

- **C4**: si `Expediente` fuera concreta con una implementación por defecto arbitraria (30 días), violaría el **principio de responsabilidad única (SRP)** al mezclar "qué es un expediente" con una regla de negocio genérica que no corresponde a ningún tipo real, y sobre todo debilitaría el **principio abierto/cerrado (OCP)**: cualquier desarrollador podría olvidar sobrescribir el método en una subclase nueva y el sistema devolvería silenciosamente un plazo incorrecto (30 días) en lugar de fallar en compilación. Declarar el método `abstract` obliga al compilador a exigir la implementación en cada subclase concreta, haciendo explícito el contrato (§1.4, §2.1).

### Criterios de evaluación

| Criterio | Puntos |
|---|---|
| Clase abstracta con encapsulamiento y constructor correctos | 3 |
| Herencia y sobrescritura correctas en ambas subclases, con reglas exactas | 3 |
| Sobrecarga de `notificar` con firmas distintas y delegación correcta | 2 |
| Razonamiento SOLID (SRP/OCP) sobre por qué debe ser abstracta | 2 |

---

## Caso 2 — Aplicación de patrones de diseño al alta de expedientes

### Enunciado

El módulo de registro necesita: (a) crear el tipo de expediente correcto (obra o terraza, del Caso 1) a partir de un código recibido desde el formulario web, sin que el controlador web conozca las clases concretas; y (b) notificar al ciudadano por el canal que haya elegido (correo, SMS o sede electrónica), pudiendo añadirse nuevos canales en el futuro sin modificar el código existente.

### Cuestiones

**Cuestión 1 — Elección del patrón (2 puntos).** ¿Qué patrón creacional del catálogo GoF aplicaría para resolver la necesidad (a)? Justifique por qué encaja mejor que instanciar directamente cada subclase con `new` en el controlador.

**Cuestión 2 — Implementación del patrón creacional (3 puntos).** Escriba en Java la clase que aplica el patrón elegido en C1, con un método `crear(String tipo, ...)` que devuelva el `Expediente` correspondiente.

**Cuestión 3 — Elección y aplicación del patrón de comportamiento (3 puntos).** ¿Qué patrón de comportamiento aplicaría para resolver la necesidad (b)? Defina en Java la interfaz correspondiente y una implementación para el canal `SEDE_ELECTRONICA`.

**Cuestión 4 — Consecuencias del diseño (2 puntos).** Explique, en términos del principio abierto/cerrado (§1.4), qué cambia en el código existente si el Ayuntamiento añade un tercer tipo de expediente (`ExpedienteVadoPermanente`) y un cuarto canal de notificación (push en la app municipal).

### Solución orientativa

- **C1**: **Factory Method**. Instanciar directamente con `new ExpedienteLicenciaObra(...)` o `new ExpedienteLicenciaTerraza(...)` en el controlador acopla el código web a las clases concretas y obliga a modificar el controlador cada vez que se añada un tipo nuevo, violando OCP (§4.1, §4.3).

- **C2**:

```java
public class ExpedienteFactory {
    public static Expediente crear(String tipo, String id, Object datoExtra) {
        return switch (tipo) {
            case "OBRA"    -> new ExpedienteLicenciaObra(id, (String) datoExtra);
            case "TERRAZA" -> new ExpedienteLicenciaTerraza(id, (Double) datoExtra);
            default -> throw new IllegalArgumentException("Tipo de expediente no soportado: " + tipo);
        };
    }
}
```

- **C3**: **Strategy**, para intercambiar el algoritmo de envío sin tocar el código que decide "cuándo" notificar (§4.5, §1.4).

```java
public interface CanalNotificacion {
    void enviar(String destinatario, String mensaje);
}

public class NotificacionSedeElectronica implements CanalNotificacion {
    @Override
    public void enviar(String destinatario, String mensaje) {
        System.out.println("[SEDE] Para " + destinatario + ": " + mensaje);
    }
}
```

- **C4**: con Factory Method, añadir `ExpedienteVadoPermanente` solo exige un nuevo `case` en `ExpedienteFactory.crear(...)` y la nueva clase; el controlador que invoca la fábrica **no cambia**. Con Strategy, añadir la notificación push solo exige una nueva clase `NotificacionPush implements CanalNotificacion`; el código que recibe una referencia `CanalNotificacion` y llama a `enviar(...)` **tampoco cambia**. En ambos casos el sistema queda **abierto a extensión, cerrado a modificación** (§1.4): se añade código nuevo, no se toca el existente.

### Criterios de evaluación

| Criterio | Puntos |
|---|---|
| Identifica Factory Method y justifica correctamente frente a `new` directo | 2 |
| Implementación correcta de la fábrica, con manejo del caso no soportado | 3 |
| Identifica Strategy, define interfaz e implementación correctas | 3 |
| Explica correctamente el cumplimiento de OCP en ambas extensiones | 2 |

---

## Caso 3 — Modelado UML del flujo de tramitación

### Enunciado

Antes de programar el módulo de licencias del Caso 1, el equipo de análisis necesita fijar el diseño con UML para validarlo con el Área de Urbanismo. Se pide modelar, con la notación estudiada en §5, tanto la estructura estática de clases como el flujo dinámico de una solicitud.

### Cuestiones

**Cuestión 1 — Diagrama de Clases (4 puntos).** Describa, con la notación de UML (compartimentos, visibilidad y tipo de relación), el diagrama de clases de `Expediente`, `ExpedienteLicenciaObra`, `ExpedienteLicenciaTerraza` y `CanalNotificacion` (Caso 2), incluyendo el tipo exacto de relación entre `Expediente` y `CanalNotificacion` si un expediente mantiene una referencia permanente a su canal de notificación preferido.

**Cuestión 2 — Diagrama de Casos de Uso (2 puntos).** Identifique el actor y el caso de uso principal de "solicitar una licencia de obra", y proponga una relación `«include»` con otro caso de uso que sea un paso obligatorio y reutilizado en otras solicitudes.

**Cuestión 3 — Diagrama de Secuencia (3 puntos).** Describa, en orden temporal, los mensajes intercambiados entre `Ciudadano`, `PortalWeb`, `ExpedienteFactory` y el `Expediente` creado, desde que el ciudadano envía el formulario hasta que recibe la confirmación con el plazo de resolución.

**Cuestión 4 — Elección del diagrama (1 punto).** Si el objetivo fuera mostrar, en un mismo esquema, en qué distrito de la administración física reside el servidor que aloja el módulo de licencias, ¿qué diagrama UML usaría, y de qué familia (estructural o de comportamiento) es?

### Solución orientativa

- **C1**: `Expediente` es la superclase abstracta; `ExpedienteLicenciaObra` y `ExpedienteLicenciaTerraza` se conectan a ella con una flecha de **generalización** (triángulo hueco). La relación entre `Expediente` y `CanalNotificacion` es una **asociación** (§2.8, §5.3): `Expediente` conoce y colabora con `CanalNotificacion` a través de una referencia permanente (un atributo), pero no controla su ciclo de vida (el canal existe con independencia del expediente) — no es composición ni agregación, porque no hay relación «todo-parte», sino simple colaboración entre objetos de distinta naturaleza.

- **C2**: actor **Ciudadano**; caso de uso principal **"Solicitar licencia de obra"**, que incluye (`«include»`) el caso de uso **"Autenticarse en sede electrónica"**, paso obligatorio también en otras solicitudes (licencia de terraza, alta de vado, etc.) (§5.5).

- **C3**: `Ciudadano → PortalWeb: enviarSolicitud(datosFormulario)` · `PortalWeb → ExpedienteFactory: crear("OBRA", id, tipoLicencia)` · `ExpedienteFactory → ExpedienteLicenciaObra: new` (mensaje de creación) · `PortalWeb → ExpedienteLicenciaObra: calcularPlazoResolucion()` · `ExpedienteLicenciaObra --> PortalWeb: 90` (retorno, flecha discontinua) · `PortalWeb --> Ciudadano: confirmación con plazo = 90 días` (§5.6).

- **C4**: **Diagrama de Despliegue**, de la familia **estructural** (§5.4): es el único diagrama UML centrado en los nodos de hardware y su ubicación física, frente al Diagrama de Componentes (organización lógica de módulos software) o al de Clases (diseño de código).

### Criterios de evaluación

| Criterio | Puntos |
|---|---|
| Diagrama de clases correcto: compartimentos, generalización y relación Expediente-CanalNotificacion identificada como asociación | 4 |
| Actor, caso de uso principal y relación «include» correctos y justificados | 2 |
| Secuencia de mensajes completa y en el orden temporal correcto | 3 |
| Identifica correctamente el Diagrama de Despliegue y su familia | 1 |

---

*Los tres casos son orientativos y pensados para la autoevaluación; las soluciones muestran una vía correcta, no la única posible. El código de los Casos 1 y 2 está escrito en Java (decisión de Joan); el Caso 3 se resuelve con descripciones textuales de la notación UML, sin depender de ninguna herramienta de modelado concreta.*
