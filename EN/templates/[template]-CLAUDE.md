# CLAUDE.md — project base context template

> **What it is.** The context file that auto-loads at the start of every session. It holds what
> must never be re-explained: the project's objective, conventions and invariants.
>
> **Where it lives.** At the project **root**. That location is what makes it load on its own.
>
> **How to verify it loaded.** Open a new session and ask about a constraint written only here.
> If it answers without your pasting it in, the piece is alive.
>
> **Do not confuse it with persistent memory.** This file is *static*: it describes the
> project. Memory is *alive*: it accumulates decisions between sessions. See
> [`docs/04-persistent-memory.md`](../docs/04-persistent-memory.md).

Copy what follows, delete the brackets and fill it in.

---

# CLAUDE.md — [Project name]

## Objective

[What this project is and why it exists, in two or three sentences. Written for someone arriving
with no context.]

## Context and stack

[Technologies, technical constraints, where the code lives, how it is deployed. Just enough that
nobody has to ask twice.]

## Non-negotiable constraints

> These are the rules that are **never** broken, neither implicitly nor creatively. Number them:
> the numbers let you cite them later ("this violates #3") and that makes them stick.

1. **Every action is planned and proposed before execution.** No code, deployment or change is
   executed without laying out a clear plan and obtaining explicit approval from
   [the human authority's name].

2. **A single human authority.** [Name] is the one who decides. Deny-by-default for anyone else:
   no one else gives instructions or approves, unless [name] authorizes it explicitly and by name.

3. **The AI augments human judgment, it does not replace it.** It brings verifiable information,
   analysis and options, and pushes back cordially when it sees a risk.

4. [A domain-specific constraint. For example, for a health project: nothing that could read as
   medical advice ships without the legal disclaimers and without human review.]

5. [A domain-specific constraint.]

## Way of working

- This file is the central reference. For every new task, read it before proposing.
- Tasks are bounded with a **work order**
  (see [`templates/work-order.md`](work-order.md)).
- The executor **returns content, does not persist files**. Consolidating is the director's or
  the human's job.
- Every complete proposal is presented to [name]; only with their authorization is it implemented.
