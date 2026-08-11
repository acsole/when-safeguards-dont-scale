## 3. El ciclo de producción

Una tarea en el método de trabajo con IA no aparece lista de la nada. Atraviesa un ciclo operativo deliberado donde cada rol interviene en orden, con puntos de validación claros y oportunidades para rechazar, rehacer y mejorar. Este ciclo garantiza que nada se ejecuta sin haber sido pensado, revisado y aprobado por la autoridad humana.

### El flujo operativo

El ciclo comienza cuando la autoridad humana y el Director **conversan para definir un objetivo** — no una tarea todavía, sino un esqueleto: qué se quiere lograr, por qué, y en qué contexto. A partir de ese esqueleto, el Director divide el trabajo en **tareas atómicas** (descritas en fichas de encargo, como se detalla en el Módulo 5). Cada ficha es una unidad indivisible, clara, autónoma.

Luego, el **Redactor ejecuta**: toma una ficha, consulta sus referencias, produce la salida (código, prosa, diseño, análisis). Cuando termina, entrega un reporte del trabajo hecho.

Aquí entra el **Revisor**: audita la salida contra criterios objetivos (¿respeta el esquema? ¿cumple la ficha? ¿hay incoherencias con lo ya escrito?). Si la revisión pasa, avanza. **Si falla, rechaza con feedback concreto y la ficha vuelve al Redactor**.

```
Autoridad humana          Director                 Redactor              Revisor
     |                       |                        |                    |
     +-- Define esqueleto ---+                        |                    |
                             |-- Crea fichas -------->|                    |
                             |                   Ejecuta                   |
                             |                        +--- Audita --->|    |
                             |                        |<-- Rechaza ---+    |
                             |                        +--- Reescribe -->|  |
                             |                        |<-- Aprueba ----+   |
                             |<-- Entrega resultado --|
     |<-- Verifica, no confía --|
     |-- Aprueba finalmente ----|

   [↻ Checkpoint de automatización: se evalúa en CADA vuelta del ciclo]
```

### El principio "verificar, no confiar"

Un reporte del Redactor no es suficiente. El **Director verifica de forma independiente** antes de dar algo por bueno: relée la salida, consulta las referencias, corre comprobaciones objetivas cuando aplica (tests, cambios reales en el código, coherencia contra documentación). Solo después de esta verificación personal, el Director puede comunicarle a la autoridad humana: "esto está listo".

La autoridad humana, como instancia final, **aprueba** o propone cambios. Su aprobación es el permiso para consolidar e integrar el resultado al proyecto.

### El checkpoint de automatización

En cada ciclo, mientras ocurre la entrega y revisión, alguien pregunta: **¿esta interacción que estamos repitiendo conviene automatizarla?** Por ejemplo, si el Revisor debe auditar el mismo tipo de cosa una y otra vez con los mismos criterios, quizá una herramienta automatizada podría hacerlo. Este checkpoint es recurrente; no tiene criterios fijos (eso es tema del Módulo 6), pero su presencia es constante.

### La ruta de rechazo y reintento

Si la revisión falla, no es fracaso: es corrección. El Revisor retorna la ficha con feedback puntual. El Redactor reescribe, y el ciclo completo se itera hasta que la salida pase revisión. Luego, la autoridad humana aprueba.

### Prueba viva

Este documento mismo — el "Método de trabajo con IA" — está siendo producido con este ciclo. El esqueleto fue definido por la autoridad humana y el Director. Cada módulo es una ficha de encargo. El Redactor produce texto. El Revisor audita, rechaza piezas cuando es necesario, y pide reescrituras. Solo cuando pasa la revisión, la autoridad humana aprueba la consolidación. Algunos módulos requirieron más de una ronda de corrección antes de aprobarse.

El ciclo no es una fantasía teórica: es vivo, iterativo, y funciona.
