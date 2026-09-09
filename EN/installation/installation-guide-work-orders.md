# Method installation guide — Work orders (blueprint)

> **What this file is.** The blueprint for deliverable **(B)**: a **step-by-step adoption
> and installation guide** for the working method. Once installed in an AI project, the
> *scaffolding* (roles, work orders, review, traceability, memory) activates **on its own
> in every new session, with no re-setup**; the human approvals stay in force. Each work
> order defines an **atomic** drafting task; the executor (Haiku 4.5) drafts **one** section
> per work order, the reviewer (quality-guardian) audits it against the "Definition of done",
> and Opus + Human-in-the-Loop consolidate and commit. The same dogfooding pipeline that
> produced the canonical guide.
>
>
> **Input common to every work order:** the canonical document
> [`docs/00-index.md`](../docs/00-index.md) (especially M4 Memory, M6 Industrialization,
> M9 Traceability).

---

## Work order template

| Field | Function |
|---|---|
| **Purpose** | The "what for" in one line |
| **Target length** | Word range |
| **Questions it must answer** | They guide the content without writing it |
| **Must contain** | Checklist of points to cover (not closed prose) |
| **MUST NOT touch** | Explicit boundaries → keeps two sections from stepping on each other |
| **Anchor / real example** | Concrete case to cite (ASLAN ground truth) |
| **Template to include** | Copy-paste skeleton the section must deliver (if applicable) |
| **Mistakes to avoid** | Negative list of anti-patterns |
| **Key terms** | Mini-glossary for consistency across sections |
| **Definition of done** | The review yardstick |

**Suggested drafting order:** F1→F2→F3→F4→F5→F6→F7→F8→F9→F10→F11→F12.
F4–F8 (piece-by-piece installation) share a fixed internal structure:
*what it does · where it lives · how to verify it activated on its own · copy-paste template*.

---

## Work order 1 — What it installs and what it guarantees

- **Purpose:** That a newcomer understands in one pass what the guide leaves installed and what it promises (and what it does NOT promise).
- **Length:** 250-350 words.
- **Questions it must answer:**
  1. What does "out-of-the-box, automatic" mean here? (the scaffolding self-activates per session; there is no manual re-setup)
  2. What stays human? (the approvals; the judgment) → explicit anti-promise: this is NOT autonomous AI.
  3. What are the 5 pieces, named without elaborating?
- **Must contain:** the honest promise in 1-2 sentences; the distinction *automatic scaffolding ≠ automatic decisions*; a list of the 5 pieces (root CLAUDE.md, memory, skills, subagents, hooks) as a preview.
- **MUST NOT touch:** how to install each piece → F4–F8; requirements → F2; the detail of what stays human → F10.
- **Anchor:** a reference to the fact that these 5 pieces already run together in a real project (ASLAN) with no re-setup between sessions.
- **Mistakes to avoid:** promising autonomy; selling it as removing supervision; a brochure tone.
- **Key terms:** *scaffolding*, *out-of-the-box*, *per-session self-activation*, *human authority*.
- **Definition of done:** the reader knows what they will have running and what they will still be deciding.

## Work order 2 — Prerequisites

- **Purpose:** List what the project must have before installing, so it does not fail halfway.
- **Length:** 200-300 words.
- **Questions it must answer:**
  1. What AI capabilities are needed? (three distinguishable ROLES: director, executor/reviewer, economical drafter)
  2. What tool/environment? (one that supports loading base context, skills, subagents and hooks)
  3. What minimum infrastructure? (a version-control repo for the Recovery layer, M9)
- **Must contain:** a verifiable checklist of prerequisites; a note that if they are missing, the method does not apply (refers to M8). **ADJUSTMENT (2026-06-24): role ≠ model — they are hats, not distinct models; there is a REDUCED version with a single model (produces in one pass, reviews in another). Access to several models grades the rigor but does NOT block getting started; the HARD requirements are the environment and version control. Do not present "3 models" as an absolute condition ("does not apply").**
- **MUST NOT touch:** the installation itself → F4–F8; the method's conceptual limits → already in M8 (only refer).
- **Anchor:** ASLAN meets all three (differentiated models, Claude Code, a local git repo).
- **Mistakes to avoid:** assuming specific tools in the generic body (that goes in Appendix F12); taking the git repo for granted.
- **Key terms:** *differentiated capability*, *version control*, *an environment with hooks/skills/subagents*.
- **Definition of done:** the reader can tick one box per requirement before starting.

## Work order 3 — Map of the 5 pieces

- **Purpose:** Give a map-table connecting each piece with the repetition it automates and when it fires.
- **Length:** 250-350 words + table.
- **Questions it must answer:**
  1. What repetition does each piece remove?
  2. When does each one activate (at session start / by context / on an event / when delegating)?
  3. Where does each piece live?
- **Must contain:** a table with columns *Piece · What it automates · When it fires · Where it lives*; a sentence noting the pieces complement each other in layers (they are not mutually exclusive); **a brief clarification (adjustment 2026-06-24): the 5 pieces are the SCAFFOLDING (the organization of the work), they do not depend on how many models you have — that is a separate matter, Prerequisites (F2). The ROLES (director/executor/reviewer) are "hats" or functions, NOT distinct models: a single model can wear several across separate passes (the reduced version). Refer to F2, without elaborating.**
- **MUST NOT touch:** the detailed templates and instructions → F4–F8; the hook/skill/subagent decision table from M6 (cite, do not reproduce whole); the detail of model requirements → F2 (only refer).
- **Anchor:** a mirror of the M6 decision table (symptom → tool).
- **Template to include:** the 5-row map-table.
- **Mistakes to avoid:** duplicating the content of F4–F8; presenting the pieces as alternatives instead of layers; **implying that more than one model is needed to use the scaffolding (a frequent confusion: the non-technical outside reader believed that "roles" = "several models").**
- **Key terms:** *auto-load*, *self-activation*, *enforcement*, *context preloading*, *role ≠ model*, *scaffolding*.
- **Definition of done:** at a glance you understand what each piece does and when it comes in; and it is clear that the scaffolding does not require multiple models.

## Work order 4 — Installation: the project's base context (`CLAUDE.md` at the root)

- **Purpose:** Install the context file that auto-loads at the start of every session (invariants, rules, constraints).
- **Length:** 300-400 words + template.
- **Questions it must answer:** what does it do? where does it live? how do I verify it loaded on its own? what do I put inside?
- **Must contain:** the four fixed sub-parts (what it does · where it lives · how to verify · template); an explanation that it goes at the ROOT of the project so it auto-loads; what kind of content goes in (objective, non-negotiable constraints, way of working).
- **MUST NOT touch:** persistent memory → F5 (CLAUDE.md is the project's static file, memory is alive between sessions); the detail of skills/subagents → F6/F7.
- **Anchor:** a real project's CLAUDE.md (objective + non-negotiable constraints + way of working).
- **Template to include:** a copy-paste base CLAUDE.md with sections: Objective, Stack/context, Non-negotiable constraints, Way of working (human approval).
- **Mistakes to avoid:** confusing CLAUDE.md (static) with memory (alive); a template tied to a specific domain.
- **Key terms:** *auto-load at session start*, *invariants*, *non-negotiable constraints*.
- **Definition of done:** the reader copies the template, fills it in, and the piece is functional.

## Work order 5 — Installation: persistent memory (`MEMORY.md` + files)

- **Purpose:** Install the memory that provides continuity between sessions (index + atomic files).
- **Length:** 300-400 words + template.
- **Questions it must answer:** what does it do? where does it live? how do I verify the AI consults it? what structure does it have?
- **Must contain:** the four fixed sub-parts; the index + thematic files structure; the four types (user/feedback/project/reference, refers to M4); what to save and what not to (refers to M4).
- **MUST NOT touch:** the full theory of memory → already in M4 (only refer, and give the how-to-install); versioning/git → F8/M9.
- **Anchor:** the ecosystem's real MEMORY.md (an index with pointers: master document, parallel projects, pending sessions, method principles).
- **Template to include:** a copy-paste MEMORY.md index + a memory-file template with frontmatter (name/description/type) and a body with `[[...]]` links.
- **Mistakes to avoid:** repeating M4's theory instead of instructing the installation; saving in memory things that already live in the code (an M4 anti-pattern).
- **Key terms:** *memory index*, *atomic file*, *frontmatter*, *continuity between sessions*.
- **Definition of done:** the reader creates their index and their first memory file following the template.

## Work order 6 — Installation: self-activating skills

- **Purpose:** Install skills the AI invokes on its own by context (the project's conventions + the method as a skill).
- **Length:** 300-400 words + template.
- **Questions it must answer:** what does it do? where does it live? how do I verify it self-activated? what makes it fire on its own?
- **Must contain:** the four fixed sub-parts; the decisive role of the `description`/triggers field (the skill activates by context match, it is not "trained"); two recommended skills: the project's conventions and the method itself.
- **MUST NOT touch:** subagents → F7; hooks → F8; the theory of when to industrialize → M6 (refer).
- **Anchor:** two real skills from a project (one with the technical + design conventions; another with the method itself), self-activated by their triggers.
- **Template to include:** a copy-paste SKILL.md: frontmatter with `name` + a `description` rich in triggers (activating phrases), and a body with the knowledge/conventions.
- **Mistakes to avoid:** saying the skill is "trained" (it is LOADED, an anti-fabrication ground truth); a poor `description` that does not fire.
- **Key terms:** *context self-activation*, *triggers*, *a skill is loaded, not trained*.
- **Definition of done:** the reader writes a skill whose `description` makes it activate on its own in the right context.

## Work order 7 — Installation: preloaded subagents

- **Purpose:** Install subagents with a role and preloaded context (an executor with invariants + a quality-guardian reviewer).
- **Length:** 300-400 words + template.
- **Questions it must answer:** what does it do? where does it live? how do I verify it brings the context without re-pasting it? what do I configure?
- **Must contain:** the four fixed sub-parts; the two core subagents (an executor with invariants; an independent quality reviewer); how the subagent removes the re-pasting of the preamble (refers to M2 roles and M6 subagent).
- **MUST NOT touch:** skills → F6; hooks → F8; the theory of roles → M2 (refer).
- **Anchor:** two real subagents from a project: an executor (with preloaded invariants) and an independent reviewer.
- **Template to include:** a copy-paste subagent .md: frontmatter (name, description, tools, model) + a body with the role, the invariants, and the hard rule "returns content, does not persist".
- **Mistakes to avoid:** letting the executor persist files (it breaks M9's Prevention layer); reviewer = executor (they must be independent, M2).
- **Key terms:** *context preloading*, *executor*, *independent reviewer*, *the reviewer one level above the executor*.
- **Definition of done:** the reader creates an executor subagent and a reviewer one without re-pasting preambles.

## Work order 8 — Installation: enforcement hooks

- **Purpose:** Install deterministic hooks that enforce rules and block violations with no intervention.
- **Length:** 300-400 words + template.
- **Questions it must answer:** what does it do? where does it live? how do I verify it really blocks? which rule do I automate first?
- **Must contain:** the four fixed sub-parts; the distinction pre-event (PreToolUse, blocks before) vs post-event (PostToolUse, validates after); that hooks are for objective rules that must NEVER be broken (refers to M6); their role as a Detection/Recovery layer (refers to M9).
- **MUST NOT touch:** the exact registration syntax in `settings.json` → Appendix F12 (the body is generic); skills/subagents → F6/F7.
- **Anchor:** two real hooks from a project: one for enforcement (blocks patterns that violate the invariants) and one for telemetry (always exit 0, never blocks).
- **Template to include:** a copy-paste hook skeleton (reads the event from stdin, evaluates the rule, exit 2 = blocks / exit 0 = allows) — generic, with the concrete wiring deferred to the Appendix.
- **Mistakes to avoid:** a hook that blocks on a false positive (e.g. matching inside comments — a real ASLAN lesson); putting subjective rules in a hook (that is a skill).
- **Key terms:** *enforcement*, *deterministic*, *PreToolUse/PostToolUse*, *the blocking exit code*.
- **Definition of done:** the reader installs a hook that blocks an objective violation in a real test.

## Work order 9 — Verifying the installation

- **Purpose:** Give a checklist to confirm, in a new session, that each piece activates on its own.
- **Length:** 250-350 words + checklist.
- **Questions it must answer:**
  1. How do I confirm CLAUDE.md auto-loaded?
  2. How do I confirm a skill self-activated by context?
  3. How do I confirm a subagent brings its context?
  4. How do I confirm a hook really blocks?
  5. How do I confirm memory provides continuity?
- **Must contain:** an actionable checklist (open a fresh session → observe each piece's signal); the idea of "verify, don't trust" applied to the installation (M3).
- **MUST NOT touch:** the installation → F4–F8 (this only verifies); maintenance → F11.
- **Anchor:** in ASLAN, a production test revealed and fixed 2 bugs (colliding identities; elements that did not expire) — verifying live catches what the design does not anticipate (M7).
- **Template to include:** the verification checklist (one box per piece).
- **Mistakes to avoid:** assuming a piece is installed without observing it activate; a non-verifiable checklist ("it should work").
- **Key terms:** *verify, don't trust*, *fresh session*, *activation signal*.
- **Definition of done:** the reader runs through the checklist and knows whether the installation came out alive.

## Work order 10 — What stays human

- **Purpose:** Honestly delimit what is NOT automated, so as not to promise autonomy.
- **Length:** 200-300 words.
- **Questions it must answer:**
  1. Which decisions still require human approval? (consolidating, publishing, risk decisions)
  2. Why is that control preserved? (human authority, M2; the prior-approval constraint)
- **Must contain:** a list of the human checkpoints the scaffolding does NOT replace; the key phrase: the assembly is automated, not the judgment; refers to M8 (limits) and M2 (human authority).
- **MUST NOT touch:** the installation steps → F4–F8; the verification → F9.
- **Anchor:** the constraint that "every action is planned and approved by the human before execution" as a non-negotiable contract.
- **Mistakes to avoid:** suggesting that with everything installed the AI decides on its own; minimizing the human role.
- **Key terms:** *human authority*, *prior approval*, *automatic assembly ≠ automatic judgment*.
- **Definition of done:** it is unambiguous what the human decides even with everything installed.

## Work order 11 — Maintenance: when to add a new piece

- **Purpose:** Teach how to grow the scaffolding by applying the industrialization checkpoint recurrently.
- **Length:** 200-300 words.
- **Questions it must answer:**
  1. How do I detect that a new repetition deserves automating? (2-3 cycles, M6)
  2. Which piece do I choose by symptom? (repeated context → subagent; convention → skill; hard rule → hook)
- **Must contain:** the "2-3 cycles before industrializing" criterion (neither premature nor late, M6); the recurring checkpoint (M3); a reference to the M6 decision table.
- **MUST NOT touch:** reproducing the whole M6 table (refer); the initial installation → F4–F8.
- **Anchor:** in ASLAN, a recurring and predictable failure (an internal proper name) was identified as a hook candidate — dogfooding feeds the improvement of the scaffolding itself.
- **Mistakes to avoid:** industrializing on the first cycle (premature); waiting for the chaos to grow (late).
- **Key terms:** *automation checkpoint*, *2-3 cycles*, *symptom → tool*.
- **Definition of done:** the reader knows how to recognize and choose the next piece to install.

## Work order 12 — Appendix: realization in Claude Code

- **Purpose:** Land the 5 generic pieces in the concrete tool (Claude Code), with the real wiring.
- **Length:** 350-500 words + concrete templates.
- **Questions it must answer:**
  1. Where does each piece physically go in Claude Code? (root `CLAUDE.md`, `.claude/skills/`, subagents, hooks, `settings.json`)
  2. How is a hook registered in `settings.json` (a PostToolUse/PreToolUse matcher)?
  3. How is a subagent invoked and how does a skill self-activate?
- **Must contain:** the correspondence generic-piece → Claude-Code location; the hook-registration block in `settings.json` (matcher Edit|Write, command); a note that hooks usually take effect at the start of a new session; the hook convention (the event on stdin, tolerate the BOM, exit 2 blocks / exit 0 allows).
- **MUST NOT touch:** the generic theory of each piece → F4–F8 (here only the realization); do not re-explain what each piece is for.
- **Anchor:** the real pieces of a project in the environment's configuration folder (executor/reviewer subagents, a conventions skill, enforcement/telemetry hooks registered in `settings.json`).
- **Template to include:** a copy-paste `settings.json` block (registration of a PostToolUse hook) + the `.claude/` folder structure + real subagent and skill frontmatter.
- **Mistakes to avoid:** mixing the realization into the generic body; inventing paths or syntax (use the verified ASLAN ones as ground truth).
- **Key terms:** `.claude/`, `settings.json`, *matcher*, *PostToolUse/PreToolUse*, *exit 2*.
- **Definition of done:** a Claude Code user copies the appendix and leaves the 5 pieces operational.

---

## Production pipeline (an operational reminder)

For each work order: **drafting** via a general-purpose subagent with `model=haiku`, a
self-contained prompt with the work order + the ASLAN ground truth + the hard rule "return
content, do not write files" → **review** with `quality-guardian` (Sonnet) field by field →
correction if there are findings → **consolidation** by Opus into `installation-guide.md` +
commit. Every reviewer catch is poured into a dogfooding log (a project convention). If a
re-audit relapses into a 🔴 blocking finding, it escalates to a Sonnet 4.6 executor + an Opus
auditor (assurance proportional to severity).
