# Plantilla: ficha de encargo

> La ficha de encargo es la herramienta central del método. Define **una** tarea atómica: su
> alcance, sus fronteras y su criterio de aceptación. Sin ella, el ejecutor adivina y el
> revisor no tiene contra qué contrastar.
>
> Regla dura que acompaña a toda ficha: **el ejecutor devuelve contenido, no persiste
> archivos.** Consolidar es trabajo del director o del humano.
>
> Base conceptual: [`docs/05-reglas-de-atomicidad.md`](../docs/05-reglas-de-atomicidad.md).
> Ejemplos reales y trabajados: [`work-orders/`](../work-orders/).

---

## Ficha N — [Título de la tarea]

- **Propósito:** el "para qué" en una línea. Si no entra en una línea, la tarea es demasiado
  amplia y hay que dividirla.

- **Extensión objetivo:** rango concreto y verificable (por ejemplo, 450-600 palabras). Un
  número permite que el revisor lo **cuente** en vez de estimarlo a ojo.

- **Preguntas que debe responder:** las preguntas guían el contenido sin escribirlo.
  1. ...
  2. ...
  3. ...

- **Debe contener:** checklist **cerrado** de puntos verificables. No es prosa, es una lista
  que el revisor recorre punto por punto. Si un punto no se puede verificar leyendo la
  entrega, no va acá.
  - [ ] ...
  - [ ] ...

- **NO debe tocar:** el campo de mayor apalancamiento de toda la ficha. Enumera
  explícitamente qué queda fuera, aunque parezca relacionado. Es lo que evita que dos tareas
  se pisen, y es también el contrato contra el cual la capa de Detección compara la salida.
  - ...
  - ...

- **Ancla / ejemplo real:** el caso concreto que la entrega debe citar. **Entregalo ya
  verificado.** Darle hechos comprobados al ejecutor antes de escribir reduce la fabricación
  mucho más que atraparla después.

- **Errores a evitar:** lista negativa de anti-patrones conocidos para esta clase de tarea.

- **Términos clave:** mini-glosario, para que el vocabulario no se desalinee entre tareas
  hechas por distintos ejecutores o en distintas sesiones.

- **Insumos:** qué se le entrega al ejecutor para empezar. Documentos, contexto, ejemplos.

- **Forma de salida:** formato, extensión, tono. Y si aplica, la regla dura de que devuelve
  contenido en la respuesta, sin escribir archivos.

- **Criterio de listo:** la vara exacta con la que el revisor la evalúa. Se escribe desde el
  lector: "al terminar, alguien puede hacer X sin volver a consultar".

---

## Señales de que la ficha está mal escrita

- **El "NO debe tocar" es larguísimo.** Señal de que la tarea es demasiado amplia: dividila.
- **La ficha redacta en vez de acotar.** Si le escribís el contenido al ejecutor, trasladaste
  el trabajo al revisor.
- **El "Debe contener" es una intención difusa** en vez de una lista cerrada. Entonces la
  omisión de un elemento obligatorio no salta en la revisión, que es el modo de fallo más
  difícil de ver.
- **No hay número en la extensión.** Sin número, el control se vuelve una opinión.
