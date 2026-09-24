# Template: enforcement hook

> **What it does.** A deterministic script that runs on its own on an event and **blocks** what
> violates an objective rule. It is the only piece that does not depend on the model cooperating.
>
> **When to choose it.** When the symptom is *"there is an objective technical rule that must
> NEVER be violated"*. If the rule is subjective or admits judgment, that is a [skill](SKILL.md),
> not a hook. See [`docs/06-industrialization.md`](../docs/06-industrialization.md).
>
> **How to verify it really blocks.** Attempt the violation on purpose. If the action is not
> stopped, the piece is not installed: it is decorating.

## The convention

The hook receives the event on **stdin** and responds with its **exit code**:

| Exit code | Effect |
|---|---|
| `0` | Allows the action |
| `2` | **Blocks** the action |

Two possible moments: **pre-event** (blocks before it happens) and **post-event** (validates
after). For real enforcement, use pre-event.

---

## JavaScript skeleton

```javascript
#!/usr/bin/env node
// Enforcement hook. Exit 2 blocks, exit 0 allows.

let input = "";
process.stdin.on("data", (chunk) => (input += chunk));
process.stdin.on("end", () => {
  let event;
  try {
    // Tolerate the BOM: on Windows it is a real source of silent failures.
    event = JSON.parse(input.replace(/^﻿/, ""));
  } catch (e) {
    process.exit(0); // When in doubt, do not block: a broken hook must not stop the work.
  }

  const path = event?.tool_input?.file_path ?? "";
  const content = event?.tool_input?.content ?? "";

  // Narrow the scope BEFORE evaluating. A hook that applies everywhere
  // produces false positives and ends up disabled.
  if (!/your-path-pattern/.test(path)) process.exit(0);

  const violations = [];
  if (/forbidden-pattern/.test(content)) {
    violations.push("Explain WHICH rule was violated and HOW to fix it.");
  }

  if (violations.length) {
    console.error("BLOCKED:\n" + violations.join("\n"));
    process.exit(2);
  }
  process.exit(0);
});
```

## PowerShell skeleton

```powershell
# Enforcement hook. Exit 2 blocks, exit 0 allows.
$raw = [Console]::In.ReadToEnd()
try { $event = $raw -replace "^﻿", "" | ConvertFrom-Json } catch { exit 0 }

$path = $event.tool_input.file_path
if (-not $path -or $path -notmatch "your-path-pattern") { exit 0 }

if ($event.tool_input.content -match "forbidden-pattern") {
    [Console]::Error.WriteLine("BLOCKED: explain which rule was violated and how to fix it.")
    exit 2
}
exit 0
```

---

## Registering the hook

It is registered in the environment's configuration, associating a **matcher** (which tools fire
it) with a command. This block replicates the verified form of a real installation:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "node \"/absolute/path/to/your-hook.js\"",
            "statusMessage": "Checking invariants..."
          }
        ]
      }
    ]
  }
}
```

The available events include `PreToolUse`, `PostToolUse`, `SessionStart` and `SessionEnd`. A
change to this configuration usually takes effect at the start of a new session.

---

## Three mistakes that have already cost dearly

**The false positive from matching inside a comment.** A forbidden pattern that appears in a
comment or in a documentation example is not a violation. A hook that stops legitimate work ends
up disabled, and then it protects nothing.

**Putting a subjective rule in a hook.** If judgment is needed to decide whether something
violates the rule, it is not a hook: it is a skill. The hook only works for the binary,
deterministic and verifiable.

**The hook failing open silently.** If the hook breaks and exits with `0`, the action goes
through and nobody notices the protection stopped existing. A broken hook had better be noisy.
