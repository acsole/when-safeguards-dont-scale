# Copy-paste templates

The five pieces that install the scaffolding, plus the work order that sets it in motion.
Each template is a skeleton to copy, fill in and use.

## The map of the pieces

| Piece | What repetition it removes | When it fires | Where it lives |
|---|---|---|---|
| [Base context](CLAUDE.md) | Re-explaining the project in every session | At the start of every session | At the project **root** |
| [Persistent memory](memory.md) | Rebuilding what was already decided | When consulting the index | A memory folder, an index + atomic files |
| [Skill](SKILL.md) | Repeating a body of conventions | By context match | A skills folder |
| [Subagent](subagent.md) | Re-pasting the preamble when delegating | When delegating a task | A subagents folder |
| [Hook](hook.md) | Checking a hard rule by hand | On an event (pre or post) | A script + a registration in the configuration |

They are not alternatives: they are **complementary layers**. An executor subagent can apply
a conventions skill and have its changes verified by a hook. The three at once, each in its role.

And cutting across all of them, the tool that bounds the work:
**[the work order](work-order.md)**.

## Which to choose

| Symptom | Piece |
|---|---|
| "I repeat the same context every time I delegate" | Subagent |
| "There are conventions I always apply" | Skill |
| "This objective rule must NEVER be broken" | Hook |
| "What we decided last session gets lost" | Memory |
| "I have to explain the project again" | Base context |

**When to install a new piece:** after two or three cycles in which the same repetition
appears. Before that is premature; after that is accumulated inefficiency.

---

## Verification checklist

The scaffolding is not installed until you see it activate on its own. Open a **new session** and
verify piece by piece. The principle is the same one that governs the method: **verify, don't
trust.**

- [ ] **Base context.** Ask about a constraint written only there. Does it answer without
      your pasting it in?
- [ ] **Memory.** Ask about a decision made in another conversation. Does it recover it?
- [ ] **Skill.** Work in its context without naming it. Does it apply its conventions on its own?
- [ ] **Subagent.** Delegate something without explaining the conventions. Does it respect them anyway?
- [ ] **Hook.** Attempt the violation on purpose. Does it really stop it?

A box you cannot tick is a piece that **is not installed**, no matter that the file exists. And
testing under real conditions reveals failures the design does not anticipate: in a project of
my own, the live test uncovered two errors that static review had approved.

## Prerequisites

Before installing anything, verify all three are met. If any is missing, the method does not
apply in your current context and will only slow you down.

- [ ] Access to **three models of differentiated capability**: one to direct, one to review, an
      economical one to execute.
- [ ] An environment that supports **automatic base context, skills, subagents and hooks**.
- [ ] An active **version-control system**, which is the Recovery layer.
