# Fichas de encargo — Safeguards Case Study

> Documento de scoping (en español, interno). El documento final (`safeguards-case-study.md`) es **100% en inglés**.
> Cada ficha define una sección atómica. La frontera **NO debe tocar** es lo que evita que los módulos se pisen.
> Pipeline por sección: Haiku redacta (devuelve contenido, no escribe archivos) → quality-guardian (Sonnet) audita → corrección → Opus + Andrés aprueban → consolidar + commit.

## Eje intelectual transversal
El valor diferencial es el **salto de escala**: de "1 usuario / 1 proyecto" → entornos productivos con miles/millones de vidas y adversarios orquestando decenas de miles de agentes. La honestidad calibrada (decir qué NO se afirma) es en sí misma un rasgo Safeguards.

## Insumos comunes (rutas relativas desde `calmkit-brain/`, salvo nota)
- `calmkit-brain/CLAUDE.md` — deny-by-default + restricciones innegociables (human-in-the-loop).
- `calmkit-brain/00-método-de-trabajo/fichas-de-encargo.md` — scoping de autonomía.
- `calmkit-brain/00-método-de-trabajo/metodo-de-trabajo.md` — documento canónico del método.
- `~/.claude/hooks/aslan-enforcer.js` — guardrail automatizado (bloqueó ediciones reales).
- `~/.claude/hooks/aslan-telemetry.js` — telemetría/auditoría.
- Historial git de `calmkit-brain` (trazabilidad real).
- `../../ASLAN-ARC/` — dashboard con principio de honestidad de datos.

## Forma de salida (todas)
Markdown en inglés, sección autocontenida, tono profesional y sobrio (no marketing). Diagramas como SVG embebible cuando la ficha lo indique.

## Orden de redacción
**S0 → S1 → S3 → S4 → S2 → S5 → S6 → S7**, con **re-paso de S0 tras S5** (el pitch es sección viva: se blinda cuando el cuerpo ya existe).
**S9** (Incident Log) es sección VIVA: se nutre en cada sesión, a medida que el propio pipeline atrapa fallos durante la redacción. No se "redacta de una"; se acumula.

---

## S0 — Elevator Pitch
- **Propósito:** Enganchar a un lector de Safeguards en menos de 30 segundos.
- **Debe contener:** Tesis en 1 frase; 3-4 frases de respaldo; el gancho de escala (mono-usuario → adversarial poblacional).
- **NO debe tocar:** Detalle técnico, rutas, diagramas, tablas.
- **Insumos:** Visión general del sistema (S1) + eje de escala.
- **Forma de salida:** ~6-8 líneas de prosa en inglés.
- **Criterio de listo:** Un revisor entiende qué es y por qué importa sin leer nada más.
- **Nota:** Sección viva — se re-afina tras redactar S5.

## S1 — Context: The System Under Study
- **Propósito:** Describir el sistema bajo estudio para un lector sin contexto previo.
- **Debe contener:** Qué es Vitalis; el método multi-agente (Opus dirige / Sonnet revisa / Haiku redacta); ASLAN; quién es el "usuario"; qué se protege.
- **NO debe tocar:** Las 4 capas (eso es S3); análisis de escala (S5); tabla de evidencia (S4).
- **Criterio de listo:** Un lector externo ubica el sistema sin contexto previo.

## S3 — The Four Layers
- **Propósito:** Explicar el modelo defense-in-depth de 4 capas.
- **Debe contener:** Prevention / Containment / Detection / Recovery — definición + 1 ejemplo real del sistema por capa; **diagrama SVG** de una tarea atravesando las 4 capas.
- **NO debe tocar:** Tabla de evidencia/rutas (S4); ruptura a escala (S5).
- **Criterio de listo:** Cada capa tiene 1 ejemplo concreto verificable del sistema.

## S4 — Artifact → Principle → Evidence
- **Propósito:** Anclar cada afirmación a evidencia inspeccionable.
- **Debe contener:** Tabla artefacto → principio Safeguards → ruta real; **diagrama SVG** del mapa artefacto→principio.
- **NO debe tocar:** Re-explicar las capas (S3); análisis de escala (S5).
- **Criterio de listo:** Toda fila tiene una ruta inspeccionable en vivo.

## S2 — Threat Model (single-user baseline)
- **Propósito:** Enumerar qué puede salir mal hoy, a escala 1-usuario.
- **Debe contener:** 4-5 amenazas concretas (error de modelo, deriva/drift, daño a la salud del usuario final, pérdida de control humano, fuga de alcance).
- **NO debe tocar:** Soluciones (ya en S3/S4); escala (S5).
- **Criterio de listo:** 4-5 amenazas concretas nombradas y acotadas.

## S5 — Where It Breaks at Scale
- **Propósito:** Corazón intelectual — proyectar cada salvaguarda a escala adversarial.
- **Debe contener:** Por cada salvaguarda mono-usuario, cómo evoluciona o colapsa a escala poblacional con un adversario orquestando miles de agentes.
- **NO debe tocar:** Re-describir el sistema mono-usuario (S1).
- **Criterio de listo:** Cada salvaguarda tiene su análisis "where it breaks".

## S6 — Calibrated Honesty
- **Propósito:** Declarar límites del análogo y supuestos — honestidad como rasgo Safeguards.
- **Debe contener:** Qué NO se afirma; límites del salto mono-usuario→producción; supuestos.
- **NO debe tocar:** Vender de más; introducir nuevas afirmaciones técnicas.
- **Criterio de listo:** Las limitaciones quedan declaradas explícitamente.

## S7 — Appendix: Live Verification
- **Propósito:** Permitir que un entrevistador verifique todo por su cuenta.
- **Debe contener:** Comandos reproducibles (`git log`, `cat` de hooks) con rutas reales.
- **NO debe tocar:** Argumentación nueva.
- **Criterio de listo:** Un entrevistador puede correr todo y verificar las afirmaciones.

## S9 — Incident Log: Safeguards Observed During Authorship
- **Subtítulo:** *the method catching its own failures, recorded as they happened.*
- **Propósito:** Documentar casos REALES en que el propio pipeline **(Haiku → guardián → Opus → Human-in-the-Loop)** atrapó un fallo durante la construcción de ESTE documento u otros del proyecto. Evidencia de proceso, no afirmación abstracta.
- **Debe contener:** Por entrada — qué se intentó, qué falló, qué capa/rol lo atrapó, cómo se corrigió, y la lección de Safeguards que ilustra. Formato de bitácora con fecha.
- **NO debe tocar:** Argumentación teórica nueva (eso vive en S5/S6); inventar incidentes (cada entrada debe ser un hecho ocurrido y trazable en el git de este repo).
- **Naturaleza:** SECCIÓN VIVA — se acumula a lo largo de las sesiones.
- **Criterio de listo (por entrada):** El incidente es verificable contra el historial git (commit que lo corrigió) y nombra la lección Safeguards.

### Entradas capturadas (en bruto, a formalizar en inglés en el doc)
- **#1 — Fabricated verbatim quote (2026-06-22, during S1).** Haiku, al redactar S1, presentó una paráfrasis traducida del `CLAUDE.md` como **cita textual** atribuida a un "project charter" inexistente. El **quality-guardian (Sonnet)** lo marcó como BLOQUEANTE: fabricación de evidencia. Se corrigió a paráfrasis honesta sin comillas (commit `32232e7`). Lección Safeguards: un modelo puede alucinar **procedencia/evidencia**, no solo hechos; la cita con comillas es un vector de falsa autoridad. Capa que lo atrapó: **Detección** (revisión independiente por un rol distinto al que redactó). Ironía instructiva: ocurrió en el documento que *trata sobre* honestidad calibrada.
- **#2 — REINCIDENCIA del patrón de cita (2026-06-22, during S3, commit a confirmar).** Al redactar S3, Haiku volvió a presentar una cita "verbatim" del CLAUDE.md, esta vez **truncada** (omitió "en exclusividad" pero cerró las comillas como si fuera completa). El guardián lo marcó BLOQUEANTE de nuevo. Dato instructivo: **la misma clase de fallo reincidió en una sección distinta**, lo que sugiere que es un modo de fallo sistemático del redactor, no un desliz puntual. **Corrección:** cita traducida al inglés como texto principal + original español **completo** entre corchetes. **Lección Safeguards:** los modos de fallo de un modelo son **recurrentes y predecibles**; un control que solo se aplica una vez no basta — debe ser un checkpoint **persistente** del pipeline (justifica que Detección sea un rol fijo, no una revisión ad hoc).
- **#2b — Fuga de alcance hacia S5 (mismo turno).** El párrafo de Recovery de S3 derivó en una cadena de razonamiento adversarial ("defeat prevention / survive containment / evade detection") que es trabajo de S5. El guardián lo marcó como segundo bloqueante. Lección: las fronteras "NO debe tocar" de las fichas también previenen que una sección invada el alcance de otra — la atomicidad es un control de calidad, no solo de organización.
- **#3 — Severidad dimensiona el ejecutor (2026-06-22, durante S5, commit `38d892c`).** Para S5 (corazón del doc, mayor dificultad/severidad), se estableció el subir el ejecutor de Haiku 4.5 a Sonnet 4.6, razonando que el loop barato "ejecutor débil + iterar" tiene una tasa de riesgo inaceptable cuando el peor resultado es no-negociable. Opus aportó matices coincidentes: subir el revisor también (revisor siempre > ejecutor, linaje independiente → revisión = Opus + Human-in-the-Loop, NO otro Sonnet). Se registró como principio [[severity-proportionate-assurance]].**Lección Safeguards:** el rigor del control se dimensiona por la severidad del peor resultado, no por el costo de automatización.
- **#4 — Vigilancia de idioma (2026-06-22, durante S5, commit `38d892c`).** se marcó como primordial que el documento debe ser 100% inglés tras ver español en las NOTAS de resumen de Opus (no en el documento). Aunque el híbrido estaba solo en el resumen conversacional, disparó una verificación explícita (`grep` de palabras españolas) que confirmó: única excepción intencional = la cita original del CLAUDE.md entre corchetes en S3 (junto a su traducción). **Lección:** la vigilancia del Human-in-the-Loop sobre una invariante (idioma) se vuelve un checkpoint reproducible; vale formalizar la verificación, no confiar en la lectura casual.
