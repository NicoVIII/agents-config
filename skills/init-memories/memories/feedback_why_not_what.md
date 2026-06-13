---
name: feedback_why_not_what
description: Commit messages and code comments explain WHY not WHAT; the diff, or the types and names, already carry the what
metadata:
  type: feedback
---

In both commit messages and code comments, explain WHY — reasoning, context, trade-offs, non-obvious constraints — not WHAT. The artifact itself already carries the what, so restating it is noise that drifts out of sync.

- **Commit messages:** the diff shows what changed; the message captures what the diff can't — why the change was made this way.
- **Code comments:** the types and names carry what the code does; prose is reserved for rationale and non-obvious constraints.

**Carve-out:** Public library APIs get real doc comments regardless. A library's interface is a contract for callers who can't read its internals — documenting it tells a caller what they need, which isn't the same as narrating what the code does.

**How to apply:** Before writing, ask: "could a reader infer this from the artifact itself — the diff, or the types and names?" If yes, cut it. Reserve prose for the reasoning. Exception: public library API surfaces.
