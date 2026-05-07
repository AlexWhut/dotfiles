---
name: ticket-jira
description: >
  Generates a Jira comment in the standard bug-fixing template format, ready to paste
  into a Jira ticket. Use this skill whenever the user types /ticket-jira, with or
  without a ticket ID or Jira reference. Reads the relevant internal ticket file from
  /Users/alex/Desktop/Code/Boveda/Tickets and outputs the English-language Jira comment
  block. Always invoke this skill on /ticket-jira commands — do not try to handle them inline.
---

# Skill: ticket-jira

## Purpose

Read an internal ticket file and produce the standard Jira bug comment template, filled with the ticket's data, ready to copy-paste into Jira.

The Jira template is always in **English**, regardless of the ticket file language.

## Step-by-step

### 1. Locate the ticket file

**If the user provided a reference:**
- If it looks like `XXXX` (4-digit number), find the file starting with that number in `/Users/alex/Desktop/Code/Boveda/Tickets/`.
- If it looks like `BA-NNNNN`, find the file whose name contains that Jira ID.

**If no reference was provided:**
- Use the most recently modified `.md` file in `/Users/alex/Desktop/Code/Boveda/Tickets/` (excluding `_Template.md`):
  ```bash
  ls -t /Users/alex/Desktop/Code/Boveda/Tickets/*.md | grep -v _Template | head -1
  ```

Read the file.

### 2. Extract the relevant fields

From the ticket file, pull:

| Jira field | Source in ticket |
|---|---|
| BRANCHES | `branches` frontmatter or Metadata table |
| WHAT WAS THE PROBLEM | `## Causa raíz` section |
| SOLUTION PROVIDED | `## Solución implementada` section |
| RISK JUSTIFICATION | `## Justificación de riesgo` section |
| CONFIGURATION | Any config changes mentioned; if none, use "No configuration changes required." |
| AFFECTED MODULES | `imps` frontmatter / `## Metadata` IMPs afectados |
| EVIDENCE | Any evidence listed; if none, use "Pending — screenshots/recordings to be attached." |

### 3. Output the Jira comment

Output the filled template as a single fenced code block (plain text, no syntax highlighting) so the user can copy it cleanly:

````
```
BRANCHES:
release/3.2, develop

WHAT WAS THE PROBLEM?:
[clear, concise explanation of the root cause]

SOLUTION PROVIDED:
[what was implemented to fix it]

RISK JUSTIFICATION:
[risk level and reasoning]

CONFIGURATION
No configuration changes required.

AFFECTED MODULES
IMP6

EVIDENCE:
Pending — screenshots/recordings to be attached.
```
````

Keep each section tight — 2-5 lines max. If the ticket has detailed technical prose, summarize for the Jira comment; the full detail lives in the internal ticket.

Do not add anything after the code block.
