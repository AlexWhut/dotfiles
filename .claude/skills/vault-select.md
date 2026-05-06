---
name: vault-select
description: >
  Orchestrator skill that detects available Obsidian vaults, identifies the
  active project context, and routes to the appropriate project-specific vault
  skill. Trigger this FIRST whenever the user wants to update the vault, document
  a finding, or says things like "update the vault", "anota esto", "actualiza la
  bóveda", "documenta esto", "save this for later", "no quiero perder esto",
  before any vault-update skill runs. This skill decides WHICH vault-update skill
  to invoke based on the vault and project detected.
---

# Vault Select — Orchestrator

Detects available Obsidian vaults and routes to the correct project-specific
vault-update skill.

## Step 1 — Read Obsidian vault registry

Read the Obsidian state file for this OS:

| OS      | Path                                                        |
|---------|-------------------------------------------------------------|
| macOS   | `~/Library/Application Support/obsidian/obsidian.json`      |
| Linux   | `~/.config/obsidian/obsidian.json`                          |
| Windows | `%APPDATA%\obsidian\obsidian.json`                          |

Parse `vaults` — collect `path`, `ts`, and `open` for each entry.

## Step 2 — Determine active vault

- If exactly one vault has `"open": true` → use it directly, no need to ask.
- If multiple have `"open": true` or none does → show the list ordered by `ts`
  descending and ask: "Which vault should I update?"

## Step 3 — Identify the project

From the vault path and name, determine which project this vault belongs to.

| Vault contains / is named | Route to skill         |
|---------------------------|------------------------|
| `Verify`, `verify`, `IMP` | `vault-update-verify`  |
| anything else             | `vault-update`         |

If unsure, show the vault root and ask the user which project it belongs to.

## Step 4 — Hand off

Invoke the appropriate skill with full context:
- The resolved vault root path
- Any finding the user already described in their message

Do not re-ask for information the user already provided.
