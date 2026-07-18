---
name: feedback-memory-discipline
description: Keep memory files concise — every word has token cost and memories load into context on every invocation
metadata:
  type: feedback
---

Memory files load into agent context on every invocation. Every word has token cost. Write and edit them with the same discipline as AGENTS.md: only what can't be inferred from the code or conversation, no prose padding, no restating the obvious, no examples unless they add precision the rule alone doesn't convey. See [[feedback-agents-md-updates]].

**How to apply:** When creating or editing a memory, cut any sentence that doesn't add precision. Prefer one tight sentence over two loose ones.
