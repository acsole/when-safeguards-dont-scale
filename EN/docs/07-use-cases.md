## 7. Use cases

### Case 1: The production of this document (dogfooding, step by step)

The document you are reading — the "AI Working-Method" — was produced **using the method itself**. This is the clearest living example of how it works in practice.

**Starting situation:** A human-AI team needed to document how it collaborates to produce quality work. The bet was ambitious: that the method would test itself while being written.

**Applying the method:**

First, the director (a higher-reasoning model) and the human defined a skeleton of 9 modules together. For each one, they wrote a "work order" — a document with precise scope, boundaries and success conditions.

Next, for each module, the drafter-executor (a fast, economical model) received its work order, produced a draft and returned it as prose, without writing files. The text went straight to review.

The independent reviewer (a mid-capability model, in a guardian role) audited each draft against its work order. Its job: does it answer every question? does it stay within the boundaries? is there any invented data?

When findings came up, the module went back to the drafter with concrete feedback. The round repeated until the reviewer gave its approval.

Finally, the director consolidated the approved module, saved it in version control (one commit per module) and fed an incident log that recorded every incident: which reviews were needed, where the first version failed, when it was escalated to higher capability.

**Concrete results:**

The reviewer caught **real fabrications**: one module claimed that "some modules reached three rounds" when the real maximum was two; another invented a memory-selection rule based on task type that did not exist in the protocol.

The reviewer also caught **omissions**: modules that dropped mandatory elements of the work order, and **redundancies**: sentences that repeated concepts explained paragraphs above.

In one module, an **escalation rule fired**: the drafter reoffended on a specific failure. By protocol, the task moved up to a more capable drafter and the reviewer moved up to the director (one level above). The result: a correct module on the second round.

In another case, the reviewer even **corrected the director**: a length estimate the director had made turned out to be wrong; the reviewer flagged it.

**Transferable lesson:** The method does not prevent failures — it produces them and catches them. Independent review acts as the containment net. What matters is recording openly where each attempt failed (the incident log), because that record is evidence of rigor, not of incompetence.

### Case 2: ASLAN (validation in production)

ASLAN is a dashboard that monitors projects in parallel. It was built using this same method: work orders, drafter, reviewer, director, escalation when necessary.

**Situation:** The dashboard was "ready" according to static review. But the method includes a critical step: **testing under real conditions**.

**What happened:** In production, the test revealed two errors the design had not anticipated. First: agent identities that collided. Second: elements that did not expire when they should.

Both were fixed. Without the live test, those errors would have reached users.

**Transferable lesson:** Testing under real conditions reveals failures that theoretical design does not anticipate. The full method is: build → review → test → find → fix. Each cycle puts the work under tension and improves it.
