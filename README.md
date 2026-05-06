# dotfiles

Personal dotfiles, including Claude Code global configuration.

## Setup on a new machine

```bash
git clone <this-repo> ~/dotfiles
ln -sf ~/dotfiles/.claude ~/.claude
```

## Structure

```
.claude/
├── settings.json          # Global Claude Code settings
├── CLAUDE.md              # Global behavior (style, tone) — stack-agnostic
├── commands/              # Custom slash commands (*.md) → available as /<name>
├── skills/                # Reusable Claude skills (auto-loaded per session)
│   ├── vault-select.md         # Detects active Obsidian vault and routes to the right skill
│   ├── vault-update.md         # Generic vault update (fallback for any project)
│   └── vault-update-verify.md  # Vault update for the Verify KYC/AML platform
└── templates/             # Per-stack CLAUDE.md templates
    ├── laravel-vue.md
    └── flutter-firebase.md
```

## Starting a new project

Copy the relevant template into the project root as `CLAUDE.md`:

```bash
# Laravel + Vue
cp ~/dotfiles/.claude/templates/laravel-vue.md ~/projects/my-app/CLAUDE.md

# Flutter + Firebase
cp ~/dotfiles/.claude/templates/flutter-firebase.md ~/projects/my-app/CLAUDE.md
```

Commit it with the project. Claude Code loads it automatically when working in that directory.

## Adding a slash command

Create `.claude/commands/<name>.md`. Available as `/<name>` in any Claude Code session.

## Adding a skill

Create `.claude/skills/<name>.md`. Skills are reusable instructions Claude follows for recurring workflows.

To add a project-specific vault skill, create `.claude/skills/vault-update-<project>.md` and add a routing row in `vault-select.md`.
