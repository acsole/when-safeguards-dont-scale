## 8. Limits, and when not to use the method

The multi-model coordination method is not universally superior. Its value lies in *proportionality*: it should be applied where its benefits genuinely outweigh its costs. When they do not, the method becomes an unnecessary obstacle.

### When the overhead exceeds the benefit

The method introduces deliberate latency and complexity. Each task passes through several stages: initial skeleton, writing work orders, execution, review, often with rounds of iteration. That demands coordination across multiple models, amplified token consumption and waiting on human approvals. For trivial, exploratory or one-off tasks, that cost is unsustainable.

Examples that do *not* justify the full cycle:
- A quick question whose answer is thrown away afterward.
- A one-line fix in code or documentation.
- A throwaway draft to "see what comes out".
- An exploration with no consequences if it fails.

In these cases, consulting a robust model directly is more efficient.

### The method's real costs

- **Coordination time:** a sequence of human approvals, handoffs between models.
- **Token consumption:** each model processes the previous ones' context, amplifying the spend.
- **Latency:** slower than a linear execution, especially on low-severity tasks.

It is honest to acknowledge that the method is deliberately *more expensive* than asking a single model to act in one shot.

### The assumptions the method rests on (and what happens if they fail)

1. **A human available to approve.** If the human cannot review within a reasonable time, the bottleneck grows and the method collapses.
2. **Well-written work orders.** An ambiguous, incomplete or poorly specified work order corrupts the whole chain; no amount of review makes up for it.
3. **Models of differentiated capability.** Without access to models with clear roles (a nimble executor, an expert reviewer, an evaluating director), the method loses its structure.

If any of these assumptions fails, the method does not mitigate risk; it simply slows the work down.

### Limits on infallibility

The method *reduces* risk, it does not eliminate it. No model — not the reviewer, not the director — is infallible. A review can let subtle errors through; a human can approve something deficient. The method is a rain cover, not a guarantee of staying dry.

### A sign of maturity

Knowing when *not* to use the method matters as much as knowing when to. Applying it dogmatically to everything is as much a mistake as abandoning it out of impatience. The real competence is in calibrating: high-impact, complex tasks deserve the full cycle; trivial tasks deserve speed. That calibration is a shared responsibility between the AI and the human authority.
