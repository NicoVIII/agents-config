# AI Agent Config

Shared skills and configuration for AI coding agents.

## Setup

### Claude Code

```sh
git clone <repo-url> ~/.claude
```

If `~/.claude` already exists:

```sh
cd ~/.claude
git init
git remote add origin <repo-url>
git pull origin main
```

### GitHub Copilot

```sh
git clone <repo-url> ~/.copilot
```

Adjust the target path to wherever your Copilot installation reads skills from.

## After cloning

- Add your `settings.json` manually — it is gitignored and not tracked.
- Use `settings.local.json` for secrets and machine-specific overrides (also gitignored).

## Contents

- `skills/` — slash-command skills usable in Claude Code and compatible agents
