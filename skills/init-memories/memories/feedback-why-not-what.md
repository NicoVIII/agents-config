---
name: feedback-why-not-what
description: WHY not WHAT in comments and commits; grouping/orientation labels are allowed and encouraged
metadata:
  type: feedback
---

In both commit messages and code comments, explain WHY — reasoning, context, trade-offs, non-obvious constraints — not WHAT. The artifact itself carries the what.

- **Commit messages:** the diff shows what changed; the message captures why.
- **Code comments:** types and names carry what the code does; prose is for rationale and non-obvious constraints.

**Carve-out — public APIs:** Public library APIs get doc comments. The interface is a contract for callers who can't read the internals.

**Carve-out — type-lossy seams:** Any definition where the type signature cannot express the full contract warrants a brief annotation: anonymous generic parameters (`String`, `Int`) whose role isn't obvious, error semantics not encoded in the type, idempotency assumptions. Applies to port/interface definitions and type aliases for callbacks. The reader cannot resolve ambiguity by reading the implementation.

**Carve-out — grouping/readability:** Short section labels in long functions or case expressions are allowed: `// Fallback path`, `// Phase 2: reconcile`. Orientation markers, not explanations.

**How to apply:** Ask: "could a reader infer this from the types and names?" If yes, cut it. Exceptions: public API surfaces; type-lossy seams; orientation markers.
