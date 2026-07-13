# Tema 20 — Catálogo de Diagramas

> **Título oficial**: Diseño y programación orientada a objetos. Objetos, clases, herencia, métodos, sobrecarga. Ventajas e inconvenientes. Patrones de diseño y UML.
>
> **Versión**: v1.0
> **Fecha**: 2026-07-13
> **Autor**: ETRIVIUM
> **Formato**: SVG inline (zero-dependencias, escalable, imprimible, accesible con role/aria-label)
> **Paleta**: Ayuntamiento de Madrid #0055a0 (primario) + #d13c3c (alertas) + #2d8659 (ventajas) + #e89822 (callouts)
> **Nota técnica**: las clases CSS de cada SVG llevan sufijo numérico único (`.t1`, `.h1`…) para evitar colisiones de estilos entre los 12 diagramas embebidos en la misma página.

---

## Índice de diagramas

| ID | Título | Sección | Tipo | Formato |
|---|---|---|---|---|
| D1 | Evolución hacia el paradigma OO | §1.1 | Línea de tiempo | 680×300 |
| D2 | Los 4 pilares de la POO | §1.2 | Bloques | 680×280 |
| D3 | Principios SOLID | §1.4 | Cheat sheet | 660×360 |
| D4 | Anatomía de una clase y un objeto | §2.1-2.2 | Bloques | 640×320 |
| D5 | Modificadores de visibilidad | §2.3 | Matriz | 680×320 |
| D6 | Herencia simple frente a herencia múltiple | §2.4 | Comparativa | 680×340 |
| D7 | Sobrecarga frente a sobrescritura | §2.5 | Comparativa | 680×300 |
| D8 | Polimorfismo y ligadura dinámica | §2.6 | Flujo | 660×320 |
| D9 | Catálogo de patrones GoF (23) | §4.1-4.5 | Matriz | 680×320 |
| D10 | Patrón Factory Method aplicado | §4.3 | Mini clase UML | 660×340 |
| D11 | Notación del Diagrama de Clases UML | §5.3 | Notación | 680×380 |
| D12 | Familias de diagramas UML de comportamiento | §5.5-5.7 | Bloques | 680×320 |

---

## D1 · Evolución hacia el paradigma OO

**Sección**: §1.1 — Evolución de la ingeniería del software hacia el paradigma OO
**Propósito**: Fijar el orden histórico de paradigmas y los hitos de lenguaje de la POO.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 300" role="img" aria-label="Línea de tiempo de la evolución de los paradigmas de programación: no estructurada, estructurada, modular y orientada a objetos, con los hitos Simula 67, Smalltalk, C++ y Java">
  <style>.t1{font:700 12px system-ui,sans-serif;fill:#fff}.s1{font:10px system-ui,sans-serif;fill:#fff}.l1{font:11px system-ui,sans-serif;fill:#444}.h1{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="24" text-anchor="middle" class="h1">De la programación no estructurada al paradigma orientado a objetos</text>
  <line x1="50" y1="70" x2="630" y2="70" stroke="#0055a0" stroke-width="2"/>
  <circle cx="90" cy="70" r="6" fill="#0055a0"/>
  <circle cx="270" cy="70" r="6" fill="#0055a0"/>
  <circle cx="450" cy="70" r="6" fill="#0055a0"/>
  <circle cx="610" cy="70" r="6" fill="#2d8659"/>
  <rect x="30" y="90" width="120" height="46" rx="6" fill="#0055a0"/><text x="90" y="110" text-anchor="middle" class="t1">NO</text><text x="90" y="126" text-anchor="middle" class="s1">ESTRUCTURADA</text>
  <rect x="210" y="90" width="120" height="46" rx="6" fill="#0055a0"/><text x="270" y="110" text-anchor="middle" class="t1">ESTRUCTURADA</text><text x="270" y="126" text-anchor="middle" class="s1">Böhm-Jacopini</text>
  <rect x="390" y="90" width="120" height="46" rx="6" fill="#0055a0"/><text x="450" y="110" text-anchor="middle" class="t1">MODULAR</text><text x="450" y="126" text-anchor="middle" class="s1">proc. y func.</text>
  <rect x="550" y="90" width="120" height="46" rx="6" fill="#2d8659"/><text x="610" y="110" text-anchor="middle" class="t1">ORIENTADA A</text><text x="610" y="126" text-anchor="middle" class="s1">OBJETOS</text>
  <text x="90" y="160" text-anchor="middle" class="l1">GOTO,</text>
  <text x="90" y="174" text-anchor="middle" class="l1">saltos incondicionales</text>
  <text x="270" y="160" text-anchor="middle" class="l1">Secuencia · Selección</text>
  <text x="270" y="174" text-anchor="middle" class="l1">Iteración</text>
  <text x="450" y="160" text-anchor="middle" class="l1">Datos separados</text>
  <text x="450" y="174" text-anchor="middle" class="l1">de las funciones</text>
  <text x="610" y="160" text-anchor="middle" class="l1">Objetos: datos +</text>
  <text x="610" y="174" text-anchor="middle" class="l1">comportamiento juntos</text>
  <rect x="470" y="200" width="180" height="80" rx="6" fill="#eef4fa" stroke="#0055a0"/>
  <text x="560" y="220" text-anchor="middle" style="font:700 11px system-ui;fill:#0055a0">Hitos del lenguaje OO</text>
  <text x="480" y="238" class="l1">1967 · Simula 67</text>
  <text x="480" y="252" class="l1">1970s · Smalltalk</text>
  <text x="480" y="266" class="l1">1983 · C++</text>
  <text x="480" y="280" class="l1" style="font-weight:700">1995 · Java</text>
  <text x="670" y="292" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: BOOCH07; GOSLING-JLS]</text>
</svg>
```

---

## D2 · Los 4 pilares de la POO

**Sección**: §1.2 — Pilares fundamentales de la POO
**Propósito**: Presentar de un vistazo abstracción, encapsulamiento, herencia y polimorfismo.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 280" role="img" aria-label="Los cuatro pilares de la programación orientada a objetos: abstracción, encapsulamiento, herencia y polimorfismo">
  <style>.t2{font:700 13px system-ui,sans-serif;fill:#fff}.s2{font:10.5px system-ui,sans-serif;fill:#fff}.h2{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="24" text-anchor="middle" class="h2">4 PILARES DE LA POO</text>
  <rect x="30" y="44" width="150" height="140" rx="8" fill="#0055a0"/>
  <text x="105" y="72" text-anchor="middle" class="t2">ABSTRACCIÓN</text>
  <text x="105" y="98" text-anchor="middle" class="s2">Qué hace el objeto</text>
  <text x="105" y="114" text-anchor="middle" class="s2">(interfaz pública)</text>
  <text x="105" y="140" text-anchor="middle" class="s2">§1.2</text>
  <rect x="195" y="44" width="150" height="140" rx="8" fill="#0055a0"/>
  <text x="270" y="72" text-anchor="middle" class="t2">ENCAPSULA-</text>
  <text x="270" y="88" text-anchor="middle" class="t2">MIENTO</text>
  <text x="270" y="112" text-anchor="middle" class="s2">Cómo oculta su</text>
  <text x="270" y="128" text-anchor="middle" class="s2">estado interno</text>
  <text x="270" y="150" text-anchor="middle" class="s2">§1.2</text>
  <rect x="360" y="44" width="150" height="140" rx="8" fill="#2d8659"/>
  <text x="435" y="72" text-anchor="middle" class="t2">HERENCIA</text>
  <text x="435" y="98" text-anchor="middle" class="s2">Reutiliza por</text>
  <text x="435" y="114" text-anchor="middle" class="s2">especialización</text>
  <text x="435" y="140" text-anchor="middle" class="s2">§2.4</text>
  <rect x="525" y="44" width="130" height="140" rx="8" fill="#2d8659"/>
  <text x="590" y="72" text-anchor="middle" class="t2">POLIMOR-</text>
  <text x="590" y="88" text-anchor="middle" class="t2">FISMO</text>
  <text x="590" y="112" text-anchor="middle" class="s2">Una interfaz,</text>
  <text x="590" y="128" text-anchor="middle" class="s2">muchas formas</text>
  <text x="590" y="150" text-anchor="middle" class="s2">§2.6</text>
  <text x="340" y="212" text-anchor="middle" style="font:11px system-ui;fill:#444">Abstracción + Encapsulamiento fijan el DISEÑO de una clase aislada;</text>
  <text x="340" y="230" text-anchor="middle" style="font:11px system-ui;fill:#444">Herencia + Polimorfismo fijan las RELACIONES entre clases de una jerarquía</text>
  <text x="670" y="270" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: BOOCH07; MEYER97]</text>
</svg>
```

---

## D3 · Principios SOLID

**Sección**: §1.4 — Principios SOLID de diseño de software
**Propósito**: Cheat sheet de las cinco letras del acrónimo con su nombre y su idea clave.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 660 360" role="img" aria-label="Cheat sheet de los cinco principios SOLID: responsabilidad única, abierto cerrado, sustitución de Liskov, segregación de interfaces e inversión de dependencias">
  <style>.t3{font:700 14px system-ui,sans-serif;fill:#fff}.n3{font:700 12px system-ui,sans-serif;fill:#fff}.l3{font:11px system-ui,sans-serif;fill:#444}.h3{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="330" y="24" text-anchor="middle" class="h3">SOLID — 5 principios de diseño OO [MARTIN03]</text>
  <g>
    <rect x="30" y="40" width="40" height="40" rx="6" fill="#0055a0"/><text x="50" y="66" text-anchor="middle" class="t3">S</text>
    <text x="85" y="58" class="n3" style="fill:#0055a0">Single Responsibility</text>
    <text x="85" y="74" class="l3">Una clase, una única razón para cambiar</text>
  </g>
  <g>
    <rect x="30" y="94" width="40" height="40" rx="6" fill="#0055a0"/><text x="50" y="120" text-anchor="middle" class="t3">O</text>
    <text x="85" y="112" class="n3" style="fill:#0055a0">Open/Closed</text>
    <text x="85" y="128" class="l3">Abierta a extensión, cerrada a modificación</text>
  </g>
  <g>
    <rect x="30" y="148" width="40" height="40" rx="6" fill="#0055a0"/><text x="50" y="174" text-anchor="middle" class="t3">L</text>
    <text x="85" y="166" class="n3" style="fill:#0055a0">Liskov Substitution</text>
    <text x="85" y="182" class="l3">Una subclase debe poder sustituir a su superclase</text>
  </g>
  <g>
    <rect x="30" y="202" width="40" height="40" rx="6" fill="#0055a0"/><text x="50" y="228" text-anchor="middle" class="t3">I</text>
    <text x="85" y="220" class="n3" style="fill:#0055a0">Interface Segregation</text>
    <text x="85" y="236" class="l3">Varias interfaces específicas, no una sobrecargada</text>
  </g>
  <g>
    <rect x="30" y="256" width="40" height="40" rx="6" fill="#0055a0"/><text x="50" y="282" text-anchor="middle" class="t3">D</text>
    <text x="85" y="274" class="n3" style="fill:#0055a0">Dependency Inversion</text>
    <text x="85" y="290" class="l3">Depender de abstracciones, no de clases concretas</text>
  </g>
  <text x="330" y="322" text-anchor="middle" style="font:700 12px system-ui;fill:#e89822">SOLID sistematiza el objetivo alta cohesión + bajo acoplamiento (§1.3)</text>
  <text x="650" y="350" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: MARTIN00; MARTIN03; LISKOV94]</text>
</svg>
```

---

## D4 · Anatomía de una clase y un objeto

**Sección**: §2.1-2.2 — Clases y objetos; atributos, métodos y constructores
**Propósito**: Distinguir visualmente la clase (plantilla) de sus instancias (objetos).

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 320" role="img" aria-label="Anatomía de una clase Expediente con tres compartimentos (nombre, atributos, métodos) y dos objetos instanciados a partir de ella con estado propio">
  <style>.t4{font:700 12px system-ui,sans-serif;fill:#fff}.s4{font:10.5px system-ui,sans-serif;fill:#123}.m4{font:10.5px monospace;fill:#123}.l4{font:11px system-ui,sans-serif;fill:#444}.h4{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="320" y="20" text-anchor="middle" class="h4">CLASE (plantilla) → OBJETOS (instancias)</text>
  <rect x="230" y="34" width="180" height="110" fill="#fff" stroke="#0055a0" stroke-width="1.5"/>
  <rect x="230" y="34" width="180" height="24" fill="#0055a0"/><text x="320" y="50" text-anchor="middle" class="t4">Expediente</text>
  <line x1="230" y1="58" x2="410" y2="58" stroke="#0055a0"/>
  <text x="236" y="72" class="m4">- idExpediente</text>
  <text x="236" y="86" class="m4">- estado</text>
  <line x1="230" y1="94" x2="410" y2="94" stroke="#0055a0"/>
  <text x="236" y="108" class="m4">+ getEstado()</text>
  <text x="236" y="122" class="m4">+ calcularPlazo()</text>
  <text x="320" y="164" text-anchor="middle" class="l4">new ExpedienteLicencia(...) ↓</text>
  <rect x="60" y="180" width="220" height="100" fill="#eef4fa" stroke="#0055a0"/>
  <rect x="60" y="180" width="220" height="24" fill="#2d8659"/><text x="170" y="196" text-anchor="middle" class="t4">exp001 : ExpedienteLicencia</text>
  <text x="70" y="216" class="m4">idExpediente = "EXP-001"</text>
  <text x="70" y="232" class="m4">estado = "ABIERTO"</text>
  <text x="70" y="248" class="m4">tipoLicencia = "OBRA_MAYOR"</text>
  <rect x="360" y="180" width="220" height="100" fill="#eef4fa" stroke="#0055a0"/>
  <rect x="360" y="180" width="220" height="24" fill="#2d8659"/><text x="470" y="196" text-anchor="middle" class="t4">exp002 : ExpedienteTributario</text>
  <text x="370" y="216" class="m4">idExpediente = "EXP-002"</text>
  <text x="370" y="232" class="m4">estado = "ABIERTO"</text>
  <text x="370" y="248" class="m4">importe = 312.40</text>
  <text x="320" y="300" text-anchor="middle" class="l4">Cada objeto tiene su propio estado; comparten la misma estructura y comportamiento definidos en la clase</text>
  <text x="630" y="314" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: BOOCH07, cap. 2]</text>
</svg>
```

---

## D5 · Modificadores de visibilidad

**Sección**: §2.3 — Visibilidad y control de acceso
**Propósito**: Visualizar el alcance de los cuatro modificadores de acceso de Java.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 320" role="img" aria-label="Matriz de los cuatro modificadores de acceso de Java: private, package-private, protected y public, y su visibilidad desde la misma clase, el mismo paquete, una subclase o cualquier clase">
  <style>.t5{font:700 11px system-ui,sans-serif;fill:#fff}.s5{font:10px system-ui,sans-serif;fill:#123}.h5{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h5">Modificadores de acceso: de más restrictivo a más abierto</text>
  <rect x="30" y="40" width="140" height="26" fill="#0055a0"/><text x="100" y="58" text-anchor="middle" class="t5">private</text>
  <rect x="180" y="40" width="140" height="26" fill="#0055a0"/><text x="250" y="58" text-anchor="middle" class="t5">(package)</text>
  <rect x="330" y="40" width="140" height="26" fill="#2d8659"/><text x="400" y="58" text-anchor="middle" class="t5">protected</text>
  <rect x="480" y="40" width="140" height="26" fill="#2d8659"/><text x="550" y="58" text-anchor="middle" class="t5">public</text>
  <line x1="30" y1="80" x2="620" y2="80" stroke="#ccc"/>
  <text x="30" y="100" class="s5" style="font-weight:700">Misma clase</text>
  <text x="100" y="100" text-anchor="middle" class="s5">✓</text><text x="250" y="100" text-anchor="middle" class="s5">✓</text><text x="400" y="100" text-anchor="middle" class="s5">✓</text><text x="550" y="100" text-anchor="middle" class="s5">✓</text>
  <line x1="30" y1="116" x2="620" y2="116" stroke="#eee"/>
  <text x="30" y="136" class="s5" style="font-weight:700">Mismo paquete</text>
  <text x="100" y="136" text-anchor="middle" class="s5">✗</text><text x="250" y="136" text-anchor="middle" class="s5">✓</text><text x="400" y="136" text-anchor="middle" class="s5">✓</text><text x="550" y="136" text-anchor="middle" class="s5">✓</text>
  <line x1="30" y1="152" x2="620" y2="152" stroke="#eee"/>
  <text x="30" y="172" class="s5" style="font-weight:700">Subclase (otro paquete)</text>
  <text x="100" y="172" text-anchor="middle" class="s5">✗</text><text x="250" y="172" text-anchor="middle" class="s5">✗</text><text x="400" y="172" text-anchor="middle" class="s5">✓</text><text x="550" y="172" text-anchor="middle" class="s5">✓</text>
  <line x1="30" y1="188" x2="620" y2="188" stroke="#eee"/>
  <text x="30" y="208" class="s5" style="font-weight:700">Cualquier clase</text>
  <text x="100" y="208" text-anchor="middle" class="s5">✗</text><text x="250" y="208" text-anchor="middle" class="s5">✗</text><text x="400" y="208" text-anchor="middle" class="s5">✗</text><text x="550" y="208" text-anchor="middle" class="s5">✓</text>
  <text x="325" y="250" text-anchor="middle" style="font:700 12px system-ui;fill:#e89822">Regla de diseño: exponer el mínimo nivel de visibilidad necesario</text>
  <text x="325" y="270" text-anchor="middle" style="font:11px system-ui;fill:#444">En UML: - private · # protected · ~ package · + public (§5.3)</text>
  <text x="670" y="308" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: GOSLING-JLS §6.6]</text>
</svg>
```

---

## D6 · Herencia simple frente a herencia múltiple

**Sección**: §2.4 — Mecanismos avanzados en POO: herencia simple y múltiple
**Propósito**: Contrastar la herencia simple de Java con la múltiple de C++ y el problema del diamante.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 340" role="img" aria-label="Comparación entre herencia simple de Java, con una sola superclase, y herencia múltiple de C++, que puede producir el problema del diamante cuando dos superclases comparten un ancestro común">
  <style>.t6{font:700 11px system-ui,sans-serif;fill:#fff}.l6{font:11px system-ui,sans-serif;fill:#444}.h6{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h6">Herencia simple (Java) frente a herencia múltiple (C++)</text>
  <text x="150" y="44" text-anchor="middle" style="font:700 12px system-ui;fill:#2d8659">HERENCIA SIMPLE</text>
  <rect x="100" y="56" width="100" height="30" rx="4" fill="#0055a0"/><text x="150" y="76" text-anchor="middle" class="t6">Expediente</text>
  <line x1="150" y1="86" x2="150" y2="106" stroke="#0055a0" stroke-width="2"/><polygon points="150,112 144,102 156,102" fill="#0055a0"/>
  <rect x="100" y="112" width="100" height="30" rx="4" fill="#2d8659"/><text x="150" y="132" text-anchor="middle" class="t6">ExpLicencia</text>
  <text x="150" y="164" text-anchor="middle" class="l6">Una única superclase.</text>
  <text x="150" y="180" text-anchor="middle" class="l6">Sin ambigüedad posible.</text>
  <line x1="330" y1="30" x2="330" y2="320" stroke="#ddd"/>
  <text x="510" y="44" text-anchor="middle" style="font:700 12px system-ui;fill:#d13c3c">HERENCIA MÚLTIPLE — diamante</text>
  <rect x="460" y="56" width="100" height="28" rx="4" fill="#0055a0"/><text x="510" y="75" text-anchor="middle" class="t6">A</text>
  <line x1="490" y1="84" x2="440" y2="112" stroke="#0055a0" stroke-width="2"/>
  <line x1="530" y1="84" x2="580" y2="112" stroke="#0055a0" stroke-width="2"/>
  <rect x="390" y="112" width="100" height="28" rx="4" fill="#0055a0"/><text x="440" y="131" text-anchor="middle" class="t6">B (redefine m)</text>
  <rect x="530" y="112" width="100" height="28" rx="4" fill="#0055a0"/><text x="580" y="131" text-anchor="middle" class="t6">C (redefine m)</text>
  <line x1="440" y1="140" x2="490" y2="168" stroke="#d13c3c" stroke-width="2"/>
  <line x1="580" y1="140" x2="530" y2="168" stroke="#d13c3c" stroke-width="2"/>
  <rect x="460" y="168" width="100" height="28" rx="4" fill="#d13c3c"/><text x="510" y="187" text-anchor="middle" class="t6">D — ¿m()?</text>
  <text x="510" y="222" text-anchor="middle" class="l6">D hereda de B y C, que redefinen "m":</text>
  <text x="510" y="238" text-anchor="middle" class="l6">¿qué versión de "m" usa D? — ambigüedad</text>
  <text x="330" y="280" text-anchor="middle" style="font:700 12px system-ui;fill:#e89822">Java prohíbe el diamante: extends simple + implements múltiple de interfaces</text>
  <text x="670" y="328" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: GOSLING-JLS; MEYER97]</text>
</svg>
```

---

## D7 · Sobrecarga frente a sobrescritura

**Sección**: §2.5 — Sobrecarga y sobrescritura de métodos
**Propósito**: Contraste directo entre overloading (compilación) y overriding (ejecución) — la pregunta más recurrente del tema.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 300" role="img" aria-label="Comparación entre sobrecarga de métodos, resuelta en tiempo de compilación dentro de la misma clase, y sobrescritura de métodos, resuelta en tiempo de ejecución entre superclase y subclase">
  <style>.t7{font:700 12px system-ui,sans-serif;fill:#fff}.s7{font:10.5px system-ui,sans-serif;fill:#fff}.l7{font:11px system-ui,sans-serif;fill:#444}.h7{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="22" text-anchor="middle" class="h7">SOBRECARGA (overloading) frente a SOBRESCRITURA (overriding)</text>
  <rect x="40" y="40" width="290" height="170" rx="8" fill="#0055a0"/>
  <text x="185" y="66" text-anchor="middle" class="t7">SOBRECARGA</text>
  <text x="185" y="88" text-anchor="middle" class="s7">Mismo nombre, DISTINTA firma</text>
  <text x="185" y="106" text-anchor="middle" class="s7">Misma clase</text>
  <text x="185" y="128" text-anchor="middle" class="s7">notificar(String)</text>
  <text x="185" y="144" text-anchor="middle" class="s7">notificar(String, String)</text>
  <text x="185" y="172" text-anchor="middle" style="font:700 11px system-ui;fill:#fff">Ligadura ESTÁTICA</text>
  <text x="185" y="190" text-anchor="middle" class="s7">(tiempo de compilación)</text>
  <rect x="350" y="40" width="290" height="170" rx="8" fill="#2d8659"/>
  <text x="495" y="66" text-anchor="middle" class="t7">SOBRESCRITURA</text>
  <text x="495" y="88" text-anchor="middle" class="s7">MISMA firma, distinta clase</text>
  <text x="495" y="106" text-anchor="middle" class="s7">Superclase → subclase</text>
  <text x="495" y="128" text-anchor="middle" class="s7">@Override</text>
  <text x="495" y="144" text-anchor="middle" class="s7">calcularPlazoResolucion()</text>
  <text x="495" y="172" text-anchor="middle" style="font:700 11px system-ui;fill:#fff">Ligadura DINÁMICA</text>
  <text x="495" y="190" text-anchor="middle" class="s7">(tiempo de ejecución)</text>
  <text x="340" y="240" text-anchor="middle" style="font:700 12px system-ui;fill:#e89822">Overloading ≈ mismo nombre distinta lista de parámetros ; Overriding ≈ redefinición heredada</text>
  <text x="670" y="284" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: GOSLING-JLS §8.4]</text>
</svg>
```

---

## D8 · Polimorfismo y ligadura dinámica

**Sección**: §2.6 — Polimorfismo y ligadura dinámica
**Propósito**: Mostrar cómo una variable de tipo superclase invoca, en ejecución, el método de la clase real del objeto.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 660 320" role="img" aria-label="Diagrama de polimorfismo: una lista de referencias de tipo Expediente contiene objetos de distintas subclases, y al invocar calcularPlazoResolucion se ejecuta la versión de la clase real de cada objeto en tiempo de ejecución">
  <style>.t8{font:700 11px system-ui,sans-serif;fill:#fff}.m8{font:10.5px monospace;fill:#123}.l8{font:11px system-ui,sans-serif;fill:#444}.h8{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="330" y="20" text-anchor="middle" class="h8">Polimorfismo: mismo mensaje, distinta ejecución según el objeto real</text>
  <rect x="40" y="40" width="220" height="30" fill="#0055a0"/><text x="150" y="60" text-anchor="middle" class="t8">List&lt;Expediente&gt; expedientes</text>
  <line x1="90" y1="70" x2="90" y2="106" stroke="#0055a0" stroke-width="2"/>
  <line x1="210" y1="70" x2="210" y2="106" stroke="#0055a0" stroke-width="2"/>
  <rect x="30" y="106" width="150" height="30" rx="4" fill="#2d8659"/><text x="105" y="126" text-anchor="middle" class="t8">e : ExpLicencia</text>
  <rect x="200" y="106" width="160" height="30" rx="4" fill="#2d8659"/><text x="280" y="126" text-anchor="middle" class="t8">e : ExpTributario</text>
  <text x="330" y="166" text-anchor="middle" class="l8">e.calcularPlazoResolucion()  →  la JVM consulta la tabla de métodos de la clase REAL</text>
  <line x1="105" y1="136" x2="105" y2="200" stroke="#2d8659" stroke-width="2"/>
  <line x1="280" y1="136" x2="280" y2="200" stroke="#2d8659" stroke-width="2"/>
  <rect x="30" y="200" width="150" height="34" rx="4" fill="#eef4fa" stroke="#2d8659"/><text x="105" y="222" text-anchor="middle" class="m8">return 90</text>
  <rect x="200" y="200" width="160" height="34" rx="4" fill="#eef4fa" stroke="#2d8659"/><text x="280" y="222" text-anchor="middle" class="m8">return 20</text>
  <text x="105" y="256" text-anchor="middle" class="l8">tipo declarado:</text>
  <text x="105" y="270" text-anchor="middle" class="l8">Expediente</text>
  <text x="280" y="256" text-anchor="middle" class="l8">tipo real: distinto</text>
  <text x="280" y="270" text-anchor="middle" class="l8">en cada iteración</text>
  <text x="650" y="308" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: BOOCH07; GOSLING-JLS]</text>
</svg>
```

---

## D9 · Catálogo de patrones GoF (23)

**Sección**: §4.1-4.5 — Concepto, catálogo y clasificación técnica de patrones de diseño
**Propósito**: Distribución de los 23 patrones GoF en sus tres familias, para memorizar la cifra exacta.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 320" role="img" aria-label="Los 23 patrones de diseño del catálogo Gang of Four, agrupados en 5 patrones creacionales, 7 estructurales y 11 de comportamiento">
  <style>.t9{font:700 13px system-ui,sans-serif;fill:#fff}.s9{font:10px system-ui,sans-serif;fill:#fff}.n9{font:700 22px system-ui,sans-serif;fill:#fff}.h9{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h9">CATÁLOGO GoF — 23 patrones de diseño [GOF94]</text>
  <rect x="30" y="40" width="190" height="140" rx="8" fill="#0055a0"/>
  <text x="125" y="66" text-anchor="middle" class="n9">5</text>
  <text x="125" y="88" text-anchor="middle" class="t9">CREACIONALES</text>
  <text x="125" y="108" text-anchor="middle" class="s9">Singleton · Factory Method</text>
  <text x="125" y="122" text-anchor="middle" class="s9">Abstract Factory</text>
  <text x="125" y="136" text-anchor="middle" class="s9">Builder · Prototype</text>
  <rect x="245" y="40" width="190" height="140" rx="8" fill="#2d8659"/>
  <text x="340" y="66" text-anchor="middle" class="n9">7</text>
  <text x="340" y="88" text-anchor="middle" class="t9">ESTRUCTURALES</text>
  <text x="340" y="108" text-anchor="middle" class="s9">Adapter · Bridge · Composite</text>
  <text x="340" y="122" text-anchor="middle" class="s9">Decorator · Facade</text>
  <text x="340" y="136" text-anchor="middle" class="s9">Flyweight · Proxy</text>
  <rect x="460" y="40" width="190" height="140" rx="8" fill="#e89822"/>
  <text x="555" y="66" text-anchor="middle" class="n9">11</text>
  <text x="555" y="88" text-anchor="middle" class="t9">COMPORTAMIENTO</text>
  <text x="555" y="108" text-anchor="middle" class="s9">Strategy · Observer · State</text>
  <text x="555" y="122" text-anchor="middle" class="s9">Command · Template Method…</text>
  <text x="555" y="136" text-anchor="middle" class="s9">(11 en total)</text>
  <text x="340" y="204" text-anchor="middle" style="font:700 13px system-ui;fill:#123">¿CÓMO se crean los objetos? · ¿CÓMO se componen? · ¿CÓMO colaboran?</text>
  <text x="340" y="230" text-anchor="middle" style="font:11px system-ui;fill:#444">Cada patrón documenta: intención, aplicabilidad, estructura (mini UML) y consecuencias</text>
  <text x="670" y="300" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: GOF94, cap. 1]</text>
</svg>
```

---

## D10 · Patrón Factory Method aplicado

**Sección**: §4.3 — Clasificación técnica: patrones creacionales
**Propósito**: Mini diagrama de clases UML del patrón Factory Method sobre la jerarquía Expediente.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 660 340" role="img" aria-label="Diagrama de clases del patrón Factory Method aplicado a la jerarquía Expediente: ExpedienteFactory crea objetos ExpedienteLicencia o ExpedienteTributario sin que el cliente conozca las clases concretas">
  <style>.t10{font:700 11px system-ui,sans-serif;fill:#fff}.m10{font:10px monospace;fill:#123}.l10{font:11px system-ui,sans-serif;fill:#444}.h10{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="330" y="20" text-anchor="middle" class="h10">Factory Method: desacopla al cliente de las clases concretas</text>
  <rect x="40" y="44" width="150" height="50" rx="4" fill="#0055a0"/><text x="115" y="74" text-anchor="middle" class="t10">Cliente</text>
  <line x1="190" y1="70" x2="240" y2="70" stroke="#0055a0" stroke-width="2" stroke-dasharray="4,3"/>
  <rect x="240" y="44" width="180" height="50" rx="4" fill="#0055a0"/><text x="330" y="66" text-anchor="middle" class="t10">ExpedienteFactory</text><text x="330" y="82" text-anchor="middle" class="m10">+ crear(tipo)</text>
  <line x1="330" y1="94" x2="200" y2="150" stroke="#2d8659" stroke-width="2"/>
  <line x1="330" y1="94" x2="460" y2="150" stroke="#2d8659" stroke-width="2"/>
  <rect x="120" y="150" width="160" height="60" fill="#fff" stroke="#0055a0" stroke-width="1.5"/>
  <rect x="120" y="150" width="160" height="22" fill="#0055a0"/><text x="200" y="166" text-anchor="middle" class="t10">ExpedienteLicencia</text>
  <text x="128" y="188" class="m10">tipoLicencia: String</text>
  <text x="128" y="202" class="m10">calcularPlazo(): int</text>
  <rect x="380" y="150" width="180" height="60" fill="#fff" stroke="#0055a0" stroke-width="1.5"/>
  <rect x="380" y="150" width="180" height="22" fill="#0055a0"/><text x="470" y="166" text-anchor="middle" class="t10">ExpedienteTributario</text>
  <text x="388" y="188" class="m10">importe: double</text>
  <text x="388" y="202" class="m10">calcularPlazo(): int</text>
  <text x="330" y="248" text-anchor="middle" class="l10">Cliente solo conoce ExpedienteFactory.crear(tipo);</text>
  <text x="330" y="264" text-anchor="middle" class="l10">añadir un nuevo tipo de expediente no modifica al Cliente (principio abierto/cerrado, §1.4)</text>
  <text x="650" y="326" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: GOF94]</text>
</svg>
```

---

## D11 · Notación del Diagrama de Clases UML

**Sección**: §5.3 — Diagramas estructurales y estáticos
**Propósito**: Fijar la notación de caja de 3 compartimentos y los 5 tipos de relación entre clases.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 380" role="img" aria-label="Notación del diagrama de clases UML: caja de tres compartimentos con nombre, atributos y métodos, y los cinco tipos de relación entre clases: generalización, composición, agregación, asociación y dependencia">
  <style>.t11{font:700 12px system-ui,sans-serif;fill:#fff}.m11{font:10.5px monospace;fill:#123}.l11{font:11px system-ui,sans-serif;fill:#444}.h11{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h11">Diagrama de Clases UML: caja de 3 compartimentos + 5 relaciones</text>
  <rect x="40" y="36" width="170" height="100" fill="#fff" stroke="#0055a0" stroke-width="1.5"/>
  <rect x="40" y="36" width="170" height="24" fill="#0055a0"/><text x="125" y="52" text-anchor="middle" class="t11">Expediente</text>
  <line x1="40" y1="60" x2="210" y2="60" stroke="#0055a0"/>
  <text x="46" y="76" class="m11">- idExpediente</text>
  <text x="46" y="90" class="m11">- estado</text>
  <line x1="40" y1="98" x2="210" y2="98" stroke="#0055a0"/>
  <text x="46" y="114" class="m11">+ getEstado()</text>
  <text x="46" y="128" class="m11">+ calcularPlazo()</text>
  <text x="290" y="50" class="l11">— caja de 3 compartimentos:</text>
  <text x="290" y="66" class="l11">nombre / atributos / métodos</text>
  <text x="290" y="86" class="l11">- private  # protected</text>
  <text x="290" y="100" class="l11">~ package  + public</text>
  <line x1="40" y1="180" x2="100" y2="180" stroke="#0055a0" stroke-width="2"/><polygon points="100,180 88,175 88,185" fill="#fff" stroke="#0055a0"/>
  <text x="115" y="184" class="l11">Generalización (herencia) — flecha triangular hueca</text>
  <line x1="40" y1="206" x2="100" y2="206" stroke="#0055a0" stroke-width="2"/><polygon points="40,206 52,200 52,212" fill="#0055a0"/>
  <text x="115" y="210" class="l11">Composición — rombo relleno («todo-parte» fuerte)</text>
  <line x1="40" y1="232" x2="100" y2="232" stroke="#0055a0" stroke-width="2"/><polygon points="40,232 52,226 52,238" fill="#fff" stroke="#0055a0"/>
  <text x="115" y="236" class="l11">Agregación — rombo hueco («todo-parte» débil)</text>
  <line x1="40" y1="258" x2="100" y2="258" stroke="#0055a0" stroke-width="2"/>
  <text x="115" y="262" class="l11">Asociación — línea continua (colaboran, se conocen)</text>
  <line x1="40" y1="284" x2="100" y2="284" stroke="#0055a0" stroke-width="2" stroke-dasharray="4,3"/>
  <text x="115" y="288" class="l11">Dependencia — línea discontinua (uso puntual)</text>
  <text x="340" y="330" text-anchor="middle" style="font:700 12px system-ui;fill:#e89822">Composición ≠ Agregación: composición controla el ciclo de vida de la parte</text>
  <text x="670" y="368" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: OMG-UML25; FOWLER-UML]</text>
</svg>
```

---

## D12 · Familias de diagramas UML de comportamiento

**Sección**: §5.5-5.7 — Diagramas de comportamiento: casos de uso, interacción y estados/actividades
**Propósito**: Visión de conjunto de los tres bloques de diagramas de comportamiento más preguntados.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 320" role="img" aria-label="Las tres familias de diagramas UML de comportamiento: casos de uso para requisitos funcionales, diagramas de interacción (secuencia y comunicación) para colaboración temporal, y diagramas de máquina de estados y actividades para control de flujo">
  <style>.t12{font:700 12px system-ui,sans-serif;fill:#fff}.s12{font:10px system-ui,sans-serif;fill:#fff}.h12{font:700 13px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h12">Diagramas UML de comportamiento — 7 tipos, 3 grandes familias</text>
  <rect x="30" y="40" width="190" height="150" rx="8" fill="#0055a0"/>
  <text x="125" y="64" text-anchor="middle" class="t12">CASOS DE USO</text>
  <text x="125" y="86" text-anchor="middle" class="s12">Requisitos funcionales</text>
  <text x="125" y="102" text-anchor="middle" class="s12">Actor + elipse</text>
  <text x="125" y="118" text-anchor="middle" class="s12">«include» / «extend»</text>
  <text x="125" y="140" text-anchor="middle" class="s12">§5.5</text>
  <rect x="245" y="40" width="190" height="150" rx="8" fill="#2d8659"/>
  <text x="340" y="64" text-anchor="middle" class="t12">INTERACCIÓN</text>
  <text x="340" y="86" text-anchor="middle" class="s12">Secuencia (temporal)</text>
  <text x="340" y="102" text-anchor="middle" class="s12">Comunicación (espacial)</text>
  <text x="340" y="118" text-anchor="middle" class="s12">Mensajes entre objetos</text>
  <text x="340" y="140" text-anchor="middle" class="s12">§5.6</text>
  <rect x="460" y="40" width="190" height="150" rx="8" fill="#e89822"/>
  <text x="555" y="64" text-anchor="middle" class="t12">CONTROL DE FLUJO</text>
  <text x="555" y="86" text-anchor="middle" class="s12">Máquina de Estados</text>
  <text x="555" y="102" text-anchor="middle" class="s12">(ciclo de vida objeto)</text>
  <text x="555" y="118" text-anchor="middle" class="s12">Actividades (proceso)</text>
  <text x="555" y="140" text-anchor="middle" class="s12">§5.7</text>
  <text x="340" y="222" text-anchor="middle" style="font:700 12px system-ui;fill:#123">Faltan del recuento: Diagrama General de Interacción y Diagrama de Temporización</text>
  <text x="340" y="242" text-anchor="middle" style="font:11px system-ui;fill:#444">Total: 7 diagramas de comportamiento + 7 estructurales (D11) = 14 tipos UML 2.5</text>
  <text x="670" y="300" text-anchor="end" style="font:11px system-ui;fill:#666">[Fuente: OMG-UML25; UML-DIAG-TYPES]</text>
</svg>
```
