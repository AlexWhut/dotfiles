---
name: vault-update-verify
description: >
  Update Obsidian vault notes for the Verify KYC/AML platform after discovering
  something about IMP4, IMP6, IMP7, Docker infrastructure, or the tech stack.
  Use after vault-select routes here, or directly when the user is clearly in a
  Verify/IMP session and says "update the vault", "anota esto en verify",
  "documenta este hallazgo del IMP", or similar.
---

# Vault Update — Verify Platform

Updates notes in the Verify vault. Called after `vault-select` resolves the
vault path, or directly when context makes it unambiguous.

## Vault structure

```
{vault_root}/
├── Verify/
│   ├── Overview.md       ← product overview, active IMPs list
│   ├── IMP4.md           ← Laravel 9 + Vue2/Blade, branch testimp4
│   ├── IMP6.md           ← Vue3 + Inertia, branch release/3.2
│   └── IMP7-develop.md   ← Laravel 12 / PHP 8.4 + Vue3, branch develop
├── Infraestructura/
│   └── Docker.md         ← Docker + Traefik local setup
└── Tech/
    └── Stack.md          ← full technology stack reference
```

`{vault_root}` comes from `vault-select`. If called directly, detect it using
the Obsidian state file (see `vault-select` for OS paths).

## Which note to update

| Finding is about…                          | Note to update              |
|--------------------------------------------|-----------------------------|
| IMP4 specifically                          | `Verify/IMP4.md`            |
| IMP6 specifically                          | `Verify/IMP6.md`            |
| IMP7 / develop specifically                | `Verify/IMP7-develop.md`    |
| Docker, Traefik, containers                | `Infraestructura/Docker.md` |
| Cross-IMP patterns, conventions            | `Tech/Stack.md`             |
| New IMP version, product-level change      | `Verify/Overview.md`        |

If unsure, ask the user. If it touches multiple notes, update all of them.

## Process

1. **Read the target note** in full before writing anything — check what's
   already there to avoid duplication and match the existing style.

2. **Clarify if needed** — ask focused questions only if the user's description
   is too vague to write a useful note. Get: what was discovered, why it
   matters, whether it's IMP-specific or shared.

3. **Propose the change** — show exact text and insertion point. Confirm before
   writing: "Does this capture it, or anything to adjust?"

4. **Write** — use Edit for surgical additions. Match heading hierarchy and tone
   of the existing note.

## What's worth documenting

- Non-obvious architecture decisions and why they were made
- Client-specific configurations (per-tenant customizations)
- Integration quirks (IdMatrix, WorldCheck, SFTP flows, etc.)
- Root cause of important bugs
- Queue names and their purpose beyond the obvious
- Unwritten conventions the team follows
- Branch/environment-specific gotchas

## What's NOT worth documenting

- Code details readable from the source
- Commit history (use `git log`)
- Anything already in a README in the repo
