# Working method — Work orders (work order for modular drafting)

> **What this file is.** The *blueprint* of the "AI Working-Method" document.
> Each work order defines an **atomic** drafting task: its scope, its boundaries
> and its acceptance criterion. The executor (Haiku 4.5) drafts **one** module per
> work order; the reviewer (Sonnet 4.6 / quality-guardian) evaluates it against the
> "Definition of done"; Opus + Human-in-the-Loop consolidate.
>
> **Framing decisions (2026-06-22):** an *outsider-first* audience; the final output =
> a single canonical `.md`; the central principle = constant evaluation of what to
> automate (hooks/skills/subagents). Hard rule: the executor **returns content, does
> not persist**; the human/director consolidates.

---

## Work order template

| Field | Function |
|---|---|
| **Purpose** | The "what for" in one line |
| **Target length** | Word range |
| **Questions it must answer** | They guide the content without writing it |
| **Must contain** | Checklist of points to cover (not closed prose) |
| **MUST NOT touch** | Explicit boundaries → keeps two modules from stepping on each other |
| **Anchor / real example** | A concrete case to cite |
| **Mistakes to avoid** | A negative list of anti-patterns |
| **Key terms** | A mini-glossary for consistency across modules |
| **Inputs** | What the executor is handed |
| **Output form** | Length, format, tone |
| **Definition of done** | The review yardstick |

---

## Work order 1 — Vision and purpose

- **Purpose:** Explain, to someone who has never seen it, *why* this AI working-method exists and what concrete problem it solves.
- **Length:** 300-450 words.
- **Questions it must answer:**
  1. What problem appears when someone collaborates with AI without structure? (loss of control, of quality, of continuity)
  2. What is the central idea that solves it? (each model in its best role by strength and cost, with a human as the final authority)
  3. What do you get in the end? (a *reproducible* method)
  4. Why does this matter more with AI than with a traditional human team?
- **Must contain:** the problem in terms for newcomers; the thesis in 1-2 sentences; a mention of the three pillars (roles, cycle, memory) without developing them; the intended result.
- **MUST NOT touch:** the operational *how* → [[Module 3]]; role detail → [[Module 2]]; memory → [[Module 4]]; automation → [[Module 6]]. No paths or internal jargon.
- **Anchor:** a high-level reference to the author's ecosystem (Remanso/ASLAN) as proof of real use, with no technical detail.
- **Mistakes to avoid:** explaining the how before the why; selling AI as a replacement for human judgment (against constraint #3); a manual tone; promising business results.
- **Key terms:** *working method*, *role*, *model*, *reproducible*, *human authority*, *continuity*.
- **Inputs:** `CLAUDE.md` (#1, #3); the project's memory notes.
- **Output form:** Markdown, `## 1. Vision and purpose`, an outsider-first didactic tone, no tables or code.
- **Definition of done:** an outside reader understands *why they would want* to use the method and there is no content from other modules.

---

## Work order 2 — Roles and responsibilities

- **Purpose:** Define what each participant (human and models) does and where their authority begins and ends.
- **Length:** 400-550 words.
- **Questions it must answer:** Who directs and why? Who executes? Who reviews? Who is the **final decision-maker**? Why is each role assigned to that model (strength vs. cost)?
- **Must contain:** Human-in-the-Loop = the single final authority that approves (constraint #1); Opus = directs, orders, pushes back, defines skeletons; Sonnet 4.6 = executes/reviews quality; Haiku 4.5 = drafts modules; a role → responsibility → "does not do" table.
- **MUST NOT touch:** the interaction *sequence* → [[Module 3]]; automation → [[Module 6]].
- **Anchor:** an executor subagent and an independent reviewer subagent as materialized roles.
- **Mistakes to avoid:** describing the temporal flow (that is M3's); presenting rigid roles without the economic/capability why.
- **Key terms:** *role*, *human authority*, *director*, *executor*, *reviewer/guardian*, *push-back*.
- **Inputs:** `CLAUDE.md` (#1, #3); the method skill; the project's memory notes.
- **Output form:** Markdown, `## 2. …`, allows a roles table.
- **Definition of done:** the reader knows whose each decision is and why.

---

## Work order 3 — The production cycle

- **Purpose:** Show the operational sequence of a task from birth to approval.
- **Length:** 450-600 words.
- **Questions it must answer:** How does a task flow? In what order do the roles intervene? Where does the "can this be automated?" checkpoint come in? What happens if the review fails?
- **Must contain:** the flow (human+Opus define the skeleton → Haiku drafts → Sonnet reviews → Opus+Human-in-the-Loop evaluate → consolidation); a simple linear diagram; the automation checkpoint as a recurring step; the rejection path (back to Haiku with feedback).
- **MUST NOT touch:** what makes a task atomic → [[Module 5]]; how to decide on automating in depth → [[Module 6]]; the definition of roles → [[Module 2]].
- **Anchor:** this very session (skeleton → work orders → Haiku) as an example in action.
- **Mistakes to avoid:** redefining roles; skipping human approval (constraint #1).
- **Key terms:** *cycle*, *skeleton*, *atomic module*, *review*, *consolidation*, *automation checkpoint*.
- **Inputs:** this session's work orders; `CLAUDE.md` (#1).
- **Output form:** Markdown, `## 3. …`, allows a diagram block.
- **Definition of done:** the reader could draw the flow and locate where the human approves and where automating is evaluated.

---

## Work order 4 — Persistent memory as a continuity asset

- **Purpose:** Explain how memory keeps the method and the context from being lost between sessions.
- **Length:** 400-550 words.
- **Questions it must answer:** Why does the AI "forget" between sessions? What is saved and what is not? How is it organized? How is what is relevant recovered?
- **Must contain:** the forgetting problem; memory types (`user/feedback/project/reference`); an index (`MEMORY.md`) + linked atomic files; what NOT to save (what is derivable from the repo, the ephemeral).
- **MUST NOT touch:** traceability via git → [[Module 9]] (memory ≠ versioning); the cycle → [[Module 3]].
- **Anchor:** the project's own `MEMORY.md` with its living files.
- **Mistakes to avoid:** confusing memory (context continuity) with git (file history); suggesting saving everything.
- **Key terms:** *persistent memory*, *continuity*, *index*, *memory types*, *recall*.
- **Inputs:** the real structure of `…/memory/`; `MEMORY.md`.
- **Output form:** Markdown, `## 4. …`, allows a types table.
- **Definition of done:** the reader understands what to note, where, and why it is not the same as git.

---

## Work order 5 — Atomicity rules (the work order)

- **Purpose:** Teach what makes an executor's task atomic and present the work order as a tool.
- **Length:** 450-600 words.
- **Questions it must answer:** What is an atomic task? How do you keep two modules from stepping on each other? What fields does a work order carry and what is each for?
- **Must contain:** a definition of atomicity (one task, a clear boundary, no hidden dependencies); the work order template; the key role of "MUST NOT touch"; a good-vs-bad split example.
- **MUST NOT touch:** the cycle flow → [[Module 3]]; how to automate → [[Module 6]].
- **Anchor:** these very 9 work orders as an applied example.
- **Mistakes to avoid:** work orders that write the content instead of bounding it; fuzzy boundaries.
- **Key terms:** *atomicity*, *work order*, *boundary*, *scope*, *definition of done*.
- **Inputs:** this set of work orders; the memory of the atomicity decision.
- **Output form:** Markdown, `## 5. …`, includes the template as a table.
- **Definition of done:** the reader can draft their own atomic work order for a new case.

---

## Work order 6 — Industrialization: when and how to automate

- **Purpose:** Give criteria to decide whether a repeated interaction should become a HOOK, SKILL, SUBAGENT, a mix or all of them.
- **Length:** 500-650 words.
- **Questions it must answer:** When is it worth automating? What does each tool solve? How to choose between them? How do they combine?
- **Must contain:** the principle of constant evaluation; what each one is and when to use it (hook = deterministic automation/enforcement; skill = invocable knowledge/convention; subagent = a role with preloaded context); a decision table (symptom → tool); the idea of combining them.
- **MUST NOT touch:** the cycle detail → [[Module 3]]; the git safety net → [[Module 9]].
- **Anchor (strong):** a real project — preamble→executor subagent; conventions→skill; manual grep→enforcer hook. One example per tool.
- **Mistakes to avoid:** automating before the pattern is clear; using a hook where a skill suffices; presenting the options as mutually exclusive.
- **Key terms:** *industrialization*, *hook*, *skill*, *subagent*, *enforcement*, *repeated pattern*.
- **Inputs:** the project's memory notes (industrialization); the method skill.
- **Output form:** Markdown, `## 6. …`, includes a decision table.
- **Definition of done:** faced with a repeated interaction, the reader knows how to choose between hook/skill/subagent and justify it.

---

## Work order 7 — Use cases / real examples

- **Purpose:** Demonstrate with concrete cases that the method works in real projects.
- **Length:** 400-550 words.
- **Questions it must answer:** Where was it applied? What result did it give? What was learned?
- **Must contain:** 1-2 developed cases (a monitoring dashboard as the main case); for each, situation → application of the method → result; one transferable lesson per case.
- **MUST NOT touch:** re-explaining concepts (already in M1–M6); technical detail that does not illustrate the *method*.
- **Anchor:** a monitoring dashboard (phases, industrialization, data honesty as a directed decision).
- **Mistakes to avoid:** turning it into the project's technical documentation; cases with no lesson.
- **Key terms:** consistent with previous modules.
- **Inputs:** the project's memory notes (state and decisions).
- **Output form:** Markdown, `## 7. …`, subsections per case.
- **Definition of done:** the reader sees the method "live" and takes away an applicable lesson.

---

## Work order 8 — Limits, and when NOT to use the method

- **Purpose:** Honestly delimit where the method adds nothing or gets in the way, so as not to apply it dogmatically.
- **Length:** 300-450 words.
- **Questions it must answer:** When is it excessive? What tasks do not justify it? What are its costs? What assumptions hold it up?
- **Must contain:** cases where the overhead exceeds the benefit (trivial, exploratory, one-shot tasks); costs (coordination time, tokens); honesty about the models' limits.
- **MUST NOT touch:** repeating advantages (M1); automation criteria → [[Module 6]].
- **Anchor:** a small task that does NOT deserve the full cycle.
- **Mistakes to avoid:** selling the method as universal; omitting costs (it breaks the honesty principle).
- **Key terms:** *overhead*, *limits*, *cost*, *proportionality*.
- **Inputs:** `CLAUDE.md` (#3, honesty); project experience.
- **Output form:** Markdown, `## 8. …`.
- **Definition of done:** the reader knows how to recognize when NOT to use the method.

---

## Work order 9 — Traceability and reversibility (the safety net)

- **Purpose:** Explain how any change is traced and how it is reverted — the 4 safety layers.
- **Length:** 450-600 words.
- **Questions it must answer:** What happens if an executor makes an unrequested change? How is it detected? How do you go back? What prevents the harm by design?
- **Must contain:** the 4 layers (Prevention / Containment / Detection / Recovery); the hard rule (the executor returns content, does not persist; the human/director consolidates); git as the Recovery layer (commits = reversible return points); the "MUST NOT touch" field as the Detection layer.
- **MUST NOT touch:** an extensive git-commands tutorial (mention, do not teach in depth); memory as continuity → [[Module 4]] (distinguish from versioning).
- **Anchor:** this very repo (`git init`, the first commit as a return point).
- **Mistakes to avoid:** confusing memory with git; proposing to encrypt/minify before committing (it kills the diffs); trusting good faith instead of design.
- **Key terms:** *traceability*, *reversibility*, *commit*, *diff*, *safety layers*, *breadcrumbs*.
- **Inputs:** the repo's git history; the 4 layers defined in this session.
- **Output form:** Markdown, `## 9. …`, allows a 4-layers table.
- **Definition of done:** the reader understands how the method protects itself from unwanted changes and how to recover.

---

## Suggested drafting order

M1 → M2 → M5 → M3 → M4 → M9 → M6 → M7 → M8.
(First the why and the roles; then atomicity before the cycle that uses it;
the continuity/safety pillars; then industrialization; and last cases and limits,
which draw on everything above.)
