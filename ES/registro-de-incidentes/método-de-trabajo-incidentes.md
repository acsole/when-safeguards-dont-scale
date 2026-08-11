## Anexo A — Bitácora de dogfooding (registro de incidencias)

> **Qué es.** Este método se construyó usándose a sí mismo (*dogfooding*): cada módulo
> lo redactó un ejecutor (Haiku) y lo auditó un revisor independiente (quality-guardian,
> Sonnet) antes de la aprobación humana (Opus + Human-in-the-Loop). Esta bitácora registra, con
> transparencia total, **cada incidencia capturada en la revisión**: qué se detectó, a
> quién, cuándo, por qué importaba y cómo se corrigió. Su valor es doble: demuestra que la
> red de detección funciona, y sirve para **calibrar al propio revisor** y volverlo más
> atento con cada iteración — independientemente de la versión de modelo que lo encarne.
>
> Columnas: **#** · **Fecha** · **Módulo** · **Ejecutor** (corregido) · **Revisor** ·
> **Hallazgo** · **Severidad** · **Corrección aplicada** · **Por qué importaba**.

### Módulo 1 — Visión y propósito · 2026-06-22 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 1.1 | Faltaba el **ancla a proyectos reales** del autor | 🔴 Bloqueante | Se añadió la frase "no es teoría: nació de aplicarlo en proyectos reales propios" | Sin anclaje, el módulo sonaba a teoría; el campo era obligatorio en la ficha |
| 1.2 | Los **tres pilares** venían con micro-desarrollo (invadían M2/M3) | 🟡 Mejora | Se recortaron a solo sus nombres | Mantener fronteras entre módulos; evitar duplicación |
| 1.3 | La **tesis** estaba diluida en un párrafo largo | 🟡 Mejora | Se aisló en 1–2 frases destacadas | Legibilidad; la tesis debe ser identificable de inmediato |
| 1.4 | Usó "autoridad final" en vez de "**autoridad humana**" | ⚪ Menor | Se unificó el término | Coherencia terminológica entre módulos |

**Lección / calibración:** el redactor tiende a **sobre-explicar** y a **omitir el anclaje concreto**. Las fichas reforzaron desde entonces el campo "Ancla" y las fronteras "NO debe tocar".

### Módulo 2 — Roles y responsabilidades · 2026-06-23 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 2.1 | Faltaba explicitar el "por qué" de **fortaleza ↔ costo** por rol | 🟡 Mejora | Se añadió el razonamiento costo-beneficio de cada asignación | El módulo debía justificar la asignación, no solo enunciarla |
| 2.2 | El principio de severidad se repetía **tres veces** | 🟡 Mejora | Se consolidó en una sola formulación + cierre breve | Economía; la redundancia diluye el mensaje |
| 2.3 | "¿Quién decide en última instancia?" sin contundencia propia | ⚪ Menor | Se enunció explícito en la tabla ("Decide en última instancia") | Las cuatro preguntas de la ficha debían quedar con igual peso |
| 2.4 | **5 subtítulos** para ~480 palabras → fragmentación | ⚪ Menor | Se redujeron a 2 | Estructura compacta acorde a la ficha |

**Incidente de calibración notable:** durante esta revisión, el revisor **corrigió al director**. Opus estimó "más de 650 palabras, se pasó del rango"; el conteo real del revisor fue **483 palabras, dentro de rango**. Aprendizaje: las estimaciones cuantitativas se verifican con conteo, no a ojo — y la capa de revisión aplica **también al director**, no solo al ejecutor.

**Lección / calibración:** el redactor tiende a la **redundancia estructural** (repetir el mismo concepto en varias secciones) y a **sobre-subtitular**. El revisor demostró independencia de juicio al contradecir tanto al ejecutor como al director con evidencia.

### Módulo 5 — Reglas de atomicidad · 2026-06-23 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

Primera devolución del revisor — **dos bloqueantes**:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 5.1 | **Extensión** ~640–660 palabras (techo: 600) | 🔴 Bloqueante | Recorte a 542 palabras | Requisito numérico explícito y verificable de la ficha |
| 5.2 | **Redundancia:** el propio M5 usado como autoejemplo 3 veces (causa raíz del exceso) | 🔴 Bloqueante | Se dejó un solo caso; ejemplos variados (compliance / contraste / fichas del doc) | La repetición infla extensión y diluye el mensaje |
| 5.3 | Término "alcance" solo incidental | ⚪ Menor | Incorporado deliberadamente en la definición de la ficha | Coherencia con los términos clave |
| 5.4 | "Ficha que redacta en vez de acotar" no nombrado explícitamente | ⚪ Menor (opcional) | El director (Opus) lo añadió al consolidar | Completitud frente a la lista "errores a evitar" de la ficha |

**Regla de escalado activada por el Human-in-the-Loop (severity-proportionate-assurance en vivo):** se acordó que si la **re-auditoría** de esta corrección volvía con algún 🔴 bloqueante, la siguiente iteración escalaría a **ejecutor Sonnet 4.6 + auditor Opus** (subir un nivel ejecutor y revisor). **Re-auditoría: LISTO, sin bloqueantes → la regla quedó *armada*, no consumida.** Haiku se mantiene como redactor.

**Lección / calibración:** la redundancia del redactor no es solo estética: **infla la extensión hasta romper un requisito duro**. Antídoto eficaz: pedir ejemplos *variados* en vez de autorreferencias. Se confirmó (otra vez) que la extensión se **cuenta**, no se estima a ojo: el director subestimó el exceso, el revisor lo midió.

### Módulo 3 — El ciclo de producción · 2026-06-23 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

Primera devolución del revisor — **dos bloqueantes**:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 3.1 | Usó el **nombre propio interno "Andrés"** 6 veces (prosa + diagrama) | 🔴 Bloqueante | Reemplazado por "la autoridad humana" en todo | El documento es externo-primero; un tercero no sabe quién es Andrés. Rompía la convención de M1/M2 |
| 3.2 | **Fabricación:** "algunos módulos llegaron a tres rondas" (falso; máximo real: 2) | 🔴 Bloqueante | Reemplazado por "más de una ronda de corrección" (veraz, genérico) | Dato inventado presentado como hecho — y en el módulo que predica "verificar, no confiar" |
| 3.3 | El diagrama no anclaba visualmente el checkpoint de automatización | 🟡 Mejora | El director añadió la línea `[↻ Checkpoint…]` al diagrama | La ficha pedía que el lector pueda "señalar dónde se evalúa automatizar" |
| 3.4 | Singular/plural inconsistente en "Prueba viva" | ⚪ Menor | Unificado a singular | Coherencia de registro |

**Decisión de escalado (severity-proportionate):** por tener bloqueantes, se evaluó disparar la regla (ejecutor Sonnet + auditor Opus). La autoridad humana resolvió, fiel a la letra de la regla, que **esta era la primera devolución** de M3 → Haiku tenía derecho a una ronda de corrección; el escalado se reserva para una **re-auditoría** que reincida en bloqueantes. **Re-auditoría: APTO, sin bloqueantes → escalado NO consumido.**

**Decisión de redacción del director (honestidad calibrada):** el revisor sugirió, opcionalmente, afinar "más de una ronda" → "hasta dos rondas". Se **rechazó**: "hasta dos" es verdad hoy, pero caducaría si un módulo futuro llega a tres rondas. Se prefirió la formulación robusta al futuro. La verdad que no se puede volver mentira mañana vale más que la precisión de hoy.

**Lección / calibración:** se confirmó la **fabricación** como modo de fallo recurrente del redactor (ya visto en otros frentes del proyecto): inventa cifras concretas para "sonar" verificable. El revisor solo pudo cazarla porque se le entregó la **verdad-base** (conteo real de rondas) — aprendizaje clave: *el revisor necesita los hechos de referencia para detectar fabricaciones, no basta con su criterio.* Esto refuerza la práctica de darle al guardián los datos verificables del proyecto en cada auditoría factual.

### Módulo 4 — Memoria persistente · 2026-06-23 · PRIMERA ACTIVACIÓN DE LA REGLA DE ESCALADO

Este módulo es la evidencia más completa del protocolo, porque atravesó las **tres etapas** de la escalera de aseguramiento.

**Ronda 1 — Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)**

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 4.1 | **Fabricación:** regla condicional inventada de carga de memoria por tipo de tarea ("si es codificación → project+feedback; si es diseño → +user") | 🔴 Bloqueante | Haiku reformuló la sección | Mecanismo específico presentado como real sin sustento |

**Ronda 2 (re-auditoría) — Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)**

| # | Hallazgo | Severidad | Resultado |
|---|----------|-----------|-----------|
| 4.2 | **Reincidencia:** la fabricación volvió en forma más sutil ("según la naturaleza de la tarea, recupera los archivos relevantes") — el mismo mecanismo de selección, solo que velado | 🔴 Bloqueante | **Re-auditoría con bloqueante → DISPARA la regla de escalado** |

**Ronda 3 (escalada) — Ejecutor: Sonnet 4.6 · Revisor: Opus (director)**

Conforme a la regla de aseguramiento proporcional a la severidad, al reincidir el bloqueante en la re-auditoría, la iteración subió un nivel: el ejecutor pasó de Haiku a **Sonnet 4.6**, y el revisor de quality-guardian a **Opus** (preservando revisor > ejecutor). Sonnet no solo eliminó la fabricación: la **negó explícitamente** en el texto ("No existe un mecanismo automático que filtre o seleccione archivos según el tipo de tarea... la lectura de lo relevante es un paso deliberado"). Auditoría de Opus: **APTO, sin bloqueantes**. Resuelto en una sola pasada.

**Incidente de calibración del director (importante):** en las dos rondas con Haiku, el director (Opus) **subestimó la fabricación**: en su pre-lectura la calificó de "ejemplo genérico aceptable" y luego de "formulación veraz". En ambos casos el **revisor independiente** (el guardián) detectó lo que el director pasó por alto. Es la prueba más fuerte de por qué el revisor debe ser independiente del director, y de por qué la autoridad de aprobación final no recae en quien dirige.

**Lección / calibración — el protocolo funcionó como fue diseñado:**
- La **escalera de severidad** no es teoría: se activó por evidencia real (reincidencia de bloqueante) y resolvió el problema que el nivel económico no pudo.
- Subir el ejecutor (Haiku→Sonnet) Y el revisor (guardián→Opus) **al mismo tiempo** mantuvo la independencia revisor > ejecutor.
- Un modelo más capaz no solo "lo hizo bien": convirtió el punto débil en una **aclaración explícita** — señal de que la capacidad extra se invierte mejor en lo difícil (coherente con M2).
- Confirmación incómoda pero valiosa: **el director es falible y puede ser indulgente con el modo de fallo que él mismo no detecta**; la defensa no es "esforzarse más", sino la **estructura** (revisor independiente + escalado por evidencia).

### Módulo 9 — Trazabilidad y reversibilidad · 2026-06-23 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

Primera devolución del revisor — **un bloqueante**:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 9.1 | **Omisión de elemento obligatorio:** faltaba la frase que distingue memoria (M4) de versionado/git, con remisión | 🔴 Bloqueante | Se añadió la sección "Distinción crítica: versionado vs. memoria" con remisión a M4 | Era un punto explícito de "Debe contener" en la ficha; sin él, el lector confunde dos mecanismos distintos |
| 9.2 | Concepto commit/diff explicado 3 veces (tabla + sección + flujo) | 🟡 Mejora | Recortada la redundancia → liberó espacio para 9.1 sin pasar de 600 | Economía; y resolver una mejora habilitó resolver el bloqueante |
| 9.3 | Typo "decididen" → "deciden" | ⚪ Menor | Corregido | Pulcritud |

**Re-auditoría: APTO** (580 palabras, bloqueante resuelto, sin nuevos hallazgos). Escalado NO disparado: Haiku se corrigió en una ronda.

**Nota de calibración (contraste con M4):** aquí el director (Opus) **sí pre-identificó el bloqueante** —la distinción memoria↔git faltante— antes de la auditoría del guardián. El aprendizaje de M4 (no subestimar) se aplicó. La calibración del director también mejora con la experiencia, no solo la del redactor o el revisor.

**Lección / calibración:** apareció un modo de fallo **distinto** de la fabricación: la **omisión de un elemento obligatorio** de la ficha. El redactor desarrolló bien lo que sí incluyó (git), pero dejó fuera un requisito explícito. Antídoto: la ficha funciona como *checklist* verificable y el revisor la recorre punto por punto — por eso el campo "Debe contener" debe ser una lista cerrada, no una intención difusa.

### Módulo 6 — Industrialización · 2026-06-23 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Sin bloqueantes** (el módulo más limpio hasta aquí). Una sola ronda, ajustes cosméticos aplicados por el director al consolidar:

| # | Hallazgo | Severidad | Corrección aplicada |
|---|----------|-----------|---------------------|
| 6.1 | Género inconsistente de "skill" ("una skill" / "lo activa" / "los skills") | 🟡 Mejora | Unificado a femenino ("una skill" / "las skills" / "la activa") |
| 6.2 | Tabla de decisión con fila híbrida y una fila de subagente duplicada | ⚪ Menor | Simplificada a 3 filas núcleo (una por herramienta); la combinación quedó solo en la sección de texto |
| 6.3 | Giro coloquial "no hay debate" | ⚪ Menor | Reformulado a "detiene la acción de forma automática, sin intervención humana" |

**Hallazgo metodológico clave (registrado por pedido del Human-in-the-Loop):** M6 tuvo **cero fabricación**, a diferencia de M3/M4. La diferencia fue el insumo: a Haiku se le entregaron los **tres ejemplos reales de ASLAN ya verificados** (preámbulo→subagente, convenciones→skill, grep→hook). **Restringir la superficie de generación con hechos concretos reduce drásticamente la invención.** Corolario práctico para el método: cuando un módulo dependa de datos verificables, dárselos al redactor *antes* —no esperar a que el revisor cace lo inventado después— es más barato y más seguro. La detección es la última red, no la primera.

### Módulo 7 — Casos de uso · 2026-06-23 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet) · Verificación final: Opus

Este módulo dejó dos lecciones distintas: una sobre el redactor y otra, inédita, **sobre el revisor**.

**Ronda 1 — tres bloqueantes por fabricación:**

| # | Hallazgo | Severidad | Corrección aplicada |
|---|----------|-----------|---------------------|
| 7.1 | **Fabricación irónica:** al ejemplificar "qué cazó el revisor como fabricación", inventó una cita que nunca ocurrió (*"según análisis de X"*) en lugar de los casos reales | 🔴 Bloqueante | Reemplazada por las fabricaciones reales (el "tres rondas" de M3; la regla de memoria de M4) |
| 7.2 | Embellecimiento en el caso ASLAN: "bajo carga simultánea" (no ocurrió) | 🔴 Bloqueante | Eliminado |
| 7.3 | Embellecimiento: "acumulándose" (no ocurrió) | 🔴 Bloqueante | Eliminado |

El dato más jugoso: **el módulo de "casos reales" fabricó dentro de su propio ejemplo de qué es una fabricación.** Prueba contundente de que el modo de fallo "fabricación" es persistente y de por qué la detección independiente es imprescindible.

**Ronda 2 (re-auditoría) — el revisor se equivocó, y el director lo verificó:**

El guardián confirmó que las tres fabricaciones quedaron resueltas, pero levantó un **nuevo bloqueante de extensión**, estimando "~700–750 palabras" — **a ojo, sin contar**. El director (Opus), en vez de aceptarlo y disparar el escalado, aplicó *"verificar, no confiar"* **hacia el propio revisor**: contó objetivamente el cuerpo del módulo → **518 palabras**, dentro del rango. El bloqueante era un **falso positivo**.

**Lecciones / calibración:**
- **El revisor también es falible** — y, notablemente, falló en la misma regla que él nos había enseñado en M2/M5: *la extensión se cuenta, no se estima a ojo.*
- **"Verificar, no confiar" aplica en todas las direcciones**, incluida hacia arriba (del director al revisor), no solo hacia abajo (hacia el redactor).
- **Verificar el disparador antes de actuar evitó una escalada inútil:** la regla de escalado NO se activó, porque su condición (un bloqueante *real* en la re-auditoría) no se cumplía. Escalar sobre un falso positivo habría gastado capacidad sin motivo.
- Corolario para el protocolo: ninguna capa —ni redactor, ni revisor, ni director— es infalible; la robustez no viene de confiar en un rol, sino de que **cada afirmación verificable se verifique con la herramienta adecuada**, venga de quien venga.

### Módulo 8 — Límites y cuándo no usar el método · 2026-06-23 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Una ronda, un bloqueante:**

| # | Hallazgo | Severidad | Corrección aplicada |
|---|----------|-----------|---------------------|
| 8.1 | Nombre propio interno "Andrés" usado 2 veces (REINCIDENCIA del fallo de M3) | 🔴 Bloqueante | Reemplazado por "el humano" / "la autoridad humana" |

**Nota de proceso (verificación proporcional):** por tratarse de un reemplazo mecánico de dos palabras, el director NO disparó un re-auditoría completa del guardián; verificó objetivamente con una búsqueda (`grep`) que no quedara ninguna mención del nombre propio en los cuerpos de módulo. Es una aplicación del propio principio de aseguramiento proporcional a la severidad (Módulo 2): el rigor de la verificación se dimensiona según el riesgo del cambio.

**Lección / calibración:** el modo de fallo "nombre propio interno" REINCIDIÓ (ya había aparecido en M3). Un fallo recurrente y predecible es el mejor candidato a **industrializarse** (Módulo 6): podría convertirse en un hook que detecte nombres propios internos en los borradores antes de la revisión humana — un ejemplo más de cómo el dogfooding alimenta la mejora del propio protocolo.

---

---

## Cierre — Estado del documento

Los **9 módulos están consolidados** y el documento está completo. Esta bitácora registra **8 sesiones de incidencias** (M1–M9; M5 con dos rondas, M3/M4/M7 también) que cubren un repertorio de modos de fallo del redactor —**redundancia, fabricación, omisión, embellecimiento y nombre propio interno**— más un caso de **falibilidad del revisor** (falso positivo de extensión en M7) y dos de **falibilidad del director** (indulgencia en M4). En todos los casos la estructura —no la confianza en un rol— contuvo el error. Ese es, en una frase, el método.

**Complementos.** Para ver cómo el método se mapea a distintas industrias (marketing, inmobiliaria, IT) y una plantilla para adaptarlo a cualquier vertical, ver [`docs/10-aplicabilidad-a-verticales.md`](../docs/10-aplicabilidad-a-verticales.md). El blueprint de tareas atómicas que produjo este documento está en [`work-orders/metodo-de-trabajo.md`](../work-orders/metodo-de-trabajo.md).
