## 5. Atomicity rules

An atomic task is indivisible: a single piece of work with clear boundaries, no hidden dependencies on other tasks, that can be completed on its own. In the context of our method, atomicity is the antidote to confusion, duplicated effort and misunderstanding.

When an executor receives a task that actually contains two (draft one module AND review another; design a screen AND write the documentation), ambiguity appears: what do I do first? How far does my responsibility go? What does the reviewer do if part of my delivery invades someone else's territory? These questions should not exist.

The tool that guarantees atomicity is the **work order**: a short, structured, explicit document that defines the **scope** of the task — what goes in and, more importantly, what stays out. It is the boundary made tangible.

### How do you keep two tasks from stepping on each other?

Through the work order's **"MUST NOT touch"** field. This field carries the most leverage: it explicitly lists the areas, decisions, files or domains this task does NOT touch, even if they look related. If the boundary is written in black and white, there is no room for interpretation.

Example: if Task A is "review a compliance document", the "MUST NOT touch" reads: *"Do not change the underlying legal structure, do not extend the scope to new jurisdictions, do not modify contract terms already approved."* That way, even if someone reads the document and thinks "this could be improved here", they know it is out of scope.

### The work order template

| Field | Function |
|-------|----------|
| **Purpose** | A one-line summary of the task's objective. Example: *"Review the contract's compliance section."* |
| **Must contain** | A closed checklist of points the executor must include in the delivery. Not prose; verifiable requirements. Example: clause validation, date checks, comparison against current regulations. |
| **MUST NOT touch** | Explicit boundaries. What does NOT belong in this task, even if it sounds related. Example: do not change contract terms; do not expand to new jurisdictions; do not review unspecified annexes. |
| **Inputs** | What the executor is handed to start: prior documents, context, guides, examples. |
| **Output form** | Format, length, tone. Example: *"Markdown, point by point, a log of findings."* |
| **Definition of done** | The yardstick the reviewer measures it against. Example: *"When finished, decisions can be made on each finding without consulting again."* |

### A contrasting example

**Fuzzy task (bad):** *"Improve the project's methodology section."*
Problems: which part? to what level of detail? Do I change the existing modules? Do I add new ones? The executor will guess.

**Atomic task (good):** *"Draft Module 5 on atomicity: definition, work order template as a table, emphasis on 'MUST NOT touch', a good-vs-bad split example. Do not modify Modules 1-4. Markdown, 450-600 words. Criterion: the reader can draft their own work order."*
Benefit: the executor knows exactly what to do, where its work ends, and the reviewer knows how to validate it.

### Living proof

This method was built with work orders: one per module. Each drafter received a bounded work order that guaranteed the nine modules fit together with no overlaps and no gaps.

A warning to close on: a badly written work order *drafts* the content instead of *bounding* it — and that shifts the work from the drafter to the reviewer. When you design your next task, write its work order first. If you notice the "MUST NOT touch" is getting too long, that is a sign the task is too broad: split it.
