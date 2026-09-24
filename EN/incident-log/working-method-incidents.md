## Appendix A — Dogfooding log (incident record)

> **What it is.** This method was built by using itself (*dogfooding*): each module
> was drafted by an executor (Haiku) and audited by an independent reviewer (quality-guardian,
> Sonnet) before human approval (Opus + Human-in-the-Loop). This log records, with total
> transparency, **every incident caught in review**: what was detected, in whom, when, why
> it mattered and how it was corrected. Its value is twofold: it shows the detection net
> works, and it serves to **calibrate the reviewer itself** and make it more attentive with
> each iteration — regardless of the model version that embodies it.
>
> Columns: **#** · **Date** · **Module** · **Executor** (corrected) · **Reviewer** ·
> **Finding** · **Severity** · **Correction applied** · **Why it mattered**.

### Module 1 — Vision and purpose · 2026-06-22 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 1.1 | The **anchor to the author's real projects** was missing | 🔴 Blocking | Added the sentence "it is not theory: it came out of applying it on real projects of my own" | Without an anchor, the module sounded like theory; the field was mandatory in the work order |
| 1.2 | The **three pillars** came with micro-development (invading M2/M3) | 🟡 Improvement | Trimmed to just their names | Keeping boundaries between modules; avoiding duplication |
| 1.3 | The **thesis** was diluted in a long paragraph | 🟡 Improvement | Isolated into 1-2 highlighted sentences | Readability; the thesis must be immediately identifiable |
| 1.4 | Used "final authority" instead of "**human authority**" | ⚪ Minor | The term was unified | Terminological consistency across modules |

**Lesson / calibration:** the drafter tends to **over-explain** and to **omit the concrete anchor**. From then on the work orders reinforced the "Anchor" field and the "MUST NOT touch" boundaries.

### Module 2 — Roles and responsibilities · 2026-06-23 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 2.1 | The "why" of **strength ↔ cost** per role was not made explicit | 🟡 Improvement | Added the cost-benefit reasoning of each assignment | The module had to justify the assignment, not just state it |
| 2.2 | The severity principle was repeated **three times** | 🟡 Improvement | Consolidated into a single formulation + a brief close | Economy; redundancy dilutes the message |
| 2.3 | "Who decides in the last instance?" lacked its own force | ⚪ Minor | Stated explicitly in the table ("Decides in the last instance") | The work order's four questions had to carry equal weight |
| 2.4 | **5 subheadings** for ~480 words → fragmentation | ⚪ Minor | Reduced to 2 | A compact structure in line with the work order |

**Notable calibration incident:** during this review, the reviewer **corrected the director**. Opus estimated "more than 650 words, over the range"; the reviewer's real count was **483 words, within range**. Takeaway: quantitative estimates are verified by counting, not by eye — and the review layer applies **to the director too**, not just to the executor.

**Lesson / calibration:** the drafter tends toward **structural redundancy** (repeating the same concept across several sections) and toward **over-subheading**. The reviewer showed independence of judgment by contradicting both the executor and the director with evidence.

### Module 5 — Atomicity rules · 2026-06-23 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

Reviewer's first return — **two blockers**:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 5.1 | **Length** ~640-660 words (cap: 600) | 🔴 Blocking | Trimmed to 542 words | An explicit, verifiable numeric requirement of the work order |
| 5.2 | **Redundancy:** M5 itself used as a self-example 3 times (the root cause of the overrun) | 🔴 Blocking | Kept a single case; varied examples (compliance / contrast / the document's work orders) | Repetition inflates length and dilutes the message |
| 5.3 | The term "scope" only incidental | ⚪ Minor | Deliberately incorporated into the work order's definition | Consistency with the key terms |
| 5.4 | "A work order that drafts instead of bounding" not named explicitly | ⚪ Minor (optional) | The director (Opus) added it on consolidation | Completeness against the work order's "mistakes to avoid" list |

**Escalation rule armed by the Human-in-the-Loop (severity-proportionate assurance, live):** it was agreed that if the **re-audit** of this correction came back with any 🔴 blocker, the next iteration would escalate to a **Sonnet 4.6 executor + an Opus auditor** (moving executor and reviewer up a level). **Re-audit: DONE, no blockers → the rule was left *armed*, not consumed.** Haiku stays as drafter.

**Lesson / calibration:** the drafter's redundancy is not merely cosmetic: it **inflates the length until it breaks a hard requirement**. An effective antidote: ask for *varied* examples instead of self-references. It was confirmed (again) that length is **counted**, not estimated by eye: the director underestimated the overrun, the reviewer measured it.

### Module 3 — The production cycle · 2026-06-23 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

Reviewer's first return — **two blockers**:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 3.1 | Used the **internal proper name "Andrés"** 6 times (prose + diagram) | 🔴 Blocking | Replaced with "the human authority" throughout | The document is outsider-first; a third party does not know who Andrés is. It broke the M1/M2 convention |
| 3.2 | **Fabrication:** "some modules reached three rounds" (false; real maximum: 2) | 🔴 Blocking | Replaced with "more than one round of correction" (truthful, generic) | An invented fact presented as true — and in the module that preaches "verify, don't trust" |
| 3.3 | The diagram did not visually anchor the automation checkpoint | 🟡 Improvement | The director added the `[↻ Checkpoint…]` line to the diagram | The work order asked that the reader be able to "point to where automating is evaluated" |
| 3.4 | Inconsistent singular/plural in "Living proof" | ⚪ Minor | Unified to singular | Register consistency |

**Escalation decision (severity-proportionate):** because there were blockers, triggering the rule (Sonnet executor + Opus auditor) was considered. The human authority ruled, faithful to the letter of the rule, that **this was M3's first return** → Haiku was entitled to one round of correction; escalation is reserved for a **re-audit** that recurs into blockers. **Re-audit: PASS, no blockers → escalation NOT consumed.**

**The director's drafting decision (calibrated honesty):** the reviewer optionally suggested tightening "more than one round" → "up to two rounds". It was **rejected**: "up to two" is true today, but would expire if a future module reaches three rounds. The formulation robust to the future was preferred. A truth that cannot become a lie tomorrow is worth more than today's precision.

**Lesson / calibration:** **fabrication** was confirmed as a recurring drafter failure mode (already seen on other fronts of the project): it invents concrete figures to "sound" verifiable. The reviewer could only catch it because it was handed the **ground truth** (the real count of rounds) — a key takeaway: *the reviewer needs the reference facts to detect fabrications; its judgment alone is not enough.* This reinforces the practice of giving the guardian the project's verifiable data in every factual audit.

### Module 4 — Persistent memory · 2026-06-23 · FIRST ACTIVATION OF THE ESCALATION RULE

This module is the fullest evidence of the protocol, because it went through the **three stages** of the assurance ladder.

**Round 1 — Executor: Haiku · Reviewer: quality-guardian (Sonnet)**

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 4.1 | **Fabrication:** an invented conditional rule for loading memory by task type ("if it's coding → project+feedback; if it's design → +user") | 🔴 Blocking | Haiku reformulated the section | A specific mechanism presented as real with no basis |

**Round 2 (re-audit) — Executor: Haiku · Reviewer: quality-guardian (Sonnet)**

| # | Finding | Severity | Result |
|---|---------|----------|--------|
| 4.2 | **Recurrence:** the fabrication came back in a subtler form ("according to the nature of the task, it retrieves the relevant files") — the same selection mechanism, only veiled | 🔴 Blocking | **A re-audit with a blocker → TRIGGERS the escalation rule** |

**Round 3 (escalated) — Executor: Sonnet 4.6 · Reviewer: Opus (director)**

Per the rule of assurance proportional to severity, when the blocker recurred in the re-audit, the iteration went up a level: the executor moved from Haiku to **Sonnet 4.6**, and the reviewer from quality-guardian to **Opus** (preserving reviewer > executor). Sonnet not only removed the fabrication: it **explicitly denied it** in the text ("There is no automatic mechanism that filters or selects files by the type of task... reading what is relevant is a deliberate step"). Opus's audit: **PASS, no blockers**. Resolved in a single pass.

**The director's calibration incident (important):** in the two rounds with Haiku, the director (Opus) **underestimated the fabrication**: in its pre-read it rated it "an acceptable generic example" and then "a truthful formulation". In both cases the **independent reviewer** (the guardian) detected what the director had missed. It is the strongest proof of why the reviewer must be independent of the director, and of why the final approval authority does not rest with whoever directs.

**Lesson / calibration — the protocol worked as designed:**
- The **severity ladder** is not theory: it activated on real evidence (a recurring blocker) and solved the problem the economical level could not.
- Moving the executor (Haiku→Sonnet) AND the reviewer (guardian→Opus) up **at the same time** preserved the reviewer > executor independence.
- A more capable model did not just "get it right": it turned the weak point into an **explicit clarification** — a sign that the extra capability is better spent on the hard part (consistent with M2).
- An uncomfortable but valuable confirmation: **the director is fallible and can be lenient toward the failure mode it does not detect itself**; the defense is not "trying harder", but the **structure** (an independent reviewer + evidence-based escalation).

### Module 9 — Traceability and reversibility · 2026-06-23 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

Reviewer's first return — **one blocker**:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 9.1 | **Omission of a mandatory element:** the sentence distinguishing memory (M4) from versioning/git, with its reference, was missing | 🔴 Blocking | Added the section "A critical distinction: versioning vs. memory" with a reference to M4 | It was an explicit "Must contain" point of the work order; without it, the reader confuses two distinct mechanisms |
| 9.2 | The commit/diff concept explained 3 times (table + section + flow) | 🟡 Improvement | The redundancy was trimmed → it freed space for 9.1 without going over 600 | Economy; and resolving an improvement enabled resolving the blocker |
| 9.3 | Typo "decididen" → "deciden" | ⚪ Minor | Corrected | Neatness |

**Re-audit: PASS** (580 words, blocker resolved, no new findings). Escalation NOT triggered: Haiku corrected itself in one round.

**Calibration note (a contrast with M4):** here the director (Opus) **did pre-identify the blocker** — the missing memory↔git distinction — before the guardian's audit. The M4 lesson (do not underestimate) was applied. The director's calibration also improves with experience, not just the drafter's or the reviewer's.

**Lesson / calibration:** a failure mode **different** from fabrication appeared: the **omission of a mandatory element** of the work order. The drafter developed well what it did include (git), but left out an explicit requirement. Antidote: the work order works as a verifiable *checklist* and the reviewer runs through it point by point — that is why the "Must contain" field must be a closed list, not a diffuse intention.

### Module 6 — Industrialization · 2026-06-23 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**No blockers** (the cleanest module so far). A single round, cosmetic adjustments applied by the director on consolidation:

| # | Finding | Severity | Correction applied |
|---|---------|----------|--------------------|
| 6.1 | Inconsistent grammatical gender of "skill" ("una skill" / "lo activa" / "los skills") | 🟡 Improvement | Unified to feminine ("una skill" / "las skills" / "la activa") |
| 6.2 | Decision table with a hybrid row and a duplicated subagent row | ⚪ Minor | Simplified to 3 core rows (one per tool); the combination was left only in the text section |
| 6.3 | Colloquial turn "no debate" | ⚪ Minor | Reformulated to "stops the action automatically, with no human intervention" |

**Key methodological finding (recorded at the Human-in-the-Loop's request):** M6 had **zero fabrication**, unlike M3/M4. The difference was the input: Haiku was handed the **three real, already-verified ASLAN examples** (preamble→subagent, conventions→skill, grep→hook). **Restricting the generation surface with concrete facts drastically reduces invention.** A practical corollary for the method: when a module depends on verifiable data, giving it to the drafter *beforehand* — instead of waiting for the reviewer to catch the invented afterward — is cheaper and safer. Detection is the last net, not the first.

### Module 7 — Use cases · 2026-06-23 · Executor: Haiku · Reviewer: quality-guardian (Sonnet) · Final verification: Opus

This module left two distinct lessons: one about the drafter and another, unprecedented, **about the reviewer**.

**Round 1 — three blockers from fabrication:**

| # | Finding | Severity | Correction applied |
|---|---------|----------|--------------------|
| 7.1 | **Ironic fabrication:** when illustrating "what the reviewer caught as a fabrication", it invented a quote that never happened (*"according to an analysis of X"*) instead of the real cases | 🔴 Blocking | Replaced with the real fabrications (the "three rounds" of M3; the memory rule of M4) |
| 7.2 | Embellishment in the ASLAN case: "under simultaneous load" (did not happen) | 🔴 Blocking | Removed |
| 7.3 | Embellishment: "accumulating" (did not happen) | 🔴 Blocking | Removed |

The juiciest detail: **the "real cases" module fabricated inside its own example of what a fabrication is.** Compelling proof that the "fabrication" failure mode is persistent and of why independent detection is indispensable.

**Round 2 (re-audit) — the reviewer got it wrong, and the director verified it:**

The guardian confirmed the three fabrications were resolved, but raised a **new length blocker**, estimating "~700-750 words" — **by eye, without counting**. The director (Opus), instead of accepting it and triggering the escalation, applied *"verify, don't trust"* **toward the reviewer itself**: it objectively counted the module's body → **518 words**, within range. The blocker was a **false positive**.

**Lessons / calibration:**
- **The reviewer is fallible too** — and, notably, it failed on the very rule it had taught us in M2/M5: *length is counted, not estimated by eye.*
- **"Verify, don't trust" applies in every direction**, including upward (from the director to the reviewer), not only downward (toward the drafter).
- **Verifying the trigger before acting avoided a useless escalation:** the escalation rule did NOT activate, because its condition (a *real* blocker in the re-audit) was not met. Escalating over a false positive would have spent capability for no reason.
- A corollary for the protocol: no layer — not drafter, not reviewer, not director — is infallible; robustness does not come from trusting a role, but from **every verifiable claim being verified with the right tool**, whoever it comes from.

### Module 8 — Limits, and when not to use the method · 2026-06-23 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**One round, one blocker:**

| # | Finding | Severity | Correction applied |
|---|---------|----------|--------------------|
| 8.1 | The internal proper name "Andrés" used twice (a RECURRENCE of the M3 failure) | 🔴 Blocking | Replaced with "the human" / "the human authority" |

**Process note (proportional verification):** since it was a mechanical two-word replacement, the director did NOT trigger a full guardian re-audit; it objectively verified with a search (`grep`) that no mention of the proper name remained in the module bodies. It is an application of the very principle of assurance proportional to severity (Module 2): the rigor of the verification is sized to the risk of the change.

**Lesson / calibration:** the "internal proper name" failure mode RECURRED (it had already appeared in M3). A recurring and predictable failure is the best candidate to **industrialize** (Module 6): it could become a hook that detects internal proper names in the drafts before human review — one more example of how dogfooding feeds the improvement of the protocol itself.

---

---

## Closing — Document status

The **9 modules are consolidated** and the document is complete. This log records **8 incident sessions** (M1–M9; M5 with two rounds, M3/M4/M7 too) that cover a repertoire of drafter failure modes — **redundancy, fabrication, omission, embellishment and internal proper name** — plus one case of **reviewer fallibility** (a length false positive in M7) and two of **director fallibility** (leniency in M4). In every case the structure — not trust in a role — contained the error. That is, in one sentence, the method.

**Complements.** To see how the method maps to different industries (marketing, real estate, IT) and a template for adapting it to any vertical, see [`docs/10-applicability-to-verticals.md`](../docs/10-applicability-to-verticals.md). The blueprint of atomic tasks that produced this document is in [`fichas-de-encargo/método-de-trabajo-con-las-fichas.md`](../../ES/fichas-de-encargo/método-de-trabajo-con-las-fichas.md) (in Spanish for now).
