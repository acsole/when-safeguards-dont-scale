# Safeguards Case Study

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
