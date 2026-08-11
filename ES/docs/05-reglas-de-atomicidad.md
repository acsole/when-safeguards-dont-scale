## 5. Reglas de atomicidad

Una tarea atómica es indivisible: es una sola pieza de trabajo con fronteras claras, sin dependencias ocultas con otras tareas, que puede completarse de forma independiente. En el contexto de nuestro método, la atomicidad es el antídoto contra la confusión, la duplicación de esfuerzo y los malentendidos.

Cuando un ejecutor recibe una tarea que en realidad contiene dos (redactar un módulo Y revisar otro; diseñar una pantalla Y escribir la documentación), surge ambigüedad: ¿qué hago primero? ¿Hasta dónde va mi responsabilidad? ¿Qué hace el revisor si parte de mi entrega invade el territorio de otra persona? Estas preguntas no deben existir.

La herramienta que garantiza atomicidad es la **ficha de encargo**: un documento breve, estructurado y explícito que define el **alcance** de la tarea—qué va dentro y, más importante aún, qué queda fuera. Es la frontera hecha tangible.

### ¿Cómo se evita que dos tareas se pisen?

Mediante el campo **"NO debe tocar"** de la ficha. Este campo es el de mayor apalancamiento: enumera explícitamente las áreas, decisiones, archivos o ámbitos que esta tarea NO toca, aunque parezcan relacionados. Si la frontera está escrita en negro sobre blanco, no hay lugar a interpretación.

Ejemplo: si la Tarea A es "revisar un documento de compliance", el "NO debe tocar" dice: *"No cambiar la estructura legal subyacente, no ampliar el alcance a nuevas jurisdicciones, no modificar términos contractuales ya aprobados."* Así, aunque alguien lea el documento y piense "esto podría mejorarse aquí", sabe que eso está fuera de alcance.

### Plantilla de la ficha de encargo

| Campo | Función |
|-------|---------|
| **Propósito** | Resumen de una línea del objetivo de la tarea. Ejemplo: *"Revisar la sección de compliance del contrato."* |
| **Debe contener** | Checklist cerrado de puntos que el ejecutor debe incluir en su entrega. No es prosa; son requisitos verificables. Ejemplo: validación de cláusulas, verificación de fechas, contraste con normas vigentes. |
| **NO debe tocar** | Fronteras explícitas. Qué NO entra en esta tarea, aunque suene relacionado. Ejemplo: *No cambiar términos contractuales; no expandir a nuevas jurisdicciones; no revisar anexos no especificados.* |
| **Insumos** | Qué se le entrega al ejecutor para que empiece: documentos previos, contexto, guías, ejemplos. |
| **Forma de salida** | Formato, extensión, tono. Ejemplo: *"Markdown, punto por punto, registro de hallazgos."* |
| **Criterio de listo** | La vara con que el revisor lo evalúa. Ejemplo: *"Al terminar, se pueden tomar decisiones sobre cada hallazgo sin volver a consultar."* |

### Un ejemplo en contraste

**Tarea difusa (mala):** *"Mejorar la sección de metodología del proyecto."*
Problemas: ¿qué parte? ¿hasta qué nivel de detalle? ¿Cambio los módulos existentes? ¿Agrego nuevos? El ejecutor adivinará.

**Tarea atómica (buena):** *"Redactar Módulo 5 sobre atomicidad: definición, plantilla de ficha en tabla, énfasis en 'NO debe tocar', ejemplo buena vs. mala división. No modificar módulos 1–4. Markdown, 450–600 palabras. Criterio: lector puede redactar su propia ficha."*
Beneficio: el ejecutor sabe exactamente qué hacer, dónde termina su trabajo, y el revisor sabe cómo validarlo.

### Prueba viviente

Este método se construyó con fichas de encargo: una por módulo. Cada redactor recibió una ficha acotada que garantizaba que los nueve módulos se encajaban sin solapes ni huecos.

Una advertencia para cerrar: una ficha mal escrita *redacta* el contenido en vez de *acotarlo* —y eso traslada el trabajo del redactor al revisor. Cuando diseñes tu próxima tarea, escribe su ficha primero. Si notas que el "NO debe tocar" es demasiado largo, es señal de que la tarea es demasiado amplia: divide.
