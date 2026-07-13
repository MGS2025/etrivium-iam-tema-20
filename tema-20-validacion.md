# Tema 20 — Checklist de Validación

> **Título oficial**: Diseño y programación orientada a objetos. Objetos, clases, herencia, métodos, sobrecarga. Ventajas e inconvenientes. Patrones de diseño y UML.
> **Versión**: v1.0 — Pendiente validación
> **Fecha**: 2026-07-13
> **Revisores**: María y Ana (eTrivium) · revisión técnica IAM (Jesús Cuadrado)
> **Instrucciones**: marcar cada ítem. Los cambios no se guardan en la web (imprimir o exportar a PDF si se desea fijarlos).

---

## 1. Cobertura del temario oficial

- [ ] **Objetos, clases, herencia, métodos, sobrecarga**: pilares POO, clases/objetos/ciclo de vida, atributos/constructores, visibilidad, herencia simple/múltiple, sobrecarga/sobrescritura, polimorfismo, jerarquías, acoplamiento — §1-2
- [ ] **Ventajas e inconvenientes**: reutilización, mantenibilidad, escalabilidad, aislamiento de errores frente a curva de aprendizaje, complejidad, sobrecarga en ejecución y riesgos de mal diseño — §3
- [ ] **Patrones de diseño**: concepto, catálogo GoF, anti-patrones, clasificación creacional/estructural/comportamiento — §4
- [ ] **UML**: origen del estándar OMG, bloques de construcción, diagramas estructurales (clases, objetos, despliegue) y de comportamiento (casos de uso, secuencia, comunicación, estados, actividades) — §5

## 2. Contenido teórico

- [ ] El nivel de profundidad es adecuado para C1 (¿hay que ampliar o recortar alguna sección, especialmente el bloque UML de §5?)
- [ ] Las definiciones de abstracción, encapsulamiento, herencia y polimorfismo, y la distinción sobrecarga/sobrescritura, son correctas y sin ambigüedad
- [ ] La decisión de usar **Java** en todos los ejemplos de código es adecuada (¿o se prefiere un lenguaje neutro / pseudocódigo, como en T18?)
- [ ] El catálogo GoF (23 = 5+7+11) está completo y correctamente clasificado
- [ ] La distinción entre el Diagrama de Clases UML (§5.3) y el modelo Entidad-Relación del Tema 16 (nota de diferenciación explícita) es clara y no induce a confusión
- [ ] La frontera con el Tema 18 (lenguajes de programación, procedimientos/funciones genéricos), el Tema 19 (SQL, disparadores) y el Tema 21 (Java EE) está bien trazada
- [ ] Los ejemplos Ayto Madrid (expedientes, licencias, notificaciones) son verosímiles

## 3. Fuentes

- [ ] Todas las afirmaciones técnicas están respaldadas por fuente Tier 1
- [ ] Las referencias inline se corresponden con `tema-20-fuentes.md`
- [ ] Atribuciones históricas correctas (Simula 67 1967, Smalltalk años 70, C++ 1983, Java 1995; GoF 1994; UML 1997/2005/2017)

## 4. Test (60 preguntas)

- [ ] Cada pregunta tiene una sola respuesta correcta e inequívoca
- [ ] Los distractores (A/B/C) son plausibles
- [ ] La distribución de la opción correcta entre A/B/C está equilibrada (20/20/20)
- [ ] Las explicaciones y referencias de cada respuesta son correctas
- [ ] La pregunta 15-19 (sobrecarga vs sobrescritura, ligadura estática vs dinámica) no induce a confusión — es el punto más delicado del tema

## 5. Casos prácticos (3)

- [ ] Realistas y propios del Ayuntamiento (licencias de obra, terrazas, notificaciones a ciudadanos)
- [ ] El código Java de las soluciones compila conceptualmente (sintaxis correcta)
- [ ] La puntuación de cada caso suma 10 puntos
- [ ] El Caso 3 (UML) es coherente con la notación fijada en §5.3

## 6. Diagramas (12 SVG)

- [ ] Cada diagrama es correcto y legible (también impreso en B/N)
- [ ] Accesibilidad: todos tienen `role="img"` y `aria-label`
- [ ] Sin desbordes de texto ni colisiones de estilo entre SVG (clases con sufijo único, QA de caja contenedora)
- [ ] D6 (herencia simple/múltiple) y D11 (notación de relaciones UML) son especialmente sensibles a errores de precisión — revisar con atención

## 7. Referencias cruzadas a otros temas

- [ ] Validadas contra BOAM 10.032 (T7, T16, T18, T19, T21, T22, T25)
- [ ] Ninguna referencia cruzada cita un enunciado de tema incorrecto

## 8. Calidad editorial

- [ ] Ortografía verificada (tildes y ñ) — sin diacríticos perdidos
- [ ] Coherencia de versión (v1.0) en title, badges, banner y footer del `index.html`
- [ ] El `index.html` abre, navega entre las 8 pestañas y el motor de test funciona
- [ ] Las listas anidadas del Contenido se muestran con sus niveles (sin aplanar)
- [ ] Los bloques de código Java se muestran correctamente formateados, sin markdown crudo

---

## Observaciones abiertas

_(Espacio para anotaciones de María, Ana y la revisión IAM.)_
