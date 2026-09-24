# Template: persistent memory

> **What it does.** It provides continuity between sessions. The model starts each conversation
> with no memory of the previous one; memory closes that gap with the project's living context.
>
> **How to verify it is used.** Open a new session and ask about a decision made in another
> conversation. If it recovers it without your telling it, the piece is alive.
>
> **What NOT to save:** what already lives in the code or the repository, the version history
> (that is version control's job), and the ephemera of a one-off exchange.
>
> Conceptual basis: [`docs/04-persistent-memory.md`](../docs/04-persistent-memory.md).

Memory is organized as an **index** plus a collection of **atomic files** linked to one another.
One topic per file.

---

## Index template

```markdown
# MEMORY INDEX — [Project]

- [file-name.md](file-name.md) — [one line of what it contains, written to decide whether it is
  worth opening or not]
- [another-file.md](another-file.md) — [...]
```

The index is a map, not a summary. Each line exists so that whoever reads it can decide whether
they need to open that file. If the line does not allow deciding, it is badly written.

---

## Memory file template

```markdown
---
name: <slug-in-kebab-case>
description: <one line; it is what gets read to decide whether this file is relevant>
metadata:
  type: user | feedback | project | reference
---

<The fact. For feedback and project, follow with the why and with how to apply it.>

Related: [[another-file]], [[and-another]]
```

## The four types

| Type | Content | What for |
|---|---|---|
| **user** | Role, preferences, history, who the person is | Personalize the tone, understand intentions, respect limits |
| **feedback** | Corrections and agreements on how the AI should work, with their why | Refine behavior without repeating the same mistake |
| **project** | Current goals, constraints not derivable from the code, key decisions | Keep alignment and avoid regressions |
| **reference** | URLs, boards, tickets, external documents | Quick access without searching |

## Rules that avoid the two most common failures

**Update the index when you update the file.** A corrected file with its index line uncorrected
is worse than not having touched it: the next session reads the old summary and starts from the
wrong premise.

**Turn relative dates into absolute ones.** "Next week" means nothing three months from now.
Write the date.
