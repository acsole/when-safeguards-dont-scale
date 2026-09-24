# Method adoption and installation guide

> Canonical document of the **installation guide**. Audience: outsider-first
> (didactic for someone who has never seen it). A **generic/portable** body — the 5
> pieces as concepts applicable to any AI environment — plus an **Appendix** with the
> concrete realization in Claude Code. Built section by section following the blueprint
> in [`installation-guide-work-orders.md`](installation-guide-work-orders.md), with the
> same dogfooding cycle that produced the method: drafting → review (quality-guardian) →
> consolidation and commit.
>
> **Status:** COMPLETE — the 12 sections consolidated.

---

## 1. What it installs and what it guarantees

This guide installs a **scaffolding for collaborative work between humans and AI**, not an autonomous system. Once configured, it **self-activates per session**: in every new conversation the scaffolding starts on its own, with no manual re-setup, but the decisions stay yours.

### The promise: out-of-the-box, no surprises

You install once. From the next session on, the scaffolding is alive: roles defined, persistent memory recovered, skills ready, subagents preloaded, execution rules active. You do not reinvent the wheel in every conversation. But here is what matters: **the scaffolding is automatic; the decisions are not**. The human authority is still the one who approves what matters before it is executed.

### The five pieces (preview)

1. **A base context file at the project root** — what the project is, its conventions and constraints; it loads at the start of every session.
2. **Persistent memory** — the project's living context, kept between sessions.
3. **Self-activating skills** — bodies of knowledge the AI invokes on its own when the context warrants it.
4. **Preloaded subagents** — specialized roles (executor, reviewer) ready without rebuilding the context every time.
5. **Enforcement hooks** — deterministic rules that run on their own on an event and block what must not happen.

Each piece is installed and verified in its own section later on; here they are only named.

### What this guide does NOT guarantee

It does not automate *judgment*. It does not replace supervision. It does not make the AI the owner of the project. What it does do is remove operational friction: fewer repeated questions, less context lost between sessions, less "what was I doing here?". It is scaffolding, not autopilot.

This is not theory: a real project in production — a multi-project monitoring dashboard — already runs with the five pieces together, across many sessions, with zero re-setup. Each session starts better informed because the context lives on; each decision stays human.

---

## 2. Prerequisites

Before installing the scaffolding, check these three fronts. Two are hard requirements (the environment and version control); the third — access to models — grades the rigor but does not prevent starting, as explained below.

### Access to models of differentiated capability

The **complete** method takes advantage of **at least three distinguishable AI roles**:

- A **director role** with higher reasoning, capable of complex planning, synthesis and strategic validation.
- An **executor/reviewer role** of mid capability, suited to implementation, code search and iterative improvement.
- An **economical drafter role**, fast and efficient, for low cognitive-cost tasks (synthesis, formatting, documentation).

An important point: **these are roles, not necessarily distinct models** (see also the Map of the 5 pieces). The ideal is to assign each role to the model that best exploits it, and to have the reviewer be independent of whoever produced. But **there is a reduced version with a single model**: the same model produces in one pass and critically reviews in another. It is weaker than having an independent reviewer, but far superior to a single pass with no review. In short: with one model you can already start; adding differentiated models is scaling the rigor, not a requirement to begin.

### An environment with integral support

Your AI tool or platform must allow you to:

- **Load base context automatically** in every new session (with no manual re-setup).
- **Define and activate skills** according to operational need.
- **Delegate to subagents**.
- **Run enforcement hooks** (validations, rules before/after actions).

### Operational version control

The project must have **a version-control system** to:

- Track changes to base context and memory.
- Guarantee recovery of previous states.
- Audit decisions and the traceability of tasks.

### Verification checklist

- [ ] I have access to at least one AI model (ideally several, of differentiated capability, for the complete method).
- [ ] My environment supports automatic base context, skills, subagents and hooks.
- [ ] The project uses an active version-control system.

The environment and version control are hard requirements: without them, the automatic scaffolding cannot be installed. Access to several models, by contrast, grades the rigor, it does not block starting: with a single one you run the reduced version. To understand when the method is simply not the right choice, see the module "Limits, and when not to use the method" in the method document.

---

## 3. Map of the 5 pieces

The scaffolding for working with AI rests on five structural pieces, each automating a different kind of repetition and solving a specific problem of the development cycle: how to keep context between sessions, how to reuse knowledge without rewriting it, how to delegate roles precisely, and how to guard critical rules. The following table shows what problem each one solves, when it comes into play, and where it lives in your working infrastructure.

| Piece | What it automates | When it fires | Where it lives |
|-------|---|---|---|
| **Base context at the root** | Remembering the project's objective, rules and constraints in every session | At session start (auto-load) | A configuration file in the project's root folder |
| **Persistent memory** | Rebuilding the context accumulated between sessions (prior decisions, state, lessons) | At the start of, or during, the session | Memory files: a master index + thematic files per area |
| **Self-activating skills** | Repeating a body of knowledge, convention or protocol without rewriting it | By context, when the environment recognizes it applies | Declared as skills in the working environment |
| **Preloaded subagents** | Re-pasting the same preamble and specialized context when delegating tasks | When delegating to a specific role (director, executor, reviewer, auditor) | Subagent definitions registered in the environment |
| **Enforcement hooks** | Objectively verifying that a critical rule (security, brand, data) is met | Before or after a key action (save, publish, delegate) | Scripts registered in the environment |

These five pieces **are not mutually exclusive alternatives, but layers that work together**. The base context arrives first, setting the compass; memory enriches it with accumulated learning; skills contextualize it by task; subagents inherit it when they receive a delegation; hooks guard it before it crosses the exit door. Each layer adds value to the previous one, it does not replace it.

The order in which they come in usually matters, but as reinforcement, not as a rigid dependency: the base context anchors memory; memory gives history to skills; skills bring knowledge that subagents inherit; and hooks guard the final result. Even so, **each piece adds value on its own**: a hook can verify an objective technical rule even with no subagents, and skills add value even before any accumulated memory exists. You can install one, some or all of them; adding the missing ones is scaling, not a requirement to start.

An important clarification: **the scaffolding is the *organization of the work*, not a question about the quantity or type of models**. The five pieces work with a single model or with several; the how-many and the which of models is the responsibility of the *Prerequisites* section. The roles (director, executor, reviewer, auditor) are *hats* or functions the same model can wear across separate passes, not distinct models. A single model can produce content in one pass, review it critically in another, and execute a change in a third, without that requiring three different models. Well-built scaffolding stays agnostic to the number of agents that occupy it: if later you decide to add more models or specialized subagents, the structure scales with no redesign.

---

## 4. Install the base context file (at the project root)

Every project needs a base context file that lives at the root and auto-loads at the start of every session (in each tool this file has an agreed name that the tool loads on its own; see the Appendix). This ensures that everything operates under the same invariants and that the AI always has the full map before any conversation.

### What it does

The file gives the AI: the project's objective; the technologies, environment and non-negotiable constraints; the working protocol (the AI proposes a plan and waits for explicit approval before executing); brand, security or data rules that can never be violated; and how the AI collaborates with the human (a technical assistant that augments judgment, it does not replace it). It is also worth fixing who has authority to approve changes and by what criterion one task is prioritized over another, so that criterion does not depend on the memory of whoever is running the session. It is STATIC: it defines the rules that do not change, unlike persistent memory, which is alive and changes between sessions (see the memory section).

### Where it lives

At the ROOT of the project, because from there the tool detects it and auto-loads it at the start of every session, without having to ask for it or paste it. The file is readable and versioned in version control, so any change to the project's rules is recorded like any other relevant change, with its own history and its own traceability. This also allows that, if the project grows or branches, each branch can inherit the same base context file without duplicating criteria.

### How to verify it activated on its own

In a new session, ask the AI about a constraint or invariant that only exists in your context file (e.g. "how should I propose changes before executing them?"). If it answers without your having pasted it in, it loaded. If not, check that the file is at the root and with the name the tool expects (see the Appendix).

### Base template

```markdown
# Project base context: <project name>

> This file is loaded automatically at the start of every session.
> It defines the objective, the stack, the constraints and the way of working.

## Objective
Explain in 2-3 sentences: what is the project? What is it trying to achieve?

## Context / stack
Technologies, environment, data and references the AI must always know.

## Non-negotiable constraints
1. The AI proposes a plan and waits for explicit approval before executing.
2. Deny by default: only explicitly authorized people have permissions.
3. Never compromise <ethical rule or data limit of the domain>.

## Way of working
- The AI proposes, <responsible human> approves.
- The identity of the active task on every deliverable.
- Validation before moving on to the next task.
```

---

## 5. Install persistent memory

### What it does

While the base context file (Section 4) is static and holds the project's architecture and invariant rules, persistent memory is the living complement that changes between sessions. It stores the context that evolves: decisions made, agreements established, the project's current state, lessons captured, and any information the AI needs to pick up again without starting from zero. Thanks to this memory, each new session starts with continuity: the AI accesses the index, knows what happened in the previous session, and can propose or execute knowing where the work stood. For the full theory of persistent memory and its role in the working cycle, see the method document.

### Where it lives

Memory lives in two complementary places within the project: a central index file (the concrete name depends on the tool; see the Appendix) that lists all memory topics, and a collection of atomic thematic files (one per topic: one for decisions, another for state, another for lessons, etc.). The index is the "map" the AI consults first; the atomic files hold the detail. This separation keeps memory readable and easy to update.

### How to verify the AI consults it

In a new session, ask the AI about a fact or decision that lives ONLY in memory (not in code files or published documentation). For example: "*What was the last decision we made about X?*" If the AI answers correctly, it confirmed that it read the index. If it does not remember, check that the index is at the correct path and that the AI has read permission.

### What structure it has

Memory organizes four types of information (detail in the method document):

- **User**: profile, preferences, working style, constraints.
- **Feedback**: accumulated observations and corrections (what worked, what did not).
- **Project**: current state, milestones reached, key decisions, pending tasks.
- **Reference**: links to resources, external references, third-party context.

**What to save and what NOT to:** save facts that change between sessions and that the AI must know. Do NOT save in memory what already lives in the project's code, in a repository, or in published documentation (that is memory noise).

### Templates

**Template 1 — Memory index file:**

```markdown
# Memory index — <project name>

## User
- [<title>](<file>.md) — <one-line summary>

## Feedback
- [<title>](<file>.md) — <one-line summary>

## Project
- [<title>](<file>.md) — <one-line summary>

## Reference
- [<title>](<file>.md) — <one-line summary>
```

**Template 2 — Atomic memory file:**

```markdown
---
name: <short-slug>
description: <one-line summary to decide whether to read it in full>
type: user | feedback | project | reference
---

# <Descriptive title>

<The concrete fact or context. Develop it in readable paragraphs.>

**Why:** <Why this matters; what would happen without this information>

**How to apply it:** <The concrete action the AI must take when it reads this>

**Related links:** [[<file>]], [[<file>]]
```

> A note on convention: the readable headers can go in your language (User, Feedback, Project, Reference), but the value of the `type` field stays in English (`user | feedback | project | reference`) because it is a technical label.

---

## 6. Install self-activating skills

### What it does

A self-activating skill is a store of knowledge, conventions or procedures the AI invokes automatically when the context matches, without your having to ask for it explicitly. Instead of repeating instructions by hand in every session, you declare a skill that encapsulates that body of know-how: the team's working method, the project's conventions, a validation checklist, a communication protocol, a formatting standard. The AI reads it when it applies and applies it without your having to remind it.

### Where it lives

A skill is declared as a file in the working environment (the concrete format and location depend on the tool; see the Appendix). It generally contains:

- A **declarative header** (the skill's metadata: name, description).
- A **body of knowledge**: the conventions, steps, rules or examples the skill encodes.

### How to verify it self-activated

In a task that should trigger the skill, observe that the AI **applies the conventions or procedures without your having reminded it**. For example, if you declared a skill about "document formatting standards", and the AI generates a document respecting those standards without your having asked for it in that dialogue, the skill activated correctly. Another indicator: the AI explicitly mentions that it is applying a convention or protocol from the skill.

### What makes it fire on its own

The heart of a self-activating skill is its **description field**. That field must be **rich in triggers** (situations, keywords, contexts that make the AI recognize it and apply it). If the description is generic or vague, the skill does not fire. A strong description explicitly enumerates when it is used: "Activate when the user mentions X, Y or Z"; "Apply if the task involves procedure P"; "Invoke whenever a document of type Q is written".

**Critical point:** the skill is **LOADED**, it is not "trained" or "learned". It does not adjust weights; it is a block of information the AI consults when it identifies the trigger. The quality of the load depends on how clear and specific the description is.

**Recommendation:** install TWO skills first:

1. One that encodes **the project's conventions and constraints** (what is allowed and what is not; tones; formats; key decisions).
2. One that encapsulates **the AI working-method itself** (how you plan, how you validate, what role each part takes, how they collaborate).

These two stores reduce friction drastically: the AI already "knows" how you operate without your repeating it every time.

### Generic skill template

```
---
name: <skill-slug>
description: |
  Activate when: <situation 1> is mentioned; the user writes <keyword>; the task involves <context>;
  a document of type <doc type> is written; questions about <topic> come up; the user uses the
  marker [<command>]; a session of <activity> begins.
---

# <Readable skill name>

## <Convention 1>

<Description of the convention, rule or procedure. Be specific; include examples if it helps.>

## <Convention 2>

<Description.>

## <Checklist / Steps>

- Step 1: <description>
- Step 2: <description>
- Step 3: <description>
```

---

## 7. Install preloaded subagents

### What it does

A subagent is a delegated role that **is born with the context already loaded**: you do not need to re-paste the full preamble every time you invoke it. It is like having a specialist on your team who already knows the project's invariants, the quality standards and the rules of how you work, without your having to remind them on every task.

When you delegate to a subagent, it automatically respects your conventions — because it knows them in advance — and you gain speed by not having to repeat "here are our rules again".

### Where it lives

Subagents are defined as entries in your working environment's configuration (the exact location and format depend on the tool; see the Appendix). Each definition includes: a name, a description of when to use it, the role it plays, and the preloaded context (invariants, conventions, hard rules). Once installed, they appear as available options when delegating.

### How to verify it brings the context without re-pasting it

The clearest test is **to delegate a task without reminding it of the invariants and see that it respects them anyway**. For example: if your rule is "return content, do not write files", you delegate a task without mentioning that rule, and the subagent still returns its answer in the chat without writing files, then the preload works.

### What I configure

You configure **two core subagents**: an **executor** and an **independent reviewer**.

The **executor** carries your project's invariants and conventions (data accuracy, tone of voice, the prevention rule, etc.). It receives operational tasks: writing, analyzing, implementing. **Hard rule: it returns the content in its reply; it does not write or persist files.** That prevents an error of its from overwriting real data.

The **reviewer** is independent of the executor and runs one level above it in capability. It reviews the executor's output against fixed criteria (correctness, integrity, alignment with your voice, absence of invented data). It is the one that gives the go-ahead or detects friction before it reaches you.

For the full theory behind these two roles — why they are separated and why the reviewer scales with severity — see the method document.

### Subagent template

```markdown
---
name: <subagent-name-slug>
description: "When to delegate to it. E.g., 'Brand content drafter'"
model: <a-model-of-capability-suited-to-the-role>
tools: <generic-read-and-analysis-access>
---

## Role

You are a <specific role> specialized in <domain>. Your responsibility is <concrete task>. You are not the one who decides; you are the one who delivers raw material for the human to decide.

## Preloaded invariants

- Data accuracy: never include unverified information.
- **Hard rule: return the content in your reply; do not write or persist files.**
- Respect the project's tone and formatting conventions.
- When in doubt, ask before moving forward.

## When to ask

- A critical fact is missing.
- The task crosses a line of the rules.
- The intent of the request is not clear.
```

---

## 8. Install enforcement hooks

### What it does

An enforcement hook is a deterministic script that runs automatically on an event and can **block the action** if it detects a violation of an objective, verifiable rule. It is the most restrictive layer of the scaffolding: it activates for rules that must NEVER be broken, with no human intervention at the moment (for the criterion of when it is worth industrializing a rule into a hook, see the method document). It operates with binary logic: it evaluates the condition and returns an exit code that determines whether the action proceeds or stops.

### Where it lives

The hook is registered as a script in the project environment's configuration (the concrete directory, execution language and registration format are in the Appendix). The registration defines: what event fires it, the path to the script, and the expected exit codes (block vs. allow). Once registered, it is invoked automatically every time the event occurs, without the user doing anything else.

### How to verify it really blocks

Reviewing the hook's code is not enough: you have to deliberately provoke a violation of the rule and confirm the hook stops it. That is, create a concrete test case (for example, trying to add a credentials file), run the action normally, and verify that the hook rejects it with a clear error message. If it does not block in the test, there is a defect in its logic or configuration.

### Which rule do I automate first

Start with an **objective and verifiable** rule: for example, *blocking the inclusion of credentials files* (names matching patterns like `.env`, `secrets.json`, `password.txt`). It is deterministic: the hook examines each pending file, applies a pattern, and decides unambiguously.

A **pre-event** hook runs *before* the action and can block it (a blocking exit code). A **post-event** hook runs *after* and validates or logs (useful for auditing, not for prevention). Choose pre-event for rules that tolerate no exceptions.

**Design warning:** a badly written hook produces false positives (e.g. detecting the word `password` inside a comment, not in a real credentials file). Use strict logic. *Subjective* rules (e.g. "the commit message must be clear") **do not go in a hook**: that is a skill. Hooks protect mechanical boundaries, not intent.

The hook acts as a **Detection and Recovery** layer (see the method document): it stops the error before it penetrates and forces an immediate correction.

### Hook template

```bash
#!/bin/bash
# Generic pre-event hook.
# Reads the incoming event, evaluates the rule, exits with the appropriate code.

while read <pending_file_or_change>; do
    # Does the file/change violate the objective rule?
    if [[ <pending_file_or_change> =~ <violation_pattern> ]]; then
        echo "BLOCK: rule violated. Detail: <clear_message>"
        exit <blocking_exit_code>
    fi
done

# No file/change violates the rule.
exit <OK_exit_code>
```

*(The concrete exit codes, the registration format and the event names are in the Appendix.)*

---

## 9. Verify the installation

The installation is complete only when each piece *activates on its own* in a new session. It is not about it "should work" by design: it is about *observing* that it works, with no manual intervention. This is the principle of **"verify, don't trust"** applied to the configuration. Open a **fresh session** (a new conversation with the AI, in the same environment) and run through the checklist below. Each piece has an identifiable **activation signal**: that is what you are looking for.

The signals are these. (1) The **base context** activated when the AI mentions a constraint or rule that exists only there, without your having pasted it into the message. (2) **Memory** activated when the AI remembers a detail of a decision or a fact recorded only in persistent memory. (3) A **skill** activated when the AI applies a convention, a style or a protocol from that skill without your reminding it. (4) A **subagent** activated when it brings its own invariants along without your having repeated them in your request. (5) A **hook** activated when it stops or rejects an action you provoked on purpose to violate a rule.

Live verification is critical. In a real project in production, a direct test in the field revealed gaps between the theoretical design and what happens in practice: errors that static review did not anticipate. Verifying live is what catches that — it is the stage the method itself reserves as the final net (see the method document). No matter how clean the installation is on paper; in production, reality rules.

**Verification checklist:**

- [ ] The base context is alive: the AI mentioned a rule or constraint without your repeating it.
- [ ] Memory works: the AI remembered a detail of a previous recorded decision.
- [ ] A skill activated: the AI applied a convention or protocol from the skill with no reminder.
- [ ] A subagent operated with its context: it brought its own invariants to the work.
- [ ] A hook blocked a violation: it stopped the action you provoked on purpose.

---

## 10. What stays human

With everything installed and running, it may seem the AI makes the decisions. It does not. The method preserves human authority at every critical point.

**What still requires human approval?**

Although the AI assembles proposals, plans and drafts, the human is still the one who decides:

- **Approving plans before executing.** The AI proposes; the human approves. No action proceeds without explicit confirmation.
- **Consolidating changes into final files.** The AI generates; the human reviews, adapts and writes to the master files. That ensures what remains is what the human wanted, not what the AI produced.
- **Publishing outward.** Before any content sees the light of day (a publication, a send, a post), the human runs it through their own voice, judgment and criterion. It is their signature at the end.
- **High-risk or irreversible decisions.** Deleting data, changing critical configuration, modifying policies, making decisions that affect third parties: all of that stays with the human.
- **Strategic or ethical decisions.** What gets published, for whom, with what purpose. How a dilemma between speed and accuracy is handled. When to stop a process. That is irreducibly human responsibility.

**The rule that sums it up:** the assembly is automated, not the judgment. The AI speeds up the work; the human is still the one who decides.

Why? Because human authority is the center of the method. The AI augments the human's capability, it does not replace it. The fundamental contract is non-negotiable: every action is planned and approved by the human *before* execution. That does not change with scale or with the years.

For the underlying theory on human authority and the method's real limits, see the method document.

---

## 11. Maintenance: when to add a new piece

The scaffolding is not static. As the work evolves, patterns appear that repeat: instructions you give the same way every time, decisions you resolve with the same criterion, or predictable failures that happen at the same point. Detecting them and turning them into new pieces is the real maintenance of the system.

The **2-3 cycle criterion** protects you from two equally costly extremes: automating too soon (while you are still changing your mind) and letting inefficiency accumulate (when the pattern is already entrenched). If something happens exactly the same way two or three times, that is a sign it deserves to be captured; before that it is premature; much later, the cost of fixing it is already high.

The key question is: **what is the symptom?** The symptom tells you which piece to use:

- **You repeat the same context or preamble** every time you delegate a task → **subagent**. The piece carries the pre-built context; the agent executes with it.
- **There is a body of conventions or rules** you always apply in a domain → **skill**. It condenses the "how we work here" and makes it reusable.
- **An objective rule that must NEVER be broken**, whose breach is a recurring and predictable failure → **hook**. It runs automatically; it does not depend on memory.

This automation checkpoint is not a one-off: it repeats. Every so often (or when you notice something repeating), you evaluate again. The very use of the method feeds its growth: the patterns that emerge from daily work are the raw material of the new pieces.

For the full decision table and examples of each piece, see the method document.

---

## 12. Appendix: what it looks like in Claude Code

The method's five pieces are not abstractions: in Claude Code each one is realized in a concrete file or configuration entry, which the tool discovers and applies on its own from the first session. This appendix maps each piece to its exact place and shows the real syntax for registering a hook, so you can copy and adapt without guessing. The example file names are illustrative: replace them with your own.

### Correspondence table

| Generic piece | Location in Claude Code |
|---|---|
| Base context file | `CLAUDE.md` at the project root |
| Persistent memory | a `MEMORY.md` index + thematic files (e.g. under `.claude/memory/`), versioned in git |
| Skills | `.claude/skills/<skill-name>/SKILL.md` (frontmatter `name` + `description` with triggers) |
| Subagents | `.claude/agents/<name>.md` (frontmatter `name`, `description`, `tools`, `model` + a body with the role and invariants) |
| Hooks | a script (e.g. `.claude/hooks/<name>.js`) registered in `.claude/settings.json` |

Each location respects the logic of the previous sections: the base context auto-loads, skills self-activate by their `description`, subagents are invoked when delegating, and hooks fire on events. It is all plain text and versioned in git, so cloning the repository reinstalls the whole scaffolding.

### Registering a hook in `settings.json`

A hook is a script plus its registration. The `hooks` key is an object indexed by event (`PreToolUse` can block before the action; `PostToolUse` validates after). Each entry carries a `matcher` (which tools fire it) and a `hooks` array with the command to run:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          { "type": "command", "command": "node .claude/hooks/block-secrets.js" }
        ]
      }
    ]
  }
}
```

The script receives the event as JSON on stdin; the tool's input arrives under `tool_input`:

```javascript
#!/usr/bin/env node
const event = JSON.parse(require('fs').readFileSync(0, 'utf-8'));
const filePath = event.tool_input?.file_path || '';
const content = event.tool_input?.content || '';

if (/secret|api[_-]?key|password/i.test(content) && filePath.includes('config')) {
  console.error('Rejected: credentials cannot be saved in config files.');
  process.exit(2); // blocks the action
}
process.exit(0); // allows the action
```

**Exit-code convention:** `exit 2` blocks (the `stderr` is shown to the model so it can correct); `exit 0` allows.

### When they become active

Claude Code reads `.claude/settings.json` **at the start of the session**: from that moment the hook is active and fires on every event that matches (every `Edit`/`Write`, in the example), with no manual invocation — it does not run once when you open, but on every action that matches. The same holds for the rest: on startup, the tool discovers the available skills (by folder under `.claude/skills/`), the invocable subagents (by file under `.claude/agents/`) and the base context (`CLAUDE.md`). That self-detection at startup is what turns the installation into living scaffolding, not a "one-time setup".

### Illustrative folder structure

```
my-project/
├── CLAUDE.md
├── MEMORY.md
└── .claude/
    ├── settings.json
    ├── skills/
    │   └── project-conventions/SKILL.md
    ├── agents/
    │   ├── executor.md
    │   └── reviewer.md
    ├── hooks/
    │   └── block-secrets.js
    └── memory/
        ├── key-decisions.md
        └── pending.md
```

---

## Appendix A — Dogfooding log (incident record)

> This guide is built by using itself. Each section is drafted by an economical
> executor and audited by an independent reviewer (quality-guardian) before human
> consolidation. This log records every incident caught in review: what was detected,
> its severity, how it was resolved and why it mattered.

### Section 1 — What it installs and what it guarantees · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**Reviewer's verdict: PASS** (265 words, in range). No blockers. Improvements applied by the director on consolidation:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 1.1 | Piece 3 (skills) carried a parenthetical example "document progress" — it matches a plausible, real skill name; it could read as an installed feature | 🟡 Improvement | Example removed; the piece stayed as a pure preview | The work order asked to name the 5 pieces "without elaborating on them"; a concrete example is already elaboration and risks confusing illustration with fact |
| 1.2 | Piece 5 (hooks) carried a parenthetical example "verify before pushing" — same pattern | 🟡 Improvement | Example removed; pure preview | Same as 1.1; consistency with the "preview only" mandate |
| 1.3 | The human side was developed in 3 sentences (a list of 4 verbs) when the work order asked only for a 1-2 preview | ⚪ Minor | Trimmed to one sentence ("approves what matters before it is executed"); the detail is reserved for its section | Avoids exhausting content that belongs to the "What stays human" section (duplication across sections) |
| 1.4 | The key term "per-session self-activation" did not appear literally | ⚪ Minor | Incorporated literally ("it self-activates per session") | Terminological consistency across the document's sections |

**Lesson / calibration:** the drafter tends to **over-illustrate** (add unrequested concrete examples) even when the work order asks for a pure preview. The examples were correctly marked with "e.g." and did not falsify the ground truth — the reviewer acknowledged it — but they invaded the scope of later sections. Antidote: the "MUST NOT touch / without elaborating" boundary applies to examples too, not just to statements.

### Section 2 — Prerequisites · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**Reviewer's first return: REJECTED** — two blockers:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 2.1 | Named the concrete tool "Git" in the body ("Git or equivalent") | 🔴 Blocking | Replaced with "a version-control system"; the concrete name is reserved for the Appendix | The body is generic/portable; tool names go in the Appendix (the work order's "MUST NOT touch" boundary) |
| 2.2 | Omission of the mandatory reference to the method's limits | 🔴 Blocking | Added a nominal reference to the module "Limits, and when not to use the method" in the method document | The work order asked for it explicitly; without it, the reader does not know where "when it does not apply" is developed |
| 2.3 | A sentence with a brochure tone ("a real project in production proves it…") | 🟡 Improvement | Replaced with a neutral statement about the replicability of roles | The work order forbids a brochure tone; the anecdotal case was not requested |
| 2.4 | Detail of the skills/subagents mechanism (a requirement is not a manual) | 🟡 Improvement | Simplified; the director also trimmed the vestige "with inherited context" on consolidation | The level of detail exceeded a requirements checklist |

**Re-audit: PASS** (231 words, both blockers resolved, no new findings). Escalation NOT triggered: being the first return, the drafter kept its round and was corrected in one pass.

**Lesson / calibration:** two already-catalogued failure modes reappeared from the method's own production — **leak of a concrete name into the generic body** (akin to the "over-illustrating" of Section 1) and **omission of a mandatory element of the work order** (the reference). It confirms that the "Must contain" field works as a verifiable checklist: the reviewer runs through it point by point and the omission jumps out.

**Later amendment (2026-06-24, by decision of the human authority):** while drafting Section 3 it was detected that this Section 2 presented "three models" as an absolute condition ("otherwise, the method does not apply"), which **contradicted** the *role ≠ model* principle and the reduced version with a single model. It was reformulated: the roles are hats (not distinct models); access to several models **grades the rigor but does not block starting**; the hard requirements are the environment and version control. It is a case of **cross-section consistency** visible only when a later section puts tension on an earlier one — the living document corrects itself.

### Section 4 — Base context file · 2026-06-24 · SECOND ACTIVATION OF THE ESCALATION RULE

This section went through the **three stages** of the assurance ladder (like M4 of the method document).

**Round 1 — Executor: Haiku · Reviewer: quality-guardian (Sonnet) → REJECTED** (3 blockers):

| # | Finding | Severity | Why it mattered |
|---|---------|----------|-----------------|
| 4.1 | The template did not use the required sections (missing *Objective* and *Context/stack*) | 🔴 Blocking | A verbatim requirement of the work order |
| 4.2 | The template included "Projects / key resources with absolute paths" → tied to a concrete multi-project workspace | 🔴 Blocking | The template must serve any project (an explicit mistake to avoid) |
| 4.3 | Placeholders with escaped HTML entities instead of raw signs | 🔴 Blocking | With escaped entities, the reader copies a broken template |

**Round 2 (re-audit) — Executor: Haiku · Reviewer: quality-guardian → REJECTED.** Haiku resolved 4.1–4.3 but **introduced a new regression**: it reintroduced a tool's concrete file name (`CLAUDE.md`) three times in the prose of the generic body — exactly what the previous version had correctly kept generic. **A re-audit with 🔴 → TRIGGERS the escalation.**

**Round 3 (escalated) — Executor: Sonnet · Reviewer: Opus (director) → PASS.** Per the rule of assurance proportional to severity, when the blocker recurred in the re-audit the iteration went up a level: executor from Haiku to **Sonnet**, reviewer from quality-guardian to **Opus** (preserving reviewer > executor). Sonnet was handed **the whole set of constraints at once**. Sonnet held them all simultaneously: it reformulated the reference to the file in generic terms + a reference to the Appendix, kept the template's exact sections and the raw signs. Opus's audit: PASS, no blockers.

**Lesson / calibration — the M4 pattern repeated:** the economical executor entered a **"fix-on-one-side, break-on-another" cycle** (resolving 4.1–4.3 cost it the concrete-name regression). It is not that it "tried too little": it is that **holding several constraints simultaneously exceeds its reliable window**. The higher level not only complied, but used the margin to *improve* the text (approval authority, inheritance between branches) without violating any rule — consistent with M2: the extra capability is better spent on the hard part. Further evidence that the defense is not "asking more of the same executor", but the **structure** (evidence-based escalation + an independent reviewer of higher capability).

### Section 3 — Map of the 5 pieces · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**Reviewer's first return: REJECTED** — two blockers:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 3.1 | A body of 151 words, well below the 250-350 range (a ~40% shortfall) | 🔴 Blocking | The drafter expanded to ~287 words developing "layers" and the role≠model clarification | A verifiable numeric requirement of the work order |
| 3.2 | A reference to a non-existent section ("Infrastructure requirements") | 🔴 Blocking | Corrected to the real name, "Prerequisites" | A link to a section that does not exist breaks the reader's navigation |
| 3.3 | "configuration manager" in the hooks row (a term foreign to the rest) | ⚪ Minor | Unified to "environment" | Terminological consistency of the table |

**Re-audit: PASS with adjustments** (287 words; the 3 blockers resolved). Escalation NOT triggered (first return). But the reviewer caught a **new finding in the added content**:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 3.4 | On expanding, the drafter introduced a paragraph of **strict dependency chain** ("if there are no subagents, the hooks have nowhere to verify") that **contradicted** the "complementary, not exclusive, layers" framing of the previous paragraph — and is factually false (a hook can verify objective rules with no subagents) | 🟡 Improvement | The director reformulated the paragraph: the order is *reinforcement, not a rigid dependency*; it made explicit that **each piece adds value on its own** and that you can install "one, some or all" | An over-statement introduced *while correcting* another finding; it reinforces that expanding text can create new defects |

**Lesson / calibration:** an instructive failure mode — **correcting one blocker (short length) created a new defect** (over-statement from padding). It is the flip side of "over-illustrating": when *more* text is asked for, the drafter can fabricate conceptual structure that sounds solid but contradicts the document's own thesis. Antidote: the re-audit does not only verify the old blocker was resolved, it **audits the new content as if it were a fresh piece**. It also reaffirms "verify, don't trust": the director had anticipated this risk and flagged it to the reviewer before the re-audit.

### Section 5 — Persistent memory · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**Reviewer's first return: REJECTED** — two blockers:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 5.1 | Template 1 (index) used headers (User/Project/Decisions/Lessons) that did NOT match the four types defined in the text (User/Feedback/Project/Reference) | 🔴 Blocking | The Template 1 headers were aligned to the four types | An internal contradiction between the text and its own template confuses the reader who copies it |
| 5.2 | It could not be confirmed the templates were copy-paste code blocks with raw signs | 🔴 Blocking | Verified in the re-audit: two ```markdown blocks with raw `<...>` placeholders | The Definition of done is that the reader copies a functional template, not a broken one |

**Re-audit: PASS with adjustments** (~340 words). Escalation NOT triggered (first return). One 🟡 remained: the `type` field in English (`user | feedback | project | reference`) against labels in Spanish (Usuario/Feedback/Proyecto/Referencia).

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 5.3 | Language inconsistency: label "Referencia" (ES) vs value `reference` (EN) in the `type` field | 🟡 Improvement | The director fixed the convention with a note: readable headers go in the user's language, but the `type` value stays in English because it is a machine-readable technical label | Without the explicit convention, the reader would not know whether to write `type: referencia` or `type: reference` |

**Lesson / calibration:** a **text↔template consistency** failure mode — the drafter defined four types in the prose but built the template with another taxonomy (Decisions/Lessons). It is a relative of "omission of a work-order element": the delivered artifact does not reflect what the text itself promises. Antidote: the template is audited **against the definition that precedes it in the same section**, not in isolation.

### Section 6 — Self-activating skills · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**Reviewer's verdict: PASS** (389 words, in range), **no blockers or improvements** — the cleanest section so far, together with Section 1. The drafter held all the constraints on the first try: genericity (zero tool or real-skill names), the hard fact "the skill is **loaded**, not trained" well stated, the two recommended skills present, and the template with the `description` field modeled as the central trigger.

**Process note:** there was a retry due to a network drop of the executor (not a content one); the second attempt came out clean. The only point verified by the director on consolidation: that the template's `<...>` placeholders stayed with **raw** signs (confirmed).

**Lesson / calibration:** a contrast with the previous "piece-by-piece" sections (F4, F5) that stumbled on genericity and templates. Here the **accumulated safeguards** — the explicit "concrete name → Appendix" and "raw signs" instruction from the work order on — avoided the already-catalogued failure modes. It is the log's intended effect: each recorded failure becomes a barrier that prevents its recurrence. Detection stops being the first net when prevention does its job (an echo of the method's M6 finding).

### Section 7 — Preloaded subagents · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**Reviewer's first return: REJECTED** — one blocker:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 7.1 | **Omission of a mandatory element:** the reference to the method document for the theory of roles was missing | 🔴 Blocking | The director added a reference line at the close of "What I configure" (proportional verification, no full re-audit, being the insertion of a single line the reviewer itself specified) | The work order asked for it explicitly; without it, the reader does not know where the why of the two roles is developed |

Everything else met the mark on the first try: 325 words in range, genericity (zero concrete names), raw signs, and **the two explicit hard rules** (executor "returns content, does not persist"; reviewer independent and one level above). A 🟡 from the reviewer ("the dangling Appendix reference") was dismissed as an **isolation false positive**: the reviewer audited the section alone, but in the full document the Appendix (Section 12) exists and the reference is consistent with F4–F6.

**Lesson / calibration:** the **omission of a mandatory work-order element** failure mode reappears (already seen in M9 of the method and in Section 2). It is the quietest one: the drafter develops well what it includes, but leaves out a requirement. It confirms that the antidote is to run through the "Must contain" as a closed checklist. It also illustrates "verify, don't trust" toward the reviewer: not every 🟡 survives the full context (the Appendix one was an artifact of auditing in isolation).

### Section 8 — Enforcement hooks · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**Reviewer's first return: REJECTED** — one blocker + two improvements:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 8.1 | Length 451 words, ~13% over the 400 cap | 🔴 Blocking | The director pruned "What it does" and "Design warning" to ~387 words without losing mandatory content | The work order's closed, verifiable range; length consistency across sections |
| 8.2 | The reference to the method for "when to industrialize" a rule was missing (it only referenced for Detection/Recovery) | 🟡 Improvement | Added the reference in "What it does" | The work order asked for both anchors to the parent document |
| 8.3 | The example names (`.env`, etc.) came with `<...>`, clashing with the template's placeholder syntax | 🟡 Improvement | Replaced with backticks (`.env`, `secrets.json`, `password.txt`) | In a section with a copy-paste template, `<...>` must mean "replace this"; confusing an example with a placeholder breaks usability |

**Lesson / calibration:** two already-catalogued failure modes, together — **length overrun** (like M5 of the method) and **notation collision** (the example `<...>` against the placeholder `<...>`), a fine relative of text↔template consistency. The rest (genericity, pre/post-event, false positives, "subjective = skill", template) came out on the first try. With this section **the piece-by-piece installation block (F4–F8) closes**; the closing sections remain (verification, human limits, maintenance and appendix).

### Section 9 — Verify the installation · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**Reviewer's first return: REJECTED** — one blocker + one improvement:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 9.1 | **Embellishment:** the anchor invented unverified failure details ("load-order inconsistencies", "overlapping signals") about the real project's live test | 🔴 Blocking | The invented examples were removed; the honest, generic statement was kept ("errors that static review did not anticipate") | A plausible but unconfirmed fact = an incorrect fact (the accuracy rule); the document preaches honesty, it cannot fabricate in its own anchor |
| 9.2 | The anchor did not explicitly reference the method document | 🟡 Improvement | Added the reference ("the stage the method itself reserves as the final net") | The work order asked for it; it closes the loop with the parent document |

**Process note — double detection:** the director **anticipated** the embellishment in its pre-read and flagged it explicitly to the reviewer; the reviewer **confirmed** it independently. It is the ideal "verify, don't trust" configuration: the director's suspicion does not replace the independent audit, it reinforces it.

**Lesson / calibration:** **fabrication/embellishment** reappears — the drafter's most dangerous failure mode — and, again, in an anchor to "real facts". It confirms the M3/M7 pattern of the method: the drafter fills specificity gaps with invented detail that "sounds verifiable". A known antidote: give the reviewer the **ground truth** (here, that the only real facts are generic) so the fabrication does not pass.

### Section 10 — What stays human · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**Reviewer's verdict: PASS** (272 words, in range). No blockers. A single adjustment:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 10.1 | Typo "accelera" in the key sentence ("The AI accelera the work") | 🟡 Improvement | Corrected to "acelera"; the director also unified the final reference to "the method document" | A spelling error right in the sentence that carries the thesis detracts from the polish of a method document |

**Lesson / calibration:** one of the cleanest sections. The key sentence ("the assembly is automated, not the judgment") and the five categories of human checkpoint came out on the first try. It confirms that the **conceptual** sections (no template, no verifiable data) have the drafter's lowest incident rate: the serious failure modes (fabrication, name leak, notation collision) concentrate where there is **concrete data or technical artifacts** (anchors, templates, names). A corollary for the method: size the vigilance by content type — more rigor where there are facts and code, less where it is conceptual prose.

### Section 11 — Maintenance · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet)

**Reviewer's verdict: PASS** (262 words, in range), **no blockers or mandatory improvements** — only a ⚪ cosmetic one on the typographic density of the bullets, not applied. The drafter met the four requirements on the first try: the 2-3 cycle criterion, the recurring checkpoint, the symptom → tool mapping (subagent/skill/hook) and the reference to the method without reproducing the table. **And — the notable point — it kept the anchor GENERIC without fabricating details**, exactly the failure mode the previous section (S9) had triggered.

**Lesson / calibration:** it confirms the corollary just noted in S10: it is a conceptual section and it came out clean. Moreover, the drafter **did not repeat the S9 embellishment** in an equivalent anchor (recurring failure → hook), because the work order this time explicitly included "keep the anchor generic, do not invent details". Prevention (an anti-fabrication instruction in the work order itself) did again the work that in S9 had to be done by detection.

### Section 12 — Appendix: realization in Claude Code · 2026-06-24 · Executor: Haiku · Reviewer: quality-guardian (Sonnet) · Technical verification: Opus

**Reviewer's first return: REJECTED** — one blocker + several improvements:

| # | Finding | Severity | Correction applied | Why it mattered |
|---|---------|----------|--------------------|-----------------|
| 12.1 | **Syntax fabrication:** the `settings.json` block used an invented form (a flat array with `name`/`event`) that does not exist in Claude Code | 🔴 Blocking | The director rewrote the block with the real syntax (a `hooks` object indexed by event, with `matcher` + an inner `hooks` array of `{type, command}`) | An appendix on wiring whose flagship example does not work is worse than not having it: the reader copies something broken |
| 12.2 | The script read the payload as `event.parameters?.…` (a non-existent field) | 🟡 Improvement | Corrected to `event.tool_input?.…` | The reader who copies the script would detect nothing, reading an empty field |
| 12.3 | "Hooks run at the start of every session" — ambiguous (suggests they run once on opening) | 🟡 Improvement | Reformulated: they become *active* at startup and *fire* on every matching event | Prevents the reader from believing the hook runs a single time |
| 12.4 | Prose body below the range (350-500) | 🟡 Improvement | Expanded with context from the table and the activation note, without re-explaining the "what for" of each piece | The work order's length requirement |

**Process note — the director's technical verification:** the syntax fabrication was **anticipated by the director** (who knows Claude Code's real syntax) and **independently confirmed by the reviewer**, who was handed the correct syntax as ground truth. Double detection, as in S9.

**Lesson / calibration — closing the failure repertoire:** the appendix concentrates the greatest risk of **technical fabrication** of the whole document, because it is the only section that touches concrete detail of a tool. It confirms, for the last time, this log's structural finding: the drafter's serious failure modes (fabrication, name leak, notation collision, embellishment) **concentrate where there are verifiable facts, code or syntax**, not in conceptual prose. The antidote that worked across the 12 sections was always the same: **ground truth for the drafter + independent detection + the director's verification of what is verifiable**, each layer covering what the previous one might let through.

---

## Closing — Document status

The **12 sections are consolidated** and the guide is complete: the promise (Section 1), the requirements (2), the map of the 5 pieces (3), the piece-by-piece installation (4–8), the verification (9), the human limits (10), the maintenance (11) and the concrete Claude Code appendix (12). This log records **12 incident sessions** that cover the drafter's full repertoire of failure modes — **over-illustrating, leak of a concrete name, omission of a mandatory element, text↔template consistency, length overrun, notation collision, embellishment and syntax fabrication** — two real activations of the escalation rule (Section 4 and, in the method's production, M4) and several cases of the reviewer's and the director's own fallibility corrected by the structure. In all of them, what contained the error was not trusting a role, but the scaffolding: ground truth, independent review and proportional verification. That is, in one sentence, the method this guide teaches you to install.

Produced with the blueprint in [`installation-guide-work-orders.md`](installation-guide-work-orders.md).
