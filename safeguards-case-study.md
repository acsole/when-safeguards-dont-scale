# Safeguards Case Study
### Reading my own AI-assisted project through the lens of AI safeguards, and asking what breaks when it scales

**Author:** Andrés Curcio Sole

> **Status:** living document, work in progress. I draft it through the same multi-agent pipeline it describes: a drafting model works against a work order I write, an independent reviewer model audits the draft against that order, and I approve, reject or rewrite every section before anything is committed.
> **Written so far:** Elevator Pitch, Context, The Four Layers, Artifact to Principle to Evidence, Threat Model, Where It Breaks at Scale.
> **Scoped but not yet written:** Calibrated Honesty (my limitations, stated plainly), Appendix on live verification (the commands to check every evidence path myself), and an Incident Log of the failures this pipeline catches while writing this document, recorded as they happen.
> **What this is not:** a claim of production-grade security. I describe safeguard design and the cases I have actually observed. I have no measured detection rate, and I do not claim one.

---

## Elevator Pitch

The safeguards that protect my single-user application (human approval gates, automated checks, audit trails) may degrade or fail outright when the same design is scaled to an adversarial population. This case study examines a real project I built with those mechanisms from the start: deny-by-default governance, quality checkpoints across agent workflows, and traceability hooks that have caught policy violations in supervised operation. I trace each safeguard from my own oversight as a single founder to population-scale pressure, separating the principles that hold under adversarial stress from the fractures that only appear in production. The question I care about is whether mechanisms designed for one trusted supervisor can survive when millions of users, thousands of concurrent agents, and bad actors probe the same checkpoints at the same time. My answer, worked out below, is that they cannot, and that the reason is structural rather than technical.

---

## Context: The System Under Study

### The Remanso Project

Remanso is a project I started alone, with zero capital. (I named it CalmKit first, then Vitalis the App, and renamed it Remanso in July 2026. The production URL still carries the earlier name.) It is a family of free Progressive Web Applications for wellbeing problems people actually have: anxiety, sleep, burnout, digestion. People reach it through organic search, not paid acquisition. **It has no monetization of any kind: no advertising network, no affiliate marketing, no paid tier.** I had planned to introduce advertising and I abandoned that plan in July 2026, then removed the preparatory advertising code from the codebase. The stack is deliberately constrained: plain HTML5, CSS3 and ES6+ JavaScript with no external frameworks, Service Workers for offline use, browser-native storage, and free static hosting. What I want is for this to keep serving people without venture capital, using AI assistance to multiply what one person can build.

The reason this project is worth reading through a safeguards lens is its domain. These tools touch mental health and physical wellbeing, where wrong advice or unsupervised AI output can hurt someone. So I built the project on a rule: anything that could be misread as a substitute for medical or psychological advice carries the legally required disclaimers, and I review and approve the wording before it is published. The governing charter I wrote for the project says it directly, and I mean it as a constraint on myself as much as on the AI: honor life, care for it, protect it, and do not harm it.

### The Multi-Agent Working Method

Rather than lean on a single model, I split the work across several, matching the model to the job. A high-reasoning model acts as director: it plans, questions my assumptions, pushes back, and breaks work into atomic tasks. A mid-tier model acts as an independent quality guardian, auditing each draft for consistency, accuracy and compliance with its constraints. A fast, cheap model drafts the atomic pieces against a work order that states not only what the piece must contain but explicitly what it must not touch.

This is not autonomous multi-agent reasoning, and I want to be precise about that because the distinction is the whole point. Every output waits for me. I review every substantive decision before any code is written, deployed or published, and a proposal does not proceed without my explicit approval. Between sessions, a file-based memory of git-tracked markdown files carries forward the decisions, constraints and lessons already settled, so that continuity does not depend on any single conversation staying alive.

### The Monitoring Dashboard

In parallel I maintain a monitoring dashboard that shows me the state of several projects at once, built in plain JavaScript with Web Components and no dependencies. Two principles in it are non-negotiable for me. The first is data honesty: what the dashboard shows has to be true, and I will not let it fabricate a number to display progress that has not happened. The second is automated enforcement: a hook inspects edits to the dashboard's core `.js` files and blocks any edit that violates its `file://` architectural invariants, such as `import`, `export`, `type="module"` or `fetch()`. That hook has fired on real edits, mine included. The dashboard also keeps telemetry and audit logs, so there is a persistent record of what changed and when, which is what I need in order to check afterwards whether a safeguard boundary actually held.

### The User and What Is Protected

The supervisor in this system is one person: me. Three things are being protected. First, codebase integrity, so that changes stay inside the architecture and constraints I set. Second, my own decision authority, so that no AI commits a change, makes a strategic pivot or publishes anything without my explicit prior consent. Third, and the one that matters most, the wellbeing of whoever eventually uses these tools: every wellness tool that reaches a person carries its disclaimers and has passed a human review for its potential to do harm.

So this is a constrained, supervised environment: one human, known governance boundaries, explicit approval gates, persistent audit trails. What I want to examine is how that structure behaves when it stops being that. What happens to a design built for one founder and a small AI-assisted team when it meets an adversarial population, untrusted operators and distributed autonomous agents.

---

## The Four Layers

I think about defense in depth across four structural layers, each one catching a different kind of failure. The diagram below traces a single task through all four, showing where a malicious or mistaken directive gets intercepted, contained, detected, and recovered from. Here is how each layer works in my project.

**Prevention: stop bad actions before they happen.**
Bad directives never reach execution because the governance is written into the problem statement itself. The project's CLAUDE.md file codifies a deny-by-default rule, which I wrote in Spanish and render here as: "The AI will not execute any code, deployment or change without first presenting a clear plan and obtaining explicit approval from Andrés exclusively." That is not a guideline, it is a structural constraint on what the system is allowed to attempt. On top of it, every task is scoped by a work order that states what must be done and, just as explicitly, what must not be touched. One of my work orders might say that a section must contain the role boundaries, must not touch git history, and must not be written to a file or committed by the agent. The boundaries are unambiguous on purpose. An agent handed contradictory instructions, write this section but also modify nothing, faces a constraint it cannot satisfy, so it stays in the design phase instead of executing.

**Containment: limit what a component can do, so a failure stays bounded.**
Even when prevention fails, the blast radius has to stay small. The drafting agent in my pipeline can only return text. It has no permission to write files, commit to git or deploy. If its output contains a serious error, the damage is confined to a chat message that the next layer can reject, and the file system and repository are untouched. Compare that with an executor that can write and commit without review: there, a corrupted file is live until somebody notices. With the drafter restricted to text, I see the error before anything is persisted.

**Detection: notice when something has gone wrong.**
A second, independent role audits each draft against its work order before I accept it, checking field by field. Is the required content there? Is the tone right? Are the assumptions grounded? During the pilot run of Module 1 of my method documentation, that reviewer caught that the anchor to real projects was missing, a semantic flaw that both the director model and I had read straight past. Every change lands as its own git commit, so the history stays reviewable and I can see what changed and decide whether to accept it or revert.

**Recovery: restore a good state after a failure.**
I persist each accepted section as a distinct commit, which preserves the full history and lets me return to any earlier state. A persistent memory of markdown files records the decisions I have made and the problems I have already resolved, so when something recurs in a later session the solution is documented rather than rediscovered.

<p align="center">
<svg width="880" height="380" viewBox="0 0 880 380" xmlns="http://www.w3.org/2000/svg" font-family="Segoe UI, Helvetica, Arial, sans-serif" role="img" aria-label="A single task traversing the four defense-in-depth layers: Prevention, Containment, Detection, Recovery.">
  <title>A single task traversing the four defense-in-depth layers</title>
  <defs>
    <marker id="arrow" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto" markerUnits="strokeWidth">
      <path d="M0,0 L7,3 L0,6 Z" fill="#3b5566"/>
    </marker>
    <marker id="arrowRed" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto" markerUnits="strokeWidth">
      <path d="M0,0 L7,3 L0,6 Z" fill="#b25b4a"/>
    </marker>
  </defs>

  <!-- Task token -->
  <rect x="18" y="150" width="96" height="56" rx="10" fill="#eef3f6" stroke="#3b5566" stroke-width="1.5"/>
  <text x="66" y="174" text-anchor="middle" font-size="13" font-weight="600" fill="#22343f">Task</text>
  <text x="66" y="192" text-anchor="middle" font-size="11" fill="#5a7180">(directive)</text>

  <!-- Layer columns -->
  <!-- Prevention -->
  <rect x="150" y="110" width="150" height="136" rx="12" fill="#f3f7f4" stroke="#4a7a5d" stroke-width="1.5"/>
  <text x="225" y="98" text-anchor="middle" font-size="14" font-weight="700" fill="#2f5a40">1 · Prevention</text>
  <text x="225" y="150" text-anchor="middle" font-size="11.5" fill="#3d5346">deny-by-default</text>
  <text x="225" y="168" text-anchor="middle" font-size="11.5" fill="#3d5346">human approval</text>
  <text x="225" y="186" text-anchor="middle" font-size="11.5" fill="#3d5346">scoped work orders</text>
  <text x="225" y="218" text-anchor="middle" font-size="10.5" font-style="italic" fill="#6a7f70">blocks before start</text>

  <!-- Containment -->
  <rect x="340" y="110" width="150" height="136" rx="12" fill="#f3f6f8" stroke="#3f6b86" stroke-width="1.5"/>
  <text x="415" y="98" text-anchor="middle" font-size="14" font-weight="700" fill="#2c4f66">2 · Containment</text>
  <text x="415" y="150" text-anchor="middle" font-size="11.5" fill="#36495a">drafter returns</text>
  <text x="415" y="168" text-anchor="middle" font-size="11.5" fill="#36495a">text only —</text>
  <text x="415" y="186" text-anchor="middle" font-size="11.5" fill="#36495a">no write, no commit</text>
  <text x="415" y="218" text-anchor="middle" font-size="10.5" font-style="italic" fill="#6a7c89">blast radius = text</text>

  <!-- Detection -->
  <rect x="530" y="110" width="150" height="136" rx="12" fill="#f7f5f3" stroke="#8a6d3f" stroke-width="1.5"/>
  <text x="605" y="98" text-anchor="middle" font-size="14" font-weight="700" fill="#6b5226">3 · Detection</text>
  <text x="605" y="150" text-anchor="middle" font-size="11.5" fill="#5a4a36">independent</text>
  <text x="605" y="168" text-anchor="middle" font-size="11.5" fill="#5a4a36">guardian review</text>
  <text x="605" y="186" text-anchor="middle" font-size="11.5" fill="#5a4a36">+ reviewable diffs</text>
  <text x="605" y="218" text-anchor="middle" font-size="10.5" font-style="italic" fill="#897a64">catches bad drafts</text>

  <!-- Recovery -->
  <rect x="720" y="110" width="150" height="136" rx="12" fill="#f6f3f6" stroke="#71527f" stroke-width="1.5"/>
  <text x="795" y="98" text-anchor="middle" font-size="14" font-weight="700" fill="#553f60">4 · Recovery</text>
  <text x="795" y="150" text-anchor="middle" font-size="11.5" fill="#4a3a52">revertible commits</text>
  <text x="795" y="168" text-anchor="middle" font-size="11.5" fill="#4a3a52">+ persistent</text>
  <text x="795" y="186" text-anchor="middle" font-size="11.5" fill="#4a3a52">memory</text>
  <text x="795" y="218" text-anchor="middle" font-size="10.5" font-style="italic" fill="#7d6a87">restores good state</text>

  <!-- Flow arrows (accepted path) -->
  <line x1="114" y1="178" x2="148" y2="178" stroke="#3b5566" stroke-width="1.6" marker-end="url(#arrow)"/>
  <line x1="300" y1="178" x2="338" y2="178" stroke="#3b5566" stroke-width="1.6" marker-end="url(#arrow)"/>
  <line x1="490" y1="178" x2="528" y2="178" stroke="#3b5566" stroke-width="1.6" marker-end="url(#arrow)"/>
  <line x1="680" y1="178" x2="718" y2="178" stroke="#3b5566" stroke-width="1.6" marker-end="url(#arrow)"/>

  <!-- Rejection routes (downward) -->
  <line x1="225" y1="246" x2="225" y2="300" stroke="#b25b4a" stroke-width="1.4" stroke-dasharray="5,4" marker-end="url(#arrowRed)"/>
  <line x1="605" y1="246" x2="605" y2="300" stroke="#b25b4a" stroke-width="1.4" stroke-dasharray="5,4" marker-end="url(#arrowRed)"/>
  <text x="225" y="320" text-anchor="middle" font-size="10.5" fill="#a0503f">refused / not started</text>
  <text x="605" y="320" text-anchor="middle" font-size="10.5" fill="#a0503f">rejected → re-draft</text>

  <!-- Recovery loop back -->
  <path d="M795 246 L795 340 L225 340 L225 340" fill="none" stroke="#71527f" stroke-width="1.3" stroke-dasharray="4,4"/>
  <line x1="225" y1="340" x2="120" y2="340" stroke="#71527f" stroke-width="1.3" stroke-dasharray="4,4" marker-end="url(#arrow)"/>
  <text x="470" y="357" text-anchor="middle" font-size="10.5" fill="#6b5179">revert / re-attempt from a known-good state</text>

  <!-- Output -->
  <text x="795" y="262" text-anchor="middle" font-size="10.5" font-weight="600" fill="#2f5a40">✓ accepted commit</text>
</svg>
</p>

*Figure 1. A single task traversing the four layers. The solid path is the accepted route. The dashed red routes show where Prevention and Detection intercept a faulty directive, and the purple loop shows Recovery returning the system to a known-good state.*

---

## Artifact → Principle → Evidence

Here I map each governance artifact (the documents, hooks, commits and practices that make the system run) to the safeguards principle it embodies and to where it lives. I do this because I do not want the claims in this document to rest on assertion. Thirteen years in QA taught me to distrust a claim I cannot verify, including my own. The public evidence for this document is its own git history, in this repository; the remaining artifacts live in the private working environment where I built the system, and I describe them rather than expose their internal layout. The diagram after the table summarizes the relationships.

| Artifact | Safeguards principle | Evidence (verified path / ref) |
|----------|----------------------|--------------------------------|
| Governance charter: deny-by-default, the AI proposes and I approve | Human-in-the-loop, deny-by-default | The project's root governance charter (its auto-loaded context file), in the private workspace |
| Work orders that scope each task ("must contain", "must not touch") | Task scoping, least authority | The work-orders file in the project's working-method folder (private workspace) |
| Canonical method document: roles, and the drafter returns text only and cannot write or commit | Containment, no persistence by the executor | The method document in the same working-method folder (private workspace) |
| Independent quality-guardian review, a different role audits each draft | Detection, separation of duties | Per-section commits in this repository's git history |
| Automated enforcement hook that blocks edits violating the `file://` invariants | Automated guardrail, policy enforcement | An automated enforcement hook in the author's local environment |
| Telemetry hook that records tool activity | Audit logging, observability | A telemetry hook in the author's local environment |
| Per-section commits plus project seed commits | Traceability, recovery | Seed and per-section commits in the project's private repository |
| Data-honesty principle: never fabricate a dashboard metric | Truthfulness, no fabrication of data | The dashboard's data and state layer. Note honestly: this is a convention I hold myself to, not a rule enforced in those files |
| Incident Log recording the failures this pipeline caught in itself | Calibrated honesty, transparency about failure | Scoped in my work-orders file but **not yet written**. Entries accumulate as the pipeline catches its own failures |

The public trail for this document is its own commit history, which anyone can query from this repository. The other artifacts sit in the private environment where the system runs; I describe them here rather than expose their paths. Here I am only concerned with the mapping.

<p align="center">
<svg width="920" height="540" viewBox="0 0 920 540" xmlns="http://www.w3.org/2000/svg" font-family="Segoe UI, Helvetica, Arial, sans-serif" role="img" aria-label="A bipartite map connecting nine governance artifacts on the left to six Safeguards principles on the right.">
  <title>Mapping of governance artifacts to Safeguards principles</title>

  <!-- connecting lines (drawn first, behind boxes) -->
  <line x1="280" y1="70"  x2="640" y2="95"  stroke="#4a7a5d" stroke-width="1.6"/>
  <line x1="280" y1="123" x2="640" y2="175" stroke="#4a7a5d" stroke-width="1.6"/>
  <line x1="280" y1="176" x2="640" y2="255" stroke="#3f6b86" stroke-width="1.6"/>
  <line x1="280" y1="229" x2="640" y2="335" stroke="#8a6d3f" stroke-width="1.6"/>
  <line x1="280" y1="282" x2="640" y2="415" stroke="#3b5566" stroke-width="1.6"/>
  <line x1="280" y1="335" x2="640" y2="415" stroke="#3b5566" stroke-width="1.6"/>
  <line x1="280" y1="388" x2="640" y2="415" stroke="#3b5566" stroke-width="1.6"/>
  <line x1="280" y1="441" x2="640" y2="495" stroke="#71527f" stroke-width="1.6"/>
  <line x1="280" y1="494" x2="640" y2="495" stroke="#71527f" stroke-width="1.6"/>

  <!-- column headers -->
  <text x="155" y="30" text-anchor="middle" font-size="13" font-weight="700" fill="#22343f">Governance artifact</text>
  <text x="770" y="30" text-anchor="middle" font-size="13" font-weight="700" fill="#22343f">Safeguards principle</text>

  <!-- left: artifacts -->
  <g font-size="11.5" fill="#22343f">
    <rect x="30" y="51"  width="250" height="38" rx="8" fill="#eef3f6" stroke="#3b5566"/><text x="42" y="74">CLAUDE.md — governance charter</text>
    <rect x="30" y="104" width="250" height="38" rx="8" fill="#eef3f6" stroke="#3b5566"/><text x="42" y="127">fichas-de-encargo.md — work orders</text>
    <rect x="30" y="157" width="250" height="38" rx="8" fill="#eef3f6" stroke="#3b5566"/><text x="42" y="180">metodo-de-trabajo.md — method doc</text>
    <rect x="30" y="210" width="250" height="38" rx="8" fill="#eef3f6" stroke="#3b5566"/><text x="42" y="233">quality-guardian review (Sonnet)</text>
    <rect x="30" y="263" width="250" height="38" rx="8" fill="#eef3f6" stroke="#3b5566"/><text x="42" y="286">enforcement hook</text>
    <rect x="30" y="316" width="250" height="38" rx="8" fill="#eef3f6" stroke="#3b5566"/><text x="42" y="339">telemetry hook</text>
    <rect x="30" y="369" width="250" height="38" rx="8" fill="#eef3f6" stroke="#3b5566"/><text x="42" y="392">git history / per-section commits</text>
    <rect x="30" y="422" width="250" height="38" rx="8" fill="#eef3f6" stroke="#3b5566"/><text x="42" y="445">dashboard data-honesty convention</text>
    <rect x="30" y="475" width="250" height="38" rx="8" fill="#eef3f6" stroke="#3b5566"/><text x="42" y="498">Incident Log (this document)</text>
  </g>

  <!-- right: principles -->
  <g font-size="11.5" font-weight="600">
    <rect x="640" y="73"  width="260" height="44" rx="8" fill="#f3f7f4" stroke="#4a7a5d"/><text x="652" y="91" fill="#2f5a40">Human-in-the-loop +</text><text x="652" y="107" fill="#2f5a40">deny-by-default</text>
    <rect x="640" y="153" width="260" height="44" rx="8" fill="#f3f7f4" stroke="#4a7a5d"/><text x="652" y="171" fill="#2f5a40">Least authority /</text><text x="652" y="187" fill="#2f5a40">task scoping</text>
    <rect x="640" y="233" width="260" height="44" rx="8" fill="#f3f6f8" stroke="#3f6b86"/><text x="652" y="259" fill="#2c4f66">Containment</text>
    <rect x="640" y="313" width="260" height="44" rx="8" fill="#f7f5f3" stroke="#8a6d3f"/><text x="652" y="331" fill="#6b5226">Detection /</text><text x="652" y="347" fill="#6b5226">separation of duties</text>
    <rect x="640" y="393" width="260" height="44" rx="8" fill="#eef3f6" stroke="#3b5566"/><text x="652" y="411" fill="#22343f">Automated guardrail ·</text><text x="652" y="427" fill="#22343f">audit · recovery</text>
    <rect x="640" y="473" width="260" height="44" rx="8" fill="#f6f3f6" stroke="#71527f"/><text x="652" y="491" fill="#553f60">Truthfulness /</text><text x="652" y="507" fill="#553f60">calibrated honesty</text>
  </g>
</svg>
</p>

*Figure 2. Each governance artifact maps to the safeguards principle it embodies. Line colors echo the four-layer model of Figure 1: green for Prevention, blue for Containment, amber for Detection, slate for automated guardrail, audit and recovery, purple for truthfulness.*

---

## Threat Model: The Single-User Baseline

At its current scale, one founder working with Claude across a persistent session, I see five concrete failure modes that could undermine the safeguards or reach the people who eventually use these tools. The defenses are the four layers above. This section stays on the threats themselves.

**Hallucination and fabrication.** The model can produce plausible-sounding falsehoods: invented file paths, commit hashes that do not exist, quotes that were never said, citations to evidence that is not there. This is not hypothetical for me. It has already happened inside the pipeline that writes this very document, where sections came back with fabricated quotes and distorted references that only surfaced when I reviewed them. If a hallucination reached user-facing copy, for instance a wellbeing tip framed as research-backed when no such research exists, it would reach real people because I failed to catch it before publishing.

**Constraint drift.** Across a long session, or across several, the model can drift from the scope and conventions we agreed on: shifting what a work order was meant to say, quietly widening what it believes it should do, reading a guardrail a little more loosely each time. What worries me here is not one large violation. It is the incremental loosening that erodes the deny-by-default posture until a boundary that was once sharp has gone soft.

**Harm through health-adjacent content.** These tools touch anxiety, sleep, burnout and digestion, and a person can reasonably read guidance in those areas as medical or psychological advice. If the model writes authoritatively about a health condition without the right hedging and disclaimers, someone using the tool later could be misled or hurt. At this scale I have to catch every single instance before it ships. If my gate fails, harmful content reaches people.

**Loss of the human gate.** The core rule is deny-by-default: the AI proposes, I approve, then implementation happens. If the model starts executing, committing code, deploying or publishing without that approval, the safeguard is simply gone. It can happen through overt disobedience, or more insidiously through reframing, where a change is presented as too small to count as an action and the approval step is skipped on that basis.

**Scope leakage.** Tasks have boundaries. The model can touch files, dependencies or concerns it was never asked to address: drafting content for a different subsystem, changing shared configuration without coordination, or blurring the roles of drafter, reviewer and director into each other. Every one of those bleeds costs clarity and introduces inconsistency that I then have to detect and correct.

---

## Where It Breaks at Scale

Strip away the implementation detail and nearly every safeguard I have described rests on the same scarce resource: the judgment of one trusted human. Deny-by-default works because one person can review what one agent proposes before anything is committed. Detection works because that same person, or someone equally accountable, can look at every diff before it lands. Containment works because a human, not the executor, decides what gets persisted. Recovery works because the history that person curates is short enough to read and linear enough to revert. None of this is a property of the algorithms. It is a property of having exactly one well-calibrated decision-maker in the loop with enough time to look at everything that matters. That person is the keystone of the whole architecture, and scale is precisely the force that pulls the keystone out first.

Scale does something else that is easy to miss if the analysis stays mechanical: it changes the nature of the threat. Every failure mode I listed above (hallucination, drift, an over-eager edit) is accidental. Nothing in my system is trying to defeat the safeguards, and the worst case is a mistake that a careful human catches. At population scale, with an adversary able to orchestrate many agents in parallel, the failures stop being accidental. The adversary is not making mistakes. The adversary is running a search. Tens of thousands of agents probing a system are, functionally, an optimization process looking for the seam between safeguards: the input the reviewer did not sample, the queue depth that forces a rubber stamp, the edit that is individually compliant and jointly harmful. The question the architecture has to answer changes from "how do we catch errors nobody intended" to "how do we withstand pressure that is intended, sustained and adaptive." A safeguard that comfortably absorbs accidents can still fail completely against optimization pressure, because accidents are bounded while an adversarial search actively redistributes its effort toward whatever is weakest.

What follows works through the four layers in order of fragility, which gives first and which second, using one adversary scenario threaded through all four so that the failures can be seen compounding instead of considered in isolation.

**The scenario.** An adversary controls on the order of tens of thousands of automated agents and points them at a system that nominally keeps the same four-layer defense I described: human approval at the front, independent review of outputs, an executor that proposes rather than persists, and a recoverable audit history. The adversary is not trying to break any single layer outright. It is looking, across all four at once, for the path of least resistance.

**1. Human-in-the-loop and deny-by-default, the first to break.** My version of this safeguard assumes human attention is effectively constant: one project, one founder, proposals arriving slowly enough that I can read each one, understand it, and approve or push back before the next arrives. The assumption that fails at scale is not that humans get worse at judging. It is that the volume of actions grows with the population while review capacity stays roughly fixed. Tens of thousands of agents submitting in parallel produce an approval queue that grows faster than any team of reviewers can clear it, and from there the system has three paths, all bad. It can hand approval to an automated policy, at which point the adversary stops attacking the human and starts attacking the policy, probing for the inputs it misclassifies, the edge cases its rules do not cover, the phrasing that slips past a filter built for different phrasing. It can let the human gate degrade in place, where reviewers under throughput pressure stop actually reading and start clicking approve to keep the queue moving: deny-by-default still exists on paper, but in practice it has become approve-by-exhaustion. Or the gate is removed outright, formally or not, because it has become the bottleneck and there is pressure to ship. The flood of agents is aimed exactly here. Not at getting any one request approved, but at pushing the queue past the point where careful review is humanly possible, forcing one of those three degradations.

**2. Detection, the independent review of every output.** In my version this safeguard assumes two things: that all output can be reviewed, and that the reviewer is trustworthy. Both erode at scale, in different ways. Volume defeats the first, because reviewing everything is only tractable while everything is small, so detection shifts from exhaustive review to sampling. The adversary's job then becomes characterizing the sampling window: through repeated low-stakes probing, tens of thousands of agents can map which classes of input draw scrutiny and which pass unexamined, and then route the harmful payload through the second kind. That is the direct continuation of the scenario, with the same agent population spending part of its volume learning what the reviewer does not look at and the rest exploiting it. The second assumption also stops being free. Reviewing my own project, I have no principal-agent problem. A population-scale system needs many reviewers drawn from a larger and less individually vetted pool, and it therefore has an insider-threat surface that my single-user version never had to account for at all.

**3. Containment, where the executor returns text and cannot persist.** My version of this assumes a human gate sits between proposal and persistence, so containment is really a restatement of Prevention's promise: nothing irreversible happens unless I approve it. But in this scenario layer one has already broken, and the queue has forced delegation, degradation or removal of that gate. Once it is gone, the executor can no longer wait for a human to act as the write barrier. Something has to persist state directly at the volume the system now runs at, or the system stops working. The blast radius changes accordingly. In my case the worst plausible outcome of a contained failure is a malformed chat message that never leaves the conversation. Once containment is relaxed to keep pace with volume, that same class of failure, one unremarkable bad edit, writes to production state that many people depend on. This is where the adversary's agents stop producing obviously harmful output, which detection might still catch at the margin, and start submitting edits that each pass every automated invariant in isolation while being harmful only in combination. Containment was never designed to catch that. It was built to stop one bad write, not to reason about the joint effect of ten thousand individually compliant ones.

**4. Recovery, revert and a persistent auditable history.** My version assumes a history that grows slowly, stays linear, and is small enough for me to read and pick the right point to revert to. At adversarial scale that fails on two fronts at once. First, with many agents committing concurrently, "revert to before the bad state" stops being well defined: there may be no clean point in a tangled history that excludes the damage without discarding large amounts of legitimate work, and even when such a point exists, the bad state has usually already propagated to users, so reverting the repository does not undo the harm. Second, the audit log that recovery depends on becomes an attack surface of its own. The sheer volume makes manual reconstruction infeasible, and an adversary able to generate that volume can also poison it, burying the signal of what actually happened inside enough noise that timely recovery stops being possible even in principle. That is the last compounding step: by the time anyone tries to reconstruct what the agent population did, the record they would use has been degraded by the same flood that defeated the first three layers.

Run end to end, the scenario shows something the four layers cannot show in isolation. A coordinated population of adversarial agents does not need to defeat any single safeguard outright. It only needs to apply enough simultaneous load that Prevention degrades into a rubber stamp, Detection's blind spots get mapped and used, Containment's removed gate widens the blast radius, and Recovery's audit trail grows too large and too contaminated to act on in time. Four failures that look independent are in fact one failure, propagating through a system whose layers all quietly depended on the same human bandwidth.

That leaves a perverse inversion, and I want to state it plainly because it is the thing I keep coming back to. As a system goes from one user to a population of thousands or millions, the stakes rise: health-adjacent harms, financial harms, harms compounding silently across many people before anyone notices, not just the predictable misjudgment of one founder reviewing his own work. By any reasonable account, the assurance should rise to match. But the safeguard that gave me the most assurance, direct and attentive human judgment applied to every action before it takes effect, is exactly the one that becomes unaffordable per action at the volumes where the stakes are highest. Severity climbs at the same time the keystone becomes impossible to keep in place. The next section turns to what this single-user case can and cannot honestly tell us about production scale, and where the analogy has to be handled with care.
