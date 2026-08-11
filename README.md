# When Safeguards Don't Scale

**Un estudio de caso sobre salvaguardias de IA — y el método de trabajo con IA con el que fue construido.**
*A case study on AI safeguards — and the AI working-method it was built with.*

Autor / Author: **Andrés Curcio Sole**

> **English below** · [Jump to English](#english)

---

## En una frase

Tomé un proyecto real que construí solo, con salvaguardias desde el día uno (gobernanza *deny-by-default*, puntos de control de calidad, *hooks* de trazabilidad), y me pregunté algo incómodo: **¿qué de esto sobrevive cuando deja de haber un solo supervisor de confianza y aparecen millones de usuarios, miles de agentes concurrentes y actores maliciosos probando los mismos controles a la vez?** La respuesta, desarrollada en el documento, es que **no sobreviven — y que la razón es estructural, no técnica.**

Pero hay una segunda capa: **este repositorio se produjo con el mismo método que documenta.** Un modelo redacta contra una orden de trabajo, un revisor independiente audita, y yo apruebo, rechazo o reescribo antes de consolidar. El *registro de incidentes* captura, en vivo, cada fallo que el propio proceso atrapó mientras se escribía. El método no se describe: se demuestra.

## Qué vas a encontrar acá

Tres piezas conectadas, cada una útil por separado:

| Pieza | Qué es | Estado |
|---|---|---|
| **Estudio de caso de salvaguardias** | El análisis: de un usuario a escala adversarial, qué se rompe y por qué. | ⏳ En progreso |
| **Método de trabajo con IA** | El método reusable (roles, ciclo, memoria, atomicidad, industrialización, trazabilidad) en módulos. | ✅ Completo |
| **Guía de instalación** | Cómo instalar el método en tu propio proyecto para que funcione *out-of-the-box* en cada sesión — con plantillas copiables. | ✅ Completa (12/12) |

Más las **fichas de encargo** (los *blueprints* que produjeron cada documento), las **plantillas** reusables, y el **registro de incidentes** (la evidencia viva del protocolo).

## Cómo navegarlo

Todo el contenido está en español en [`ES/`](ES/) (la versión en inglés, en [`EN/`](EN/), llegará más adelante):

- [`ES/safeguards-case-study.md`](ES/safeguards-case-study.md) — el estudio de caso.
- [`ES/docs/`](ES/docs/) — el método de trabajo, módulo por módulo.
- [`ES/instalaciones/guía-instalación.md`](ES/instalaciones/guía-instalación.md) — la guía de instalación completa.
- [`ES/plantillas/`](ES/plantillas/) — plantillas copiables (contexto base, skill, subagente, hook, memoria, ficha).
- [`ES/registro-de-incidentes/`](ES/registro-de-incidentes/) — los fallos que el proceso atrapó al escribirse.
- [`diagrams/`](diagrams/) — figuras SVG.

## Lo que esto NO es

No es una afirmación de seguridad de nivel de producción. Describo diseño de salvaguardias y los casos que **efectivamente observé**. **No tengo una tasa de detección medida, y no afirmo tenerla.**

## Licencia

- **Contenido y diagramas** (`ES/safeguards-case-study.md`, `ES/docs/`, `diagrams/`): **CC BY 4.0** — ver [`LICENSE.md`](LICENSE.md).
- **Fichas y plantillas** (*work orders*, reusables): **MIT** — ver [`LICENSE-fichas`](LICENSE-fichas).

Atribución: *Andrés Curcio Sole — When Safeguards Don't Scale*.

---

<a name="english"></a>

## In one sentence

I took a real project I built alone, with safeguards from day one (deny-by-default governance, quality checkpoints, traceability hooks), and asked an uncomfortable question: **what survives when there is no longer a single trusted supervisor, and millions of users, thousands of concurrent agents, and bad actors probe the same controls at once?** The answer, worked out in the document, is that **they do not survive — and that the reason is structural, not technical.**

But there is a second layer: **this repository was produced with the very method it documents.** A model drafts against a work order, an independent reviewer audits, and I approve, reject or rewrite before consolidating. The *incident log* captures, live, every failure the process caught while writing itself. The method isn't described — it's demonstrated.

## What you'll find here

Three connected pieces, each useful on its own:

| Piece | What it is | Status |
|---|---|---|
| **Safeguards case study** | The analysis: from one user to adversarial scale — what breaks, and why. | ⏳ In progress |
| **AI working-method** | The reusable method (roles, cycle, memory, atomicity, industrialization, traceability), in modules. | ✅ Complete |
| **Installation guide** | How to install the method in your own project so it works out-of-the-box each session — with copy-paste templates. | ✅ Complete (12/12) |

Plus the **work orders** (the blueprints behind each document), the reusable **templates**, and the **incident log** (the method's living evidence).

## How to navigate it

Everything is in Spanish under [`ES/`](ES/) for now (the English version, under [`EN/`](EN/), will follow):

- [`ES/safeguards-case-study.md`](ES/safeguards-case-study.md) — the case study (written in English).
- [`ES/docs/`](ES/docs/) — the working-method, module by module.
- [`ES/instalaciones/guía-instalación.md`](ES/instalaciones/guía-instalación.md) — the complete installation guide.
- [`ES/plantillas/`](ES/plantillas/) — copy-paste templates.
- [`ES/registro-de-incidentes/`](ES/registro-de-incidentes/) — the failures the process caught as it was written.

## What this is NOT

Not a claim of production-grade security. I describe safeguard design and the cases I actually observed. **I have no measured detection rate, and I do not claim one.**

## License

- **Content and diagrams**: **CC BY 4.0** — see [`LICENSE.md`](LICENSE.md).
- **Work orders and templates**: **MIT** — see [`LICENSE-fichas`](LICENSE-fichas).

Attribution: *Andrés Curcio Sole — When Safeguards Don't Scale*.
