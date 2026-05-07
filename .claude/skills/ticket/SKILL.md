---
name: ticket
description: >
  Creates an internal bug ticket file in /Users/alex/Desktop/Code/Boveda/Tickets.
  Use this skill whenever the user types /ticket followed by bug context — Jira ID,
  title, severity, branches, affected IMPs, root cause, solution, or any partial
  description of a bug. Even if the context is incomplete, infer what you can and
  fill the rest with placeholders. Always invoke this skill on /ticket commands —
  do not try to handle them inline.
---

# Skill: ticket

## Purpose

Create a structured internal bug ticket `.md` file based on context the user provides.
The goal is to build a searchable, consistent registry of bug investigations in `/Users/alex/Desktop/Code/Boveda/Tickets`.

## Step-by-step

### 1. Determine the next ticket ID

List all `.md` files in `/Users/alex/Desktop/Code/Boveda/Tickets`:

```bash
ls /Users/alex/Desktop/Code/Boveda/Tickets/*.md
```

Extract the leading 4-digit number from each filename (e.g. `0004` from `0004-BA-25855-...md`).
Find the highest, add 1, zero-pad to 4 digits. If no files exist, start at `0001`.

Skip `_Template.md` and any file that doesn't start with a digit.

### 2. Parse the user's context

Extract as many fields as possible from what the user provided:

| Field | Where to look |
|---|---|
| `jira` | Anything matching `BA-NNNNN` |
| `title` | Short description of the bug |
| `severity` | Critical / High / Medium / Low |
| `branches` | Branch names mentioned (e.g. `release/3.2`, `develop`) |
| `imps` | IMP identifiers (e.g. `IMP6`) |
| `root_cause` | Technical explanation of why the bug happens |
| `files` | File paths and methods involved |
| `solution` | What was or will be done to fix it |
| `risk` | Risk level or justification |

For any field not provided, use a clear placeholder like `"PENDING"` or the bracket placeholders from the template — don't omit sections.

### 3. Name the file

Format: `{XXXX}-{jira-id}.md`

Examples:
- `0007-BA-29001.md`
- `0007-PENDING.md` (if no Jira ID was given)

### 4. Write the file

Use **exactly** this template, filled with the parsed data:

```markdown
---
ticket_id: "XXXX"
jira: "BA-XXXXX"
title: "Título corto del bug"
status: "Open"
severity: "High"
branches: ["release/3.2", "develop"]
imps: ["IMP6"]
date_opened: "YYYY-MM-DD"
date_closed: ""
---

# [XXXX] BA-XXXXX — Título corto

## Metadata

| Campo | Valor |
|---|---|
| **Jira** | BA-XXXXX |
| **Status** | Open |
| **Severity** | High |
| **Branches** | `release/3.2` → `develop` |
| **IMPs afectados** | IMP6 |
| **Fecha apertura** | YYYY-MM-DD |
| **Fecha cierre** | — |

---

## Descripción del bug

> Resumen en 1-2 líneas de qué falla y en qué condición.

---

## Causa raíz

> Cadena completa de causa → efecto. Ser específico con clases, métodos y líneas.

```
1. [Causa inicial]
2. [Efecto A] porque [razón técnica]
3. [Efecto B] porque [razón técnica]
4. [Síntoma visible para el usuario]
```

---

## Archivos involucrados

| Archivo | Método / Línea | Rol en el bug |
|---|---|---|
| `app/Models/...` | `método()` L123 | descripción |

---

## Solución implementada

### Fix 1 — `archivo/ruta.php` *(committed: `abc1234`)*

**Qué hace:** descripción breve.

```php
// código relevante
```

**Cubre:** casos que resuelve.  
**No cubre:** casos que NO resuelve.

---

## Resultado de QA / Testing

| Escenario | Credencial | Resultado |
|---|---|---|
| Escenario 1 | — | ✅ / ❌ |

---

## Justificación de riesgo

**Severidad del bug:** ...  
**Riesgo de la solución:** ...  
**Razonamiento:** ...

---

## Pendientes / Decisiones

- [ ] Pendiente 1

---

## Notas técnicas

> Cualquier hallazgo relevante que no encaje en lo anterior.
```

Use today's date (from system context or `date +%Y-%m-%d`) for `date_opened`.

### 5. Confirm to the user

After writing the file, tell the user:
- The filename created (as a clickable link if possible)
- The ticket ID assigned
- Nothing else — no summaries, no trailing notes
