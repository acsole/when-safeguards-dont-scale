# Template: self-activating skill

> **What it does.** It encapsulates a body of knowledge or conventions that gets applied again
> and again, so you do not repeat the same preamble in every conversation.
>
> **When to choose it.** When the symptom is *"there is a body of conventions I always apply"*.
> If the symptom is an objective rule that must never be broken, that is a [hook](hook.js). If it
> is context that repeats when delegating, that is a [subagent](subagent.md). See
> [`docs/06-industrialization.md`](../docs/06-industrialization.md).
>
> **The skill is LOADED, not trained.** It is a file that is read when the context matches its
> triggers.
>
> **How to verify it self-activated.** Work in the context that should trigger it, without naming
> it. If it applies its conventions on its own, the piece is alive.

---

## The decisive field is `description`

The skill activates by context match against its `description`. A poor description never fires,
however good the skill is.

A well-written `description` answers three things: **what** it contains, **when** to use it, and
with **what phrases or situations** it fires. Write the triggers as a real user would say them,
not as you would name them internally.

---

## Template

```markdown
---
name: <slug-in-kebab-case>
description: <What this skill is and what it solves.> Use this skill WHENEVER <concrete
  situation 1>, <situation 2> or <situation 3>. Activate it too when the words
  "<trigger>", "<trigger>", "<trigger>" appear, or when <another skill> needs <X>.
---

# <Title>

**Scope:** <which projects or tasks it applies to, and which explicitly not>

## 1. <The guiding principle>

<What is non-negotiable. If there is a single thing someone should take away, it goes here.>

## 2. <The rules>

- <A concrete, verifiable rule>
- <A concrete, verifiable rule>

## 3. What works and what doesn't

**WORKS:**
- <A validated practice, with its why>

**DOESN'T WORK:**
- <An observed anti-pattern, with its real consequence>

## VERSION HISTORY

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | YYYY-MM-DD | Initial version. |
```

---

## Two tips that come from real failures

**Put in the version history.** A skill with no version cannot be corrected with confidence: no
one knows whether what they are reading is what was agreed or a leftover from a previous iteration.

**Separate the learning log from the skill itself.** A `LEARNING-LOG.md` alongside accumulates
the cases that justified each change. The skill says what to do; the log says why.
