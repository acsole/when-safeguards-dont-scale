# Incident log

This method was built by using itself. Each module of its documentation was drafted by an economical model against a work order, audited by an independent reviewer, and only then approved and consolidated by the human authority. The files in this folder record **every failure that pipeline caught during the process**, with its severity, its correction and the lesson it left.

## Why it exists

A method that only publishes its successes gives you nothing to judge it by. These records exist for two concrete reasons:

1. **They show the detection net works.** Not as an abstract claim, but with dated cases traceable to the commit that fixed them.
2. **They calibrate the reviewer itself.** Each entry describes a failure mode, and the failure modes turned out to be recurring and predictable, not stray accidents.

What makes this log different is that it **includes the failures of the system's upper layers, not just those of the cheap drafter**. The reviewer caught fabrications the director had already read and approved. And on another occasion the director caught a false alarm the reviewer had raised by estimating instead of measuring. No layer turned out to be infallible, and that is exactly the argument for having several.

## What's here

| Record | What it documents |
|---|---|
| [`working-method-incidents.md`](working-method-incidents.md) | Eight incident sessions during the writing of the canonical document (M1-M9), plus the closing that summarizes them |
| The adoption guide's log | Still lives inside [`installation/installation-guide.md`](../installation/installation-guide.md), in its Appendix A. It will move here when the guide is complete |

## The failure modes catalogued so far

From the drafter: **fabrication** (inventing figures, quotes or mechanisms to sound verifiable), **redundancy** (repeating a concept until it breaks a hard length limit), **omission** of a mandatory element of the work order, **embellishment** of a real fact, and **leak of an internal proper name** into a document meant for external readers.

From the reviewer: **false positive** from estimating by eye instead of counting.

From the director: **leniency** toward the failure mode it does not detect itself.

## The most useful finding

The Module 6 entry records that that module had **zero fabrication**, unlike the earlier ones. The only difference was the input: the drafter was handed the real, already-verified examples before writing. Restricting the generation surface with concrete facts reduces invention far more than catching it afterward.

Put another way: **detection is the last net, not the first.**
