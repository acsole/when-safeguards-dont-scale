# Safeguards Case Study

**Analizando mi propio proyecto asistido por IA desde la perspectiva de las medidas de seguridad de la IA y preguntándome qué falla al escalarlo.**

Autor: Andrés Curcio Sole

---

## ¿Qué es esto?

Un estudio de caso que examina un proyecto real de un solo usuario que desarrollé con medidas de seguridad desde el principio:

- Gobernanza de denegación por defecto,
- Puntos de control de calidad en los flujos de trabajo de los agentes,
- Ganchos de trazabilidad
- y rastrea cada medida de seguridad desde mi propia supervisión como fundador único hasta la presión de un despliegue a gran escala con amenazas.

Separa los principios que se mantienen bajo estrés ante amenazas de las fallas que solo aparecen en producción.

La pregunta central: ¿pueden los mecanismos diseñados para un supervisor de confianza sobrevivir cuando millones de usuarios, miles de agentes concurrentes y actores maliciosos ponen a prueba los mismos puntos de control al mismo tiempo? La respuesta que se encuentra en el documento es que no pueden, y que la razón es estructural, no técnica.

## Lo que esto *NO* es

Esto **NO** es una afirmación de seguridad de nivel de producción. Describo el diseño de medidas de seguridad y los casos que he observado. **No tengo una tasa de detección medida, ni afirmo tenerla**.

## Estado: documento en desarrollo, trabajo en progreso

Redacto esto mediante el mismo proceso multiagente que se describe:
- Un modelo de redacción trabaja con una orden de trabajo que escribo.

- Un modelo de revisión independiente audita el borrador con respecto a dicha orden.

- Apruebo, rechazo o reescribo cada sección antes de que se confirme.

- El repositorio se actualiza a medida que se completan las secciones.

**Escrito hasta ahora:**

- Presentación breve · Contexto · Las cuatro capas · Artefacto → Principio → Evidencia · Modelo de amenazas · Dónde falla a gran escala

**Alcance previsto pero aún no escrito:** Honestidad calibrada (mis limitaciones, explicadas claramente) · Apéndice sobre verificación en vivo · Registro de incidentes de los fallos detectados por este proceso durante la redacción de este documento

## Contenido del repositorio

| Ruta | Qué es |

|------|-----------|

| [`safeguards-case-study.md`](safeguards-case-study.md) | El estudio de caso en sí. |

| [`fichas-de-encargo.md`](fichas-de-encargo.md) | Las órdenes de trabajo ("fichas de encargo"): las especificaciones de tareas atómicas con las que se basó cada sección. Reutilizable como plantilla. |

| [`diagrams/`](diagrams/) | Figuras SVG independientes a las que se hace referencia en el estudio de caso. |

## Proceso de producción

Cada sección sigue el mismo ciclo: un modelo de redacción crea una sección según su orden de trabajo, un modelo de revisión independiente la audita campo por campo y yo la apruebo o la devuelvo. Cada sección aceptada se guarda como una confirmación de Git independiente, por lo que el historial constituye un registro revisable de cómo se construyó el documento. El registro de incidencias del documento registra los fallos detectados durante la creación.

## Licencia

Este repositorio tiene doble licencia:

- **El contenido y los diagramas del estudio de caso** — `safeguards-case-study.md` y todo lo que se encuentra en `diagrams/` — están bajo la licencia **Creative Commons Atribución 4.0 Internacional (CC BY 4.0)**. Consulte [`LICENSE.md`](LICENSE.md). Puede compartir y adaptar este contenido, incluso con fines comerciales, siempre que se cite la fuente adecuadamente.
Las órdenes de trabajo (fichas-de-encargo.md) están bajo la licencia MIT, por lo que pueden reutilizarse libremente como plantilla. Consulte el archivo LICENSE.

Atribución: Andrés Curcio Sole — Estudio de caso sobre salvaguardias.

-----------------------------------------------------------------[ENGLISH VERSION]-----------------------------------------------------------------
**Reading my own AI-assisted project through the lens of AI safeguards, and asking what breaks when it scales.**

Author: Andrés Curcio Sole

---

## What this is

A case study that examines a real, single-user project I built with safeguards in place from the start: 

- deny-by-default governance,
- quality checkpoints across agent workflows,
- traceability hooks
- and traces each safeguard from my own oversight as a single founder to the pressure of an adversarial, population-scale deployment.

It separates the principles that hold under adversarial stress from the fractures that only appear in production.

The central question: can mechanisms designed for one trusted supervisor survive when millions of users, thousands of concurrent agents, and bad actors probe the same checkpoints at the same time? The answer worked out in the document is that they cannot, and that the reason is structural rather than technical.

## What this is *NOT*

This is **NOT** a claim of production-grade security. I describe safeguard design and the cases I have actually observed. I have **no measured detection rate, and I do not claim one**.

## Status: living document, work in progress

I draft this through the same multi-agent pipeline it describes: 
- a drafting model works against a work order I write,
- an independent reviewer model audits the draft against that order,
- and I approve, reject or rewrite every section before anything is committed.
- The repository is updated as sections are completed.

**Written so far:** 

- Elevator Pitch · Context · The Four Layers · Artifact → Principle → Evidence · Threat Model · Where It Breaks at Scale

**Scoped but not yet written:** Calibrated Honesty (my limitations, stated plainly) · Appendix on live verification · Incident Log of the failures this pipeline catches while writing this document

## Repository contents

| Path | What it is |
|------|-----------|
| [`safeguards-case-study.md`](safeguards-case-study.md) | The case study itself. |
| [`fichas-de-encargo.md`](fichas-de-encargo.md) | The work orders ("fichas de encargo") — the atomic task specifications each section was drafted against. Reusable as a template. |
| [`diagrams/`](diagrams/) | Standalone SVG figures referenced by the case study. |

## How it was produced

Every section follows the same cycle: a drafting model produces a section against its work order, an independent reviewer model audits it field by field, and I approve or send it back. Each accepted section lands as its own git commit, so the history is a reviewable record of how the document was built. The document's own Incident Log records failures the pipeline caught during authorship.

## License

This repository is dual-licensed:

- **The case-study content and diagrams** — `safeguards-case-study.md` and everything under `diagrams/` — are licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license. See [`LICENSE.md`](LICENSE.md). You are free to share and adapt this content, including commercially, as long as you give appropriate credit.
- **The work orders** — `fichas-de-encargo.md` — are licensed under the **MIT License**, so they can be reused freely as a template. See [`LICENSE-fichas`](LICENSE-fichas).

Attribution: *Andrés Curcio Sole — Safeguards Case Study*.
