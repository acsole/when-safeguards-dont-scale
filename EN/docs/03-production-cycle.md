## 3. The production cycle

A task in the AI working-method does not appear ready-made out of nowhere. It goes through a deliberate operational cycle where each role intervenes in order, with clear validation points and chances to reject, redo and improve. This cycle guarantees that nothing is executed without having been thought through, reviewed and approved by the human authority.

### The operational flow

The cycle begins when the human authority and the Director **talk to define an objective** — not a task yet, but a skeleton: what we want to achieve, why, and in what context. From that skeleton, the Director splits the work into **atomic tasks** (described in work orders, as detailed in Module 5). Each work order is an indivisible, clear, self-contained unit.

Then the **Drafter executes**: it takes a work order, consults its references, produces the output (code, prose, design, analysis). When it finishes, it hands back a report of the work done.

Here the **Reviewer** comes in: it audits the output against objective criteria (does it respect the schema? does it meet the work order? are there inconsistencies with what is already written?). If the review passes, it moves on. **If it fails, it rejects with concrete feedback and the work order goes back to the Drafter.**

```
Human authority           Director                 Drafter               Reviewer
     |                       |                        |                    |
     +-- Defines skeleton ---+                        |                    |
                             |-- Creates work orders->|                    |
                             |                     Executes                |
                             |                        +--- Audits ---->|   |
                             |                        |<--- Rejects ---+   |
                             |                        +--- Rewrites -->|   |
                             |                        |<--- Approves --+   |
                             |<-- Delivers result ----|
     |<-- Verifies, doesn't trust --|
     |-- Final approval --------|

   [↻ Automation checkpoint: evaluated on EVERY turn of the cycle]
```

### The "verify, don't trust" principle

A report from the Drafter is not enough. The **Director verifies independently** before taking anything as good: it re-reads the output, checks the references, runs objective checks where they apply (tests, real changes to the code, consistency against documentation). Only after this personal verification can the Director tell the human authority: "this is ready."

The human authority, as the final instance, **approves** or proposes changes. That approval is the permission to consolidate the result and integrate it into the project.

### The automation checkpoint

On every cycle, while delivery and review are happening, someone asks: **is this interaction we keep repeating worth automating?** For example, if the Reviewer has to audit the same kind of thing again and again against the same criteria, maybe an automated tool could do it. This checkpoint is recurring; it has no fixed criteria (that is the subject of Module 6), but its presence is constant.

### The reject-and-retry path

If the review fails, it is not failure: it is correction. The Reviewer returns the work order with specific feedback. The Drafter rewrites, and the whole cycle iterates until the output passes review. Then the human authority approves.

### Living proof

This very document — the "AI Working-Method" — is being produced with this cycle. The skeleton was defined by the human authority and the Director. Each module is a work order. The Drafter produces text. The Reviewer audits, rejects pieces when necessary, and asks for rewrites. Only when it passes review does the human authority approve consolidation. Some modules needed more than one round of correction before being approved.

The cycle is not a theoretical fantasy: it is live, iterative, and it works.
