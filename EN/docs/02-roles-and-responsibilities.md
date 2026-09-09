## 2. Roles and responsibilities

The method rests on a clear separation of authority, capability and responsibility. Each participant — the human and the models — occupies a role with defined limits. Final authority always rests with the human; the models are specialized facilitators, each chosen for the strength the task demands.

The key idea is **assurance proportional to severity**: the rigor of who executes and who reviews scales with the consequences of the worst plausible outcome. An economical drafter generates low-risk content (a feature description, a paragraph of documentation) because volume is high, the cost of iterating is low, and the potential harm is bounded. That is why it is not assigned to review: its resources are better spent on fast production. The higher-capability model is reserved for directing and reviewing what is critical, precisely because its cost per token is higher but its risk coverage is exponentially greater. This proportionality avoids both over-engineering the trivial and neglecting the grave.

### The roles

| Role | Responsibility | What it does NOT do |
|------|----------------|---------------------|
| **Human authority** | Decides in the last instance. Approves or rejects plans before execution. Sets strategic direction. Acts as guardian of the project's ethics and constraints. | Execute without reviewing. Delegate high-risk decisions. Assume a proposal is correct without questioning it. |
| **Director** (higher-reasoning model) | Analyzes the problem in depth. Proposes structured plans. Questions assumptions. Pushes back when it sees risk. Assigns who executes and how. Designs the architecture of the work. | Execute code or generate final content. Make decisions without consulting the human. Assume consensus where there is none. |
| **Executor / Reviewer** (mid-capability model) | Implements the concrete tasks the Director assigns. Reviews the quality of what is produced, as a guardian. Reports findings and blockers. Iterates until it meets the specification. | Change the plan without consulting. Execute extreme-severity tasks without express supervision. Pass deficient content off as ready. |
| **Drafter** (fast, economical model) | Generates concrete, atomic pieces (text, fragments, initial proposals). Works from the Director's clear instructions. Produces quickly, to iterate. | Make design decisions. Review others' work. Work without a sense of the severity at stake. |

### Severity scales and assignment

- **Low consequence** (internal documentation, examples, drafts): the Drafter produces, the Executor / Reviewer reviews briefly.
- **Medium consequence** (architecture, logic code, interface): the Director proposes, the Executor / Reviewer implements and reviews, the human approves.
- **High consequence** (security, health, ethics, legal constraints): the Director and the human design it together, a more capable Executor implements, and a human reviewer — or a top-capability model — validates before publication.

In real projects, these roles have taken shape as reusable agents: a *specialized executor* preconfigured with the project's conventions (cutting down explanation cycles) and an *independent quality reviewer* that sees the work with fresh eyes. The reviewer always sits one capability level above the executor, guaranteeing coverage with no blind spots.
