# Claude Code Config

Shared skills and configuration for Claude Code, versioned as `~/.claude`.

## Setup

```sh
git clone <repo-url> ~/.claude
```

If `~/.claude` already exists:

```sh
cd ~/.claude
git init
git remote add origin <repo-url>
git pull origin main
git branch --set-upstream-to=origin/main main
```

## After cloning

- Add your `settings.json` manually — it is gitignored and not tracked.
- Use `settings.local.json` for secrets and machine-specific overrides (also gitignored).

## Contents

- `CLAUDE.md` — global personal preferences, loaded into every Claude Code session; applies automatically after cloning
- `AGENTS.md` — guardrails for working on this repo itself
- `skills/` — slash-command skills for Claude Code, see below

## Skills

| Skill | Summary | Suggested model | Maturity |
| --- | --- | --- | --- |
| [`grill-me`](skills/grill-me/SKILL.md) | Interviews you about a plan or design one question at a time, resolving each decision branch until you reach shared understanding. | Opus | 🟢 Usable |
| [`prioritize`](skills/prioritize/SKILL.md) | Scans your GitHub repos for open PRs, issues, CI failures, and security alerts, then ranks what to tackle first. | Sonnet | 🧪 Experimental |
| [`skill-retro`](skills/skill-retro/SKILL.md) | Reviews a skill's run in the current session against its SKILL.md and turns observed friction into concrete skill edits. | Opus | 🧪 Experimental |

Maturity: 🚧 WIP → 🧪 Experimental → 🟢 Usable → 🛡️ Battle-tested

Skills below 🛡️ end with a feedback footer that asks the agent to surface friction during runs; `/skill-retro` turns that feedback into skill edits.
