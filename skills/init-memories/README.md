# init-memories

Installs a set of persistent, personal memories into a project's Claude Code memory directory — preferences and feedback that aren't derivable from the codebase, so Claude restores them on a fresh machine or in a new project instead of relearning them each time.

## The pattern this implements

Preferences you want Claude to follow tend to fall into three layers, and this skill owns exactly one of them:

- **Adviser / deliberation context** — your values and the open trade-offs you want discussed per-project. Lives wherever you brief the advising agent; not here.
- **Project instructions** (e.g. `AGENTS.md`) — facts about a specific codebase that anyone touching it must follow. Lives in each project repo.
- **Personal memories** — dispositions about *you* that hold across every project. **This is the layer this skill installs.**

The line that sorts a preference is *personal vs. project*: does it describe you (→ a personal memory), or the codebase (→ project instructions)? And a trade-off you haven't settled belongs in neither — it stays in the deliberation layer so it can be argued per-project rather than frozen into a rule.

## How it works

The canonical memories live as real files in [`memories/`](memories/) — one source of truth, not embedded in `SKILL.md`. On run, the skill copies in any that are missing, reconciles ones that differ by asking rather than overwriting, and rebuilds an index from each file's frontmatter. See [`SKILL.md`](SKILL.md) for the procedure.

## Making it yours

The `memories/` files here are examples — replace them with your own. Each is a small Markdown file with `name`/`description` frontmatter (the `description` doubles as the generated index line) and a short body stating the preference, the reason for it, and how to apply it.
