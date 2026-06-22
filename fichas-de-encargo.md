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
