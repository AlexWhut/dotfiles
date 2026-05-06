---
name: vault-update
description: >
  Generic fallback skill to update notes in any Obsidian vault for projects
  that don't have a dedicated vault-update skill. Called by vault-select when
  no project-specific skill matches. Can also trigger directly for personal
  projects, side projects, or any non-Verify vault context.
---

# Vault Update — Generic

Updates notes in any Obsidian vault. Typically called after `vault-select`
resolves the vault path and project. The vault root is passed in from there.

## If called directly (no vault-select)

Read the Obsidian state file for this OS:

| OS      | Path                                                        |
|---------|-------------------------------------------------------------|
| macOS   | `~/Library/Application Support/obsidian/obsidian.json`      |
| Linux   | `~/.config/obsidian/obsidian.json`                          |
| Windows | `%APPDATA%\obsidian\obsidian.json`                          |

Find `"open": true` in `vaults` → that `path` is the vault root.

## Step 1 — Discover the vault structure

Run `find {vault_root} -name "*.md" -maxdepth 3` (or `dir` on Windows) to map
available notes. Show a condensed list if there are many files.

## Step 2 — Identify the right note

Based on the user's finding and the vault map, propose which note to update.
If ambiguous, ask. If no good note exists, offer to create one.

## Step 3 — Read, propose, confirm, write

1. Read the target note in full.
2. Show exactly what you'll add and where.
3. Confirm with the user before writing.
4. Apply with Edit — surgical additions, matching existing style.

## What's worth documenting

- Non-obvious decisions and why they were made
- Setup steps not captured anywhere else
- Integrations and their quirks
- Patterns and conventions the project follows

## What's NOT worth documenting

- Code details readable from the source
- Anything already in a README in the repo
