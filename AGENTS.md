# Working in this repo

This is the live `~/.claude` config — edits to skills take effect in running Claude Code sessions immediately.

- `.gitignore` is an allowlist by design: secrets and runtime state live in this directory, so everything is ignored by default. Never loosen the catch-all; tracking a new file means adding an explicit `!/...` entry.
- `CLAUDE.md` here is global user memory, loaded into every session in every project — only universal personal preferences belong in it, and every word has token cost everywhere. Repo-scoped guardrails go in this file instead.
- `skills/*/SKILL.md` frontmatter must start at byte 0 (nothing above the first `---`, or it silently fails to parse). The `description` field is the model's only trigger signal — keep it rich in trigger phrases.
- Skills below 🛡️ Battle-tested in the README maturity table end with a one-line feedback footer asking the executing agent to surface friction. Add it (identical wording, copy from an existing skill) to every new skill; remove it only when a skill graduates to battle-tested. `/skill-retro` turns the surfaced friction into skill edits.
