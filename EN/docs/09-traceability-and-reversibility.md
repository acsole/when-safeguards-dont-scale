## 9. Traceability and reversibility

In any collaboration between humans and AI, there is a risk that an unrequested change — or one executed out of scope — reaches the final files without review. The working method protects against this with **four layers of safety** that work together: they prevent the harm before it happens, contain it if it happens, detect it the moment it appears, and revert it if necessary.

### The four layers

| Layer | Question it answers | Mechanism |
|-------|---------------------|-----------|
| **Prevention** | How do I keep the executor from touching the files directly? | The executor never persists changes to the source code or to consolidated files. It drafts and *returns* the content (in Markdown, in its reply). Only the director or the human consolidates into the files. That way, an executor's error overwrites nothing. |
| **Containment** | If something does get written, where is it contained? | Changes live in **separate spaces** (drafts, git branches, temporary files) until approval. They never overwrite what is approved *in place*. The harm, if any, stays isolated. |
| **Detection** | How do I know there was a deviation? | The work order's **"MUST NOT touch"** field (Module 5) is an explicit contract about scope. If the output violates it, that is an immediate red flag. The reviewer checks the output against the contract. |
| **Recovery** | How do I go back if something went wrong? | **Version control** (git). Each consolidated change is a *commit* — a full snapshot with its message and a signature of who and when. A commit is a reversible return point; any damage is reversible in seconds. |

### The hard rule: return, don't persist

The executor **returns content**, it does not persist files. This separation is deliberate: it turns the executor into a low-trust "black box". Its output is **raw material**, always subject to review and approval before it enters the system. The human or the director decides whether to write, when and where. This barrier is stronger than any folder permission or token.

### Git as a safety net

The versioned repository is the **Recovery layer** in action. Each module consolidated in this document is a *commit*: a line in the history that shows who wrote what, when and why. That commit's *diff* is the "breadcrumbs" — the readable proof of every change.

A common trap: encrypting or minifying files *before* committing. This destroys the readable diffs — it kills the Detection layer. Confidentiality is protected in other ways (a private repository, access control), not by encrypting before versioning.

### A critical distinction: versioning vs. memory

Git is the *version history of the files* — commits, diffs, return points. Context continuity across sessions — the persistent memory that lets the AI resume work without losing the thread — is a different mechanism, covered in Module 4. They should not be confused: versioning tracks changes *in the files*; memory tracks *the collaboration's context*. Both are necessary, but they operate at different layers.

### The full flow

A change follows this route:

1. The human approves a plan with its limits ("MUST NOT touch").
2. The executor returns content.
3. The reviewer checks it against the contract (Detection layer).
4. The director or human writes to the files (Prevention).
5. A commit is made with a clear message (Recovery).

If something fails at step 3, it is rejected and never reaches step 4. If something fails afterward, the diff and the history are the net that catches the error and reverts it.

**Traceability and reversibility are synonyms in this method.** You don't trust; you verify and keep a record.

---
