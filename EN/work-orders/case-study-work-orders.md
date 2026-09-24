# Work orders — Safeguards Case Study

> A scoping document (originally Spanish, internal). The final document (`safeguards-case-study.md`) is **100% in English**.
> Each work order defines an atomic section. The **MUST NOT touch** boundary is what keeps the modules from stepping on each other.
> Per-section pipeline: Haiku drafts (returns content, does not write files) → quality-guardian (Sonnet) audits → correction → Opus + Human-in-the-Loop approve → consolidate + commit.

## The cross-cutting intellectual axis
The differentiating value is the **scale jump**: from "1 user / 1 project" → production environments with thousands/millions of lives and adversaries orchestrating tens of thousands of agents. Calibrated honesty (saying what is NOT claimed) is itself a Safeguards trait.

## Output form (all)
Markdown in English, a self-contained section, a professional and sober tone (not marketing). Diagrams as embeddable SVG when the work order indicates it.

## Drafting order
**S0 → S1 → S3 → S4 → S2 → S5 → S6 → S7**, with a **re-pass of S0 after S5** (the pitch is a living section: it is hardened once the body exists).
**S9** (Incident Log) is a LIVING section: it grows each session, as the pipeline itself catches failures during drafting. It is not "written in one go"; it accumulates.

---

## S0 — Elevator Pitch
- **Purpose:** Hook a Safeguards reader in under 30 seconds.
- **Must contain:** The thesis in 1 sentence; 3-4 supporting sentences; the scale hook (single-user → population-scale adversarial).
- **MUST NOT touch:** Technical detail, paths, diagrams, tables.
- **Inputs:** The system overview (S1) + the scale axis.
- **Output form:** ~6-8 lines of English prose.
- **Definition of done:** A reviewer understands what it is and why it matters without reading anything else.
- **Note:** A living section — refined after S5 is drafted.

## S1 — Context: The System Under Study
- **Purpose:** Describe the system under study for a reader with no prior context.
- **Must contain:** What Remanso is; the multi-agent method (Opus directs / Sonnet reviews / Haiku drafts); the monitoring dashboard; who the "user" is; what is protected.
- **MUST NOT touch:** The 4 layers (that is S3); scale analysis (S5); the evidence table (S4).
- **Definition of done:** An external reader locates the system with no prior context.

## S3 — The Four Layers
- **Purpose:** Explain the 4-layer defense-in-depth model.
- **Must contain:** Prevention / Containment / Detection / Recovery — a definition + 1 real example from the system per layer; an **SVG diagram** of a task crossing the 4 layers.
- **MUST NOT touch:** The evidence/paths table (S4); the break at scale (S5).
- **Definition of done:** Each layer has 1 concrete, verifiable example from the system.

## S4 — Artifact → Principle → Evidence
- **Purpose:** Anchor every claim to inspectable evidence.
- **Must contain:** An artifact → Safeguards principle → real path table; an **SVG diagram** of the artifact→principle map.
- **MUST NOT touch:** Re-explaining the layers (S3); scale analysis (S5).
- **Definition of done:** Every row has a live, inspectable path.

## S2 — Threat Model (single-user baseline)
- **Purpose:** Enumerate what can go wrong today, at single-user scale.
- **Must contain:** 4-5 concrete threats (model error, drift, harm to the end user's health, loss of human control, scope leak).
- **MUST NOT touch:** Solutions (already in S3/S4); scale (S5).
- **Definition of done:** 4-5 concrete threats named and bounded.

## S5 — Where It Breaks at Scale
- **Purpose:** The intellectual heart — project each safeguard to adversarial scale.
- **Must contain:** For each single-user safeguard, how it evolves or collapses at population scale with an adversary orchestrating thousands of agents.
- **MUST NOT touch:** Re-describing the single-user system (S1).
- **Definition of done:** Each safeguard has its "where it breaks" analysis.

## S6 — Calibrated Honesty
- **Purpose:** State the analogy's limits and assumptions — honesty as a Safeguards trait.
- **Must contain:** What is NOT claimed; the limits of the single-user→production jump; assumptions.
- **MUST NOT touch:** Overselling; introducing new technical claims.
- **Definition of done:** The limitations are stated explicitly.

## S7 — Appendix: Live Verification
- **Purpose:** Let an interviewer verify everything on their own.
- **Must contain:** Reproducible commands (`git log`, `cat` of hooks) with real paths.
- **MUST NOT touch:** New argumentation.
- **Definition of done:** An interviewer can run everything and verify the claims.

## S9 — Incident Log: Safeguards Observed During Authorship
- **Subtitle:** *the method catching its own failures, recorded as they happened.*
- **Purpose:** Document REAL cases in which the pipeline itself (Haiku → guardian → Opus → Human-in-the-Loop) caught a failure during the construction of THIS document or others in the project. Process evidence, not an abstract claim.
- **Must contain:** Per entry — what was attempted, what failed, which layer/role caught it, how it was corrected, and the Safeguards lesson it illustrates. A dated log format.
- **MUST NOT touch:** New theoretical argumentation (that lives in S5/S6); inventing incidents (each entry must be an event that happened and is traceable in this repo's git).
- **Nature:** A LIVING SECTION — it accumulates across sessions.
- **Definition of done (per entry):** The incident is verifiable against the git history (the commit that fixed it) and names the Safeguards lesson.

### Captured entries (raw, to be formalized in English in the doc)
- **#1 — Fabricated verbatim quote (2026-06-22, during S1).** While drafting S1, Haiku presented a translated paraphrase of the `CLAUDE.md` as a **verbatim quote** attributed to a non-existent "project charter". The **quality-guardian (Sonnet)** flagged it as BLOCKING: evidence fabrication. It was corrected to an honest paraphrase without quotation marks (commit `32232e7`). Safeguards lesson: a model can hallucinate **provenance/evidence**, not just facts; a quotation with quote marks is a vector of false authority. Layer that caught it: **Detection** (independent review by a role other than the one that drafted). An instructive irony: it happened in the document that *is about* calibrated honesty.
- **#2 — RECURRENCE of the quote pattern (2026-06-22, during S3, commit to be confirmed).** While drafting S3, Haiku again presented a "verbatim" quote from the CLAUDE.md, this time **truncated** (it omitted "exclusively" but closed the quote marks as if it were complete). The guardian flagged it BLOCKING again. An instructive fact: **the same class of failure recurred in a different section**, which suggests it is a systematic drafter failure mode, not a one-off slip. **Correction:** the quote translated into English as the main text + the **complete** Spanish original in brackets. **Safeguards lesson:** a model's failure modes are **recurring and predictable**; a control applied only once is not enough — it must be a **persistent** checkpoint of the pipeline (it justifies Detection being a fixed role, not an ad hoc review).
- **#2b — Scope leak into S5 (same turn).** S3's Recovery paragraph drifted into a chain of adversarial reasoning ("defeat prevention / survive containment / evade detection") that is S5's job. The guardian flagged it as a second blocker. Lesson: the work orders' "MUST NOT touch" boundaries also prevent one section from invading another's scope — atomicity is a quality control, not just an organizational one.
- **#3 — Severity sizes the executor (2026-06-22, during S5, commit `38d892c`).** For S5 (the document's heart, of greater difficulty/severity), it was established to move the executor from Haiku 4.5 up to Sonnet 4.6, reasoning that the cheap "weak executor + iterate" loop has an unacceptable risk rate when the worst outcome is non-negotiable. Opus added converging nuances: move the reviewer up too (reviewer always > executor, independent lineage → review = Opus + Human-in-the-Loop, NOT another Sonnet). It was recorded as the principle [[severity-proportionate-assurance]]. **Safeguards lesson:** the rigor of the control is sized by the severity of the worst outcome, not by the cost of automation.
- **#4 — Language vigilance (2026-06-22, during S5, commit `38d892c`).** It was flagged as paramount that the document must be 100% English, after seeing Spanish in Opus's summary NOTES (not in the document). Although the hybrid was only in the conversational summary, it triggered an explicit verification (a `grep` for Spanish words) that confirmed: the only intentional exception = the original CLAUDE.md quote in brackets in S3 (next to its translation). Lesson: the Human-in-the-Loop's vigilance over an invariant (language) becomes a reproducible checkpoint; it is worth formalizing the verification, not trusting a casual read.
