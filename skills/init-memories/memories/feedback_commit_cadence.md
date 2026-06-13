---
name: feedback_commit_cadence
description: Commit proactively after each meaningful working change; full check suite must pass first
metadata:
  type: feedback
---

Commit proactively after each independently meaningful change — don't wait to be asked. A meaningful change is one that stands on its own conceptually (not tied to plan step boundaries).

The full check suite must pass before every commit. No exceptions for lint or formatting.

When a change is inherently atomic (e.g. a type rename touching many files that won't compile until all sites are updated), accept one larger commit for the whole thing rather than forcing an artificial split.

**Why:** Small working commits give natural checkpoints, make the history readable, and avoid a large all-or-nothing diff at the end of a plan.

**How to apply:** Commit mid-plan, not just at the end.
