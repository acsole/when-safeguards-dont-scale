## 6. Industrialization

### Principle: automate what repeats

In the working cycle described in Module 3, every interaction with the AI is an event where decisions are made, conventions are applied, results are reviewed. When one of those interactions starts to repeat — the same preamble on every delegation, the same technical rule to check, the same conventions to apply — a candidate for industrialization is born.

Industrialization is moving from "repeating it by hand each time" to "automating the repetition". It is not a first-cycle decision; it is an observation that emerges after two, three, four similar interactions. The automation checkpoint (Module 3) is the moment to put the question: is it worth investing in automating this?

The answer depends on three tools this AI working environment offers, each designed for a different pattern.

### The three tools of industrialization

**HOOK**: a deterministic script that runs automatically on an event (for example, after every edit). Its strength is *enforcement*: it can block an action if it violates an objective, verifiable rule. A real example: in the ASLAN project (a multi-project dashboard), there was a manual process where the director ran a grep to make sure no file violated certain technical invariants of the code. That grep was automated as a hook that runs the same logic every time someone edits. If the rule is violated, the hook stops the action automatically, with no human intervention at that moment. Hooks are for rules that must NEVER be broken.

**SKILL**: a package of knowledge, conventions or procedures the AI knows and applies on demand. It is invocable: when the AI detects that it applies, it activates it. A real example: in ASLAN, the project's design and technical conventions were encapsulated in a skill. Now, every time someone works on the dashboard, that skill is applied without repeating the same long preamble. Skills are for bodies of knowledge that get applied again and again, with some flexibility depending on context.

**SUBAGENT**: a delegated agent with a specific role and preloaded context. It is useful when a recurring task needs a specialized agent that already "knows" what it does. A real example: in ASLAN, delegating to an executor meant repeating a long preamble about the project's invariants. An executor subagent was created that is born with that context. Now, on every delegation, the context comes included. Subagents are for repeated roles that carry a lot of context.

### Decision table

| Symptom | Tool | Reason |
|---------|------|--------|
| "I repeat the same preamble/context on every delegation" | Subagent | Preloads the context once; removes the repetition from the communication |
| "There is a body of conventions I always apply" | Skill | Encapsulates reusable knowledge; the AI invokes it when it applies |
| "An objective technical rule that must NEVER be violated" | Hook | Automates a deterministic check; blocks the violation |

### How to choose and combine

The central question is: what kind of repetition do I have?

- If it is **context/preamble that repeats**, use a **subagent**.
- If it is **knowledge/convention that gets applied**, use a **skill**.
- If it is **a technical rule that must be enforced**, use a **hook**.

And it is rarely "just one". In ASLAN, the executor (a subagent) applies the conventions (a skill) and its changes are verified by a hook: the three work together, each in its role. They are not mutually exclusive options but complementary layers in a mature flow.

Operational maturity arrives when the patterns are recognized early, without waiting for them to grow chaotically. Two or three cycles are usually enough to know whether industrializing is worth it. Automating sooner is premature; waiting longer is accumulated inefficiency.
