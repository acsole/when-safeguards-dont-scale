# Incident log

Este método se construyó usándose a sí mismo. Cada módulo de su documentación lo redactó un
modelo económico contra una ficha de encargo, lo auditó un revisor independiente, y recién
después lo aprobó y consolidó la autoridad humana. Los archivos de esta carpeta registran
**cada fallo que ese pipeline atrapó durante el proceso**, con su severidad, su corrección y
la lección que dejó.

## Por qué existe

Un método que solo publica sus aciertos no da con qué juzgarlo. Estos registros existen por
dos razones concretas:

1. **Demuestran que la red de detección funciona.** No como afirmación abstracta, sino con
   casos fechados y trazables al commit que los corrigió.
2. **Calibran al propio revisor.** Cada entrada describe un modo de fallo, y los modos de
   fallo resultaron ser recurrentes y predecibles, no accidentes sueltos.

Lo que hace distinta a esta bitácora es que **incluye los fallos de las capas superiores del
sistema, no solo los del redactor barato**. El revisor cazó fabricaciones que el director ya
había leído y dado por buenas. Y en otra ocasión el director cazó una falsa alarma que el
revisor había levantado estimando en vez de medir. Ninguna capa resultó infalible, y eso es
exactamente el argumento a favor de que existan varias.

## Qué hay acá

| Registro | Qué documenta |
|---|---|
| [`metodo-de-trabajo.md`](metodo-de-trabajo.md) | Ocho sesiones de incidencias durante la redacción del documento canónico (M1-M9), más el cierre que las resume |
| Bitácora de la guía de adopción | Vive todavía dentro de [`install/guia-instalacion.md`](../install/guia-instalacion.md), en su Anexo A. Se moverá acá cuando la guía esté completa |

## Los modos de fallo catalogados hasta hoy

Del redactor: **fabricación** (inventar cifras, citas o mecanismos para sonar verificable),
**redundancia** (repetir un concepto hasta romper un límite duro de extensión), **omisión**
de un elemento obligatorio de la ficha, **embellecimiento** de un hecho real, y **fuga de
nombre propio interno** a un documento pensado para lectores externos.

Del revisor: **falso positivo** por estimar a ojo en vez de contar.

Del director: **indulgencia** con el modo de fallo que él mismo no detecta.

## El hallazgo más útil

La entrada del Módulo 6 registra que ese módulo tuvo **cero fabricación**, a diferencia de
los anteriores. La única diferencia fue el insumo: al redactor se le entregaron los ejemplos
reales ya verificados antes de escribir. Restringir la superficie de generación con hechos
concretos reduce la invención mucho más que atraparla después.

Dicho de otro modo: **la detección es la última red, no la primera.**
