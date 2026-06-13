---
name: init-memories
description: Initialize persistent personal memories that aren't derivable from the codebase. Run on a fresh machine (after pulling ~/.claude) or in a new project to restore preferences and feedback.
---

This skill installs my personal, cross-project memories into a project's memory directory. The canonical copies live in this skill's `memories/` directory — that is the single source of truth. The steps below copy them in without duplicating their content anywhere.

## Steps

1. **Locate** the current project's memory directory (create it if it doesn't exist).

2. **Copy missing memories.** For each `*.md` file in this skill's `memories/` directory, if a file of the same name is absent from the project memory directory, copy it in verbatim.

3. **Reconcile existing memories.** If a same-named file already exists but its contents differ from the canonical version in `memories/`, do not silently skip or overwrite it. Show the diff and ask which to keep — a difference is either a stale copy worth updating or a deliberate per-project override worth preserving, and only I can say which.

4. **Rebuild the index.** Ensure `MEMORY.md` exists and contains exactly one entry per installed memory. Generate each entry from that memory's own frontmatter (`name` and `description`) rather than maintaining the list by hand — the frontmatter is the source of truth for the index, so the two cannot drift. Leave any non-memory content already in `MEMORY.md` untouched.

## Why this shape

- Memory content lives in `memories/` as real files, not embedded in this file — one source of truth, nothing to keep in sync by hand.
- The index is derived from frontmatter, not hand-written, for the same reason.
- Reconciliation asks rather than assuming, so canonical updates can propagate without clobbering an intentional local override.
