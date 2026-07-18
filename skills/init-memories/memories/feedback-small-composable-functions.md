---
name: feedback-small-composable-functions
description: "Default to small single-purpose functions as the unit of decomposition; a named function often replaces a 'what' comment"
metadata:
  type: feedback
---

Prefer small, composable functions that each do one thing. A named function is the default unit of decomposition — a good name makes intent legible and keeps each function independently understandable.

A common trigger: a `// this block does X` comment. Extracting the block into a named function usually beats the comment. See [[feedback-why-not-what]].

**When NOT to extract:** only when extraction *reduces* complexity. Skip when the helper needs many threaded parameters (call site becomes as noisy as the inlined code) or when a one-shot block adds only indirection. Judge by whether the extracted name + signature reads more clearly than the inline block, not by line count.

**How to apply:** when a function does several things in sequence, look for cohesive sub-steps to lift out — but only where the helper has a tight, low-arity signature.
