# The AI Working-Method

> Canonical document. Audience: outsider-first (written to teach someone seeing it
> for the first time, with internal notes where they help). It is built module by
> module against the blueprint in
> [`fichas-de-encargo/método-de-trabajo-con-las-fichas.md`](../../ES/fichas-de-encargo/método-de-trabajo-con-las-fichas.md)
> (in Spanish for now). Each module goes through the cycle: drafting (economical
> model) → review (independent reviewer) → assessment and consolidation (director +
> human authority).
>
> **Status:** COMPLETE DOCUMENT — the nine modules (M1-M9), consolidated.

---

## The nine modules

| # | Module | What it covers |
|---|--------|----------------|
| 1 | [Vision and purpose](01-vision-and-purpose.md) | What problem the method solves, and why it exists |
| 2 | [Roles and responsibilities](02-roles-and-responsibilities.md) | The four roles, their limits of authority, and assurance proportional to severity |
| 3 | [The production cycle](03-production-cycle.md) | The operational sequence of a task, from skeleton to consolidation |
| 4 | [Persistent memory](04-persistent-memory.md) | How context is kept across sessions, and how it differs from version control |
| 5 | [Atomicity rules](05-atomicity-rules.md) | What makes a task atomic, and the work order as its tool |
| 6 | [Industrialization](06-industrialization.md) | When and how to automate what repeats: hook, skill or subagent |
| 7 | [Use cases](07-use-cases.md) | The method applied, with its results and its lessons |
| 8 | [Limits](08-limits.md) | When NOT to use the method, its costs, and the assumptions it rests on |
| 9 | [Traceability and reversibility](09-traceability-and-reversibility.md) | The four layers: Prevention, Containment, Detection, Recovery |

**Complement:** [Applicability to verticals](10-applicability-to-verticals.md) maps the
method to marketing, real estate and IT, and includes a template for adapting it to any sector.

## Suggested reading order

If you're here with no context: **1 → 2 → 5 → 3**. The why and the roles first, then
atomicity, and only then the cycle that uses it.

If you're here to implement it: **2 → 5 → 9**, and from there straight to
[the installation guide](../../ES/instalaciones/guía-instalación.md) and
[the templates](../../ES/plantillas/) (both in Spanish for now).

If you're here to judge whether the method holds up:
**8 → [incident log](../../ES/registro-de-incidentes/) → 9** (in Spanish for now). Limits
first, then the real failures, and last the layers that contain them.

## Where the rest lives

These folders don't have an English version yet, so the links point to the Spanish originals:

- [`registro-de-incidentes/`](../../ES/registro-de-incidentes/) — the failures the method
  caught while documenting itself, including those in its own upper layers.
- [`fichas-de-encargo/`](../../ES/fichas-de-encargo/) — the real work orders that produced this
  documentation. They serve as evidence and as worked examples.
- [`instalaciones/`](../../ES/instalaciones/) — the step-by-step adoption guide.
- [`plantillas/`](../../ES/plantillas/) — the copy-paste skeletons for each piece.
