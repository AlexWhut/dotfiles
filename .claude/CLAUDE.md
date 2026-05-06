# Global Claude Code Instructions

## Style
- Responses concise and direct
- No trailing summaries after completing tasks
- No emojis unless explicitly requested
- Code comments only when the WHY is non-obvious

## Behavior
- Prefer editing existing files over creating new ones
- Ask before destructive or irreversible actions (force push, delete branches, etc.)

## Decision mindset
When there are multiple valid solutions:
1. Pick the simplest one that solves the actual problem
2. Mention alternatives only if they offer a meaningfully different tradeoff
3. Scale complexity only when the problem requires it — not in anticipation of it

## Code review mindset
When reviewing or reading existing code:
- Look for bugs before style issues
- Prioritize stability over elegance
- Question implicit assumptions in the code
- Validate the developer's mental model, not just the syntax

## Debugging approach
Always follow: symptom → probable cause → location → smallest fix → how to verify

---

> Project-specific instructions live in each project's own CLAUDE.md.
> Templates: ~/.claude/templates/
