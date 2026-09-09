## 4. Persistent memory as a continuity asset

Every working session with the AI begins with no memory of the previous conversations. The LLM starts with no context about what was decided, what failed, what constraints govern the project, or where the work is headed. This "forgetting between sessions" is not a technical fault but a structural feature: the model responds based on what it receives in the current conversation, not on an automatic record of what happened before. That is why persistent memory is a critical asset that closes the gap.

Memory does not replace the code repository or the git history (see Module 9 for version control). Instead, it captures the *living context of the project*: decisions made, constraints not derivable from the code, agreements on how the AI should work, and references to external resources. Without this memory, each session restarts from zero, losing strategic and operational continuity.

### What gets saved and what does not

What gets **saved** are facts that resolve recurring questions: who the user is (roles, preferences, history), how the AI should behave (corrections, refinements, the why behind each agreement), the current project's goals and constraints, and links to external resources (boards, reference documents, live URLs).

What does **not** get saved: content that already lives in the code or the repository (functions, assets, versioned configuration); the full git history (that is the job of version control); or the ephemera of a one-off exchange (the steps of a debug that was resolved, ideas discarded within a single session).

### Organization: index and atomic files

Memory is structured as an **index file** that lists and summarizes every memory file, plus a collection of **thematic files** linked to one another. Each file addresses a discrete topic (for example, "user preferences", "project constraints", "architectural decisions"). The index acts as a map: it says what exists, where to find it, and one line on what it contains.

### The four types of memory

| Type | Content | What for |
|------|---------|----------|
| **User** | Role, preferences, history, who the person is | Personalize tone, understand intentions, respect limits |
| **Feedback** | Corrections, agreements on how the AI should work, the why behind each rule | Refine behavior without repeating the same mistake |
| **Project** | Current goals, constraints not derivable from the code, key decisions | Keep alignment and avoid regressions |
| **Reference** | URLs, boards, tickets, reference documents | Quick access without searching |

### Retrieval and continuity

When a session begins, the AI (or the person) consults the memory index as its entry point: it is the map that shows which files exist and what they are about. From there, whatever is relevant to that conversation is brought into context. There is no automatic mechanism that filters or selects files by the type of task at hand; the index gives visibility over what is available, and reading what is relevant is a deliberate step, not a fixed classification rule. Even so, the practical effect is the same: work can continue without losing context, because the method, the roles, the constraints and the project's history stay accessible from the index, instead of having to be rebuilt from scratch each session.

Memory is alive: it is updated when decisions change, when new constraints are added, or when a learning cycle closes. It is not a frozen record but a store of operational truth that grows and is refined with each session.
