---
name: feedback-agents-md-updates
description: After structural decisions, check whether AGENTS.md needs updating; keep it minimal
metadata:
  type: feedback
---

After any refactoring or structural decision, ask: would an agent need to know this to place new code correctly? If yes, update or create the relevant AGENTS.md (at the appropriate directory level, not always the root).

AGENTS.md files are loaded into every agent context — every word has token cost. Write them to be minimal and precise: only include what an agent cannot infer from the code itself. No prose padding, no restating the obvious, no examples that don't add information the structure alone doesn't convey.

**Why:** Structural conventions like mirroring rules, naming patterns, or layer boundaries are non-obvious. Without documenting them, agents will either infer incorrectly or ask repeatedly. But bloated AGENTS.md files waste tokens on every invocation and dilute the signal.

**How to apply:** Make this a standard step at the end of any plan that introduces or changes structural conventions.
