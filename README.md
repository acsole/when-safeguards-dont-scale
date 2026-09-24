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

Tres piezas conectadas, cada una útil por separado, disponibles **en español y en inglés**:

| Pieza | Qué es | Estado |
|---|---|---|
| **Estudio de caso de salvaguardias** | El análisis: de un usuario a escala adversarial, qué se rompe y por qué. | ⏳ En progreso |
| **Método de trabajo con IA** | El método reusable (roles, ciclo, memoria, atomicidad, industrialización, trazabilidad) en módulos. | ✅ Completo |
| **Guía de instalación** | Cómo instalar el método en tu propio proyecto para que funcione *out-of-the-box* en cada sesión — con plantillas copiables. | ✅ Completa (12/12) |

Más las **fichas de encargo** (los *blueprints* que produjeron cada documento), las **plantillas** reusables, y el **registro de incidentes** (la evidencia viva del protocolo).

## Cómo navegarlo

El repositorio es **bilingüe**: cada pieza vive en español bajo [`ES/`](ES/) y en inglés bajo [`EN/`](EN/). El estudio de caso, escrito directamente en inglés, es la pieza raíz.

- [`safeguards-case-study.md`](safeguards-case-study.md) — el estudio de caso (en la raíz del repositorio; escrito en inglés).

| Pieza | Español | English |
|---|---|---|
| El método, módulo por módulo | [`ES/docs/`](ES/docs/) | [`EN/docs/`](EN/docs/) |
| Guía de instalación completa | [`ES/instalaciones/`](ES/instalaciones/) | [`EN/installation/`](EN/installation/) |
| Plantillas copiables | [`ES/plantillas/`](ES/plantillas/) | [`EN/templates/`](EN/templates/) |
| Fichas de encargo (los *blueprints*) | [`ES/fichas-de-encargo/`](ES/fichas-de-encargo/) | [`EN/work-orders/`](EN/work-orders/) |
| Registro de incidentes | [`ES/registro-de-incidentes/`](ES/registro-de-incidentes/) | [`EN/incident-log/`](EN/incident-log/) |

Y [`diagrams/`](diagrams/) — figuras SVG (neutras al idioma).

## Lo que esto NO es

No es una afirmación de seguridad de nivel de producción. Describo diseño de salvaguardias y los casos que **efectivamente observé**. **No tengo una tasa de detección medida, y no afirmo tenerla.**

## Licencia

- **Contenido y diagramas** (`safeguards-case-study.md`, `ES/docs/`, `EN/docs/`, `diagrams/`): **CC BY 4.0** — ver [`LICENSE.md`](LICENSE.md).
- **Fichas y plantillas** (*work orders*, reusables): **MIT** — ver [`LICENSE-fichas`](LICENSE-fichas).

Atribución: *Andrés Curcio Sole — When Safeguards Don't Scale*.

---

<a name="english"></a>

## In one sentence

I took a real project I built alone, with safeguards from day one (deny-by-default governance, quality checkpoints, traceability hooks), and asked an uncomfortable question: **what survives when there is no longer a single trusted supervisor, and millions of users, thousands of concurrent agents, and bad actors probe the same controls at once?** The answer, worked out in the document, is that **they do not survive — and that the reason is structural, not technical.**

But there is a second layer: **this repository was produced with the very method it documents.** A model drafts against a work order, an independent reviewer audits, and I approve, reject or rewrite before consolidating. The *incident log* captures, live, every failure the process caught while writing itself. The method isn't described — it's demonstrated.

## What you'll find here

Three connected pieces, each useful on its own, available **in Spanish and English**:

| Piece | What it is | Status |
|---|---|---|
| **Safeguards case study** | The analysis: from one user to adversarial scale — what breaks, and why. | ⏳ In progress |
| **AI working-method** | The reusable method (roles, cycle, memory, atomicity, industrialization, traceability), in modules. | ✅ Complete |
| **Installation guide** | How to install the method in your own project so it works out-of-the-box each session — with copy-paste templates. | ✅ Complete (12/12) |

Plus the **work orders** (the blueprints behind each document), the reusable **templates**, and the **incident log** (the method's living evidence).

## How to navigate it

The repository is **bilingual**: every piece lives in Spanish under [`ES/`](ES/) and in English under [`EN/`](EN/). The case study, written directly in English, is the root piece.

- [`safeguards-case-study.md`](safeguards-case-study.md) — the case study (at the repository root; written in English).

| Piece | Español | English |
|---|---|---|
| The working-method, module by module | [`ES/docs/`](ES/docs/) | [`EN/docs/`](EN/docs/) |
| The complete installation guide | [`ES/instalaciones/`](ES/instalaciones/) | [`EN/installation/`](EN/installation/) |
| Copy-paste templates | [`ES/plantillas/`](ES/plantillas/) | [`EN/templates/`](EN/templates/) |
| Work orders (the blueprints) | [`ES/fichas-de-encargo/`](ES/fichas-de-encargo/) | [`EN/work-orders/`](EN/work-orders/) |
| Incident log | [`ES/registro-de-incidentes/`](ES/registro-de-incidentes/) | [`EN/incident-log/`](EN/incident-log/) |

And [`diagrams/`](diagrams/) — SVG figures (language-neutral).

## What this is NOT

Not a claim of production-grade security. I describe safeguard design and the cases I actually observed. **I have no measured detection rate, and I do not claim one.**

## License

- **Content and diagrams** (`safeguards-case-study.md`, `ES/docs/`, `EN/docs/`, `diagrams/`): **CC BY 4.0** — see [`LICENSE.md`](LICENSE.md).
- **Work orders and templates**: **MIT** — see [`LICENSE-fichas`](LICENSE-fichas).

Attribution: *Andrés Curcio Sole — When Safeguards Don't Scale*.
