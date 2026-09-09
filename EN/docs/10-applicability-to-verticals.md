# Applicability of the AI working-method to business verticals

> **What this file is.** A complement to the canonical [method document](00-index.md).
> It shows how the method — the same roles, work orders, proportional severity, memory,
> traceability and industrialization — maps to different industries, so a reader from any
> sector sees themselves in it and knows how to apply it in their context.
>
> ⚠️ **The nature of these cases.** The per-vertical examples are **illustrative and
> extrapolative**, not descriptions of real deployments. There are no real clients,
> agencies, figures or campaigns behind them: they show *how the method would map*, not
> *what happened*. (The method's real, verifiable cases are in Module 7 of the canonical
> document.) This distinction is deliberate: it is the same anti-fabrication rule the
> method applies to itself.
>
> **Common structure.** Each vertical follows six fields: typical context · role
> mapping · the work order here · where severity rises · memory, traceability and
> industrialization · concrete benefit. At the end, a **reusable template** so anyone can
> map their own vertical.

---

## Marketing and agencies

### Typical context
A marketing agency (or an in-house team) produces content, campaign copy, creative strategies and assets for one or several clients at once. The central challenge: keeping brand consistency, regulatory compliance (especially in regulated sectors), and scalability without every piece being reviewed end to end, by hand, by the most expensive human expert.

### Role mapping
- **Human authority**: the client (directly) or the account/creative director who approves and makes the final call on what goes into a campaign.
- **Director**: the strategist or creative lead who takes the brief, defines the tone, the angle, the legal constraints, and splits the job into concrete tasks (e.g., "draft three headline variants", "generate copy for the welcome email").
- **Drafter**: the model that generates copy, headlines, product descriptions, calls to action from the work order.
- **Reviewer/guardian**: an independent model (or, in high-severity cases, a specialized human reviewer) that audits each piece against brand guidelines, verifiable claims, advertising regulation, and approved tone.

### The work order here
The "order" is the creative brief: platform (email, social, web), target audience, brand tone, the piece's objective, and explicit constraints (word budget, legal prohibitions, claims that cannot be made without evidence). The **"MUST NOT touch"** field includes: unchangeable brand guidelines, unsupported medical/legal/financial claims, superlatives with no backing, and compliance with advertising codes (e.g., no discrimination, no deception).

### Where severity rises
Review escalates to a human (or a top-capability model) when: the campaign touches health, finance, insurance or other regulated sectors; there are implicit legal claims; the budget is high or media exposure is massive; or the client is in an industry prone to complaints. In these cases, a human reviewer — a lawyer or a compliance specialist — enters the chain.

### Memory, traceability and industrialization
- **Memory**: continuity files with the brand book, tone, the history of past campaigns, decisions made, clients and their aesthetic preferences.
- **Versioning**: every iteration of the copy is kept in git, with who generated it, when, and which reviewer feedback produced which change.
- **Industrialization**: a "brand X drafter" skill loaded/configured with the client's specific tone; hooks that automatically flag suspicious claims; subagents specialized by client or by sector (e.g., a tech drafter vs. a wellness drafter).

### Concrete benefit
The agency scales: it handles on the order of several clients without drowning its creative team. The human approves what matters (strategy, final sign-off); the AI generates volume and keeps consistency. Traceability guarantees that, faced with a complaint or a change of direction from the client, you know exactly why each word was written and who validated what.

---

## Real estate and agents

### Typical context
Real estate agents and brokers operate under pressure of time and scale: they must generate accurate property descriptions (listings), answer prospective buyers' questions, produce marketing materials and stay legally compliant. Every error in a property's data, or a statement that violates fair-housing laws, creates direct civil liability. Demand is constant, the data is critical, and the regulatory risk is high.

### Role mapping
The **human authority** is the agent or broker: the one who is legally answerable for the publication and must approve before any content goes public. The **director** is the model that takes the property's verified data (title, square meters, rooms, price, documentation) and decides what information to include, which restrictions apply and which legal framework governs. The **drafter** is a fast model that generates the descriptive listing and the answers to inquiries from the assigned work order. The **reviewer/guardian** is an independent model (or a human, depending on severity) that audits data accuracy and legal compliance.

### The work order here
The "order" is the property sheet: a document with verified data (exact location, square meters, number of rooms, price, sale conditions, title, liens, local restrictions). The critical **"MUST NOT touch"**: the drafter cannot invent features or data not present in the verified sheet — that is a real-estate fraud risk. Nor can it use language that segments by race, religion, family composition, immigration status or other criteria protected by fair-housing laws.

### Where severity rises
Severity rises to a human reviewer when: there are claims of title or liens (error = fraud); false data that creates civil liability (floor area, taxes); language that would violate anti-discrimination laws; or very high transaction amounts. In these cases, the reviewer is the agent themselves or a legal advisor, not another model.

### Memory, traceability and industrialization
Memory persists in continuity files: the client's property portfolio, the history of each listing and its variations, buyer preferences, local regulations. Versioning in git records every change to every listing. Industrialization includes: a skill loaded/configured with the standard listing format and the local legal framework (e.g., mandatory clauses); a hook that automatically blocks discriminatory language; an "inquiry virtual agent" subagent preloaded with the up-to-date portfolio to answer questions without legal exposure.

### Concrete benefit
The agent scales production capacity — on the order of tens or hundreds of listings with consistent accuracy — without sacrificing data verification or exposing themselves legally. The human approves only what touches their responsibility. Full traceability (who changed what, when, why) protects the agent in audits.

---

## Information technology

### Typical context

Software development teams face the constant challenge of producing quality code at scale, with rigorous reviews, up-to-date technical documentation and fast defect resolution. This vertical is the method's natural origin: short iterative cycles, native traceability (git), multiple technical roles, and the need for every change to be auditable and reversible. The pressure for speed without sacrificing security and maintainability is what lets the method deploy its full power here.

### Role mapping

- **Human authority:** the tech lead or repository owner, who approves or rejects the final merge.
- **Director:** a higher-capability model that breaks the feature or bug down into atomic tasks, defines clear acceptance criteria and creates the work order.
- **Drafter:** a fast model that writes the code, unit tests and documentation from the work order, without straying from scope.
- **Reviewer/guardian:** an independent model or a senior human that audits the diff against the work order: logical correctness, security, adherence to the project's styles and conventions.

### The work order here

It is the ticket or task specification: "implement an endpoint that returns user data" with explicit acceptance criteria (passing tests, API documentation, error handling). The "MUST NOT touch" is critical:
- Files or modules outside the declared scope.
- Secrets, credentials or sensitive configuration.
- Unapproved external dependencies.
- Public APIs or contracts that would break backward compatibility.

### Where severity rises

Review escalates to a human (or an independent senior) when the code touches security, authentication, payments, personal data, production infrastructure or irreversible changes (data migrations, mass deletions). A one-line fix in an internal script, by contrast, can flow through a lighter cycle. Proportionality is key: the review effort scales to the plausible harm.

### Memory, traceability and industrialization

- **Memory:** files of architectural decisions, repo conventions (how variables are named, where tests go, preferred patterns), known technical debt.
- **Traceability:** git is native here: each commit is an auditable unit of change, the diffs show exactly what changed, and a revert is a one-line operation.
- **Industrialization:** a skill loaded/configured with the project's conventions; hooks that run linters, tests and secret scanning automatically before every commit/merge (enforcement); a "security reviewer" subagent with the domain context preloaded.

### Concrete benefit

The team produces maintainable, secure code with no human bottleneck: the authority approves the critical, the director splits into pieces, the drafter delivers fast, the independent reviewer audits. Every change is recorded, reversible and fully traceable. Scale goes up without degrading quality.

---

## Reusable template: map your own vertical

The verticals above are examples. The method does not depend on the industry: it depends on the *roles*, the *work orders* and *proportionality*. To take it to your field — health, legal, education, finance, customer service, whatever it is — copy this template and answer each question for your context.

### Typical context
*What gets produced repeatedly in your vertical, at scale, where quality and consistency matter? What is the central pressure (time, volume, compliance)?*

### Role mapping
*Who is the **human authority** that approves and answers for what is published? Who plays **director** (defines what gets done and splits it)? What does the **drafter** generate? What does the independent **reviewer/guardian** check?* — The method's roles do not change; you just put a face to them in your industry.

### The work order here
*What is the typical unit of work (the "order")? And most importantly: what is your **"MUST NOT touch"** field — what must never be invented, modified or crossed — in your domain? (It is usually the legal, the regulatory, whatever creates liability or harm.)*

### Where severity rises
*Which tasks, if they go wrong, cause the worst plausible harm? Those trigger a more capable executor and a higher-level reviewer (up to a human expert). Which ones, by contrast, are trivial and do not deserve the full cycle?*

### Memory, traceability and industrialization
*What context must persist across sessions (memory: continuity files, not a database)? What is worth versioning so you can revert and audit? Which repeated interaction could you industrialize with a **skill** (knowledge loaded/configured), a **hook** (automatic enforcement) or a **subagent** (a preloaded role)?*

### Concrete benefit
*When you finish: what do you concretely gain? Usually: scaling volume without losing quality or compliance, with a human approving only what matters, and full traceability of who did what and why.*

---

> **A reminder on honesty.** If you adapt this to your vertical, keep the distinction between the *illustrative* (how it would map) and the *real* (what actually happened). Presenting a hypothetical case as real is exactly the failure mode the method is designed to catch.
