---
name: feedback-top-to-bottom-ordering
description: "Files must be ordered top-to-bottom F#-style — every definition may only reference things defined above it"
metadata:
  type: feedback
---

Every definition may only reference things defined above it in the same file. Mirrors F# source ordering. Exceptions only when circular dependencies make it impossible.

**Why:** Reads naturally, avoids forward-reference surprises.

**How to apply:** Helpers before callers, types before functions that use them. Entry-point goes last.
