# Template: work order

> The work order is the method's central tool. It defines **one** atomic task: its scope, its
> boundaries and its acceptance criterion. Without it, the executor guesses and the reviewer has
> nothing to check against.
>
> A hard rule that accompanies every work order: **the executor returns content, it does not
> persist files.** Consolidating is the director's or the human's job.
>
> Conceptual basis: [`docs/05-atomicity-rules.md`](../docs/05-atomicity-rules.md).
> Real, worked examples: [`work-orders/`](../work-orders/).

---

## Work order N — [Task title]

- **Purpose:** the "what for" in one line. If it does not fit in one line, the task is too broad
  and must be split.

- **Target length:** a concrete, verifiable range (for example, 450-600 words). A number lets the
  reviewer **count** it instead of estimating by eye.

- **Questions it must answer:** the questions guide the content without writing it.
  1. ...
  2. ...
  3. ...

- **Must contain:** a **closed** checklist of verifiable points. Not prose, a list the reviewer
  runs through point by point. If a point cannot be verified by reading the delivery, it does not
  go here.
  - [ ] ...
  - [ ] ...

- **MUST NOT touch:** the highest-leverage field of the whole work order. It explicitly lists what
  stays out, even if it looks related. It is what keeps two tasks from stepping on each other, and
  it is also the contract the Detection layer compares the output against.
  - ...
  - ...

- **Anchor / real example:** the concrete case the delivery must cite. **Hand it over already
  verified.** Giving the executor verified facts before writing reduces fabrication far more than
  catching it afterward.

- **Mistakes to avoid:** a negative list of known anti-patterns for this kind of task.

- **Key terms:** a mini-glossary, so the vocabulary does not drift between tasks done by different
  executors or in different sessions.

- **Inputs:** what the executor is handed to start. Documents, context, examples.

- **Output form:** format, length, tone. And if it applies, the hard rule that it returns content
  in the reply, without writing files.

- **Definition of done:** the exact yardstick the reviewer measures it against. Written from the
  reader: "when finished, someone can do X without consulting again".

---

## Signs the work order is badly written

- **The "MUST NOT touch" is very long.** A sign the task is too broad: split it.
- **The work order drafts instead of bounding.** If you write the content for the executor, you
  shifted the work to the reviewer.
- **The "Must contain" is a diffuse intention** instead of a closed list. Then the omission of a
  mandatory element does not jump out in review, which is the hardest failure mode to see.
- **There is no number in the length.** Without a number, the check becomes an opinion.
