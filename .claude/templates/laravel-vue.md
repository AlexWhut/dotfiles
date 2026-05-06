# Project: Laravel + Vue

## Stack
- Backend Laravel (PHP) + Vue 3 frontend
- APIs, business logic, validation, controllers, services, jobs, database queries
- Code may reach production — prioritize security and stability

## How to respond
- Start with the detected problem
- Then the probable cause
- Then the solution — if there are multiple, order them from least to most impact
- Clear and direct technical language
- If you're unsure about something, say so explicitly

## Analysis rules
- Do not invent endpoints, tables, models, relationships, middlewares, or business rules
- Do not assume variable, column, or method names that don't appear in the code
- If context is missing, ask for exactly the file, method, error, or snippet needed
- Base responses only on the code shown and the information provided

## Priority when modifying code
- Prefer minimal changes
- Avoid large refactors when the goal is fixing a specific bug
- Preserve the existing style and structure unless there's a clear error
- Do not change public names, contracts, routes, or API responses without flagging it

## Production risks
If a change may affect production, say so before proposing it. Flag potential impact on:
- API compatibility (breaking changes)
- Heavy or unindexed queries
- Queues/jobs (concurrency, duplication, retries)
- Migrations (reversibility, table locks)
- Cache (invalidation, stale data)
- Authentication / authorization (policies, gates)

## Laravel
- Prioritize idiomatic framework solutions
- Respect layer separation: Request → Controller → Service → Repository → Model
- Use Resources for consistent API responses
- Use Jobs/Queues for heavy tasks; Events/Listeners to decouple logic
- Avoid business logic in controllers if an appropriate layer already exists
- Use Middleware only for cross-cutting concerns (auth, logging, throttling)

## Database
Detect and warn about:
- N+1 queries — always suggest eager loading when applicable
- Full scans without an index
- Expensive joins on large tables
- Migrations that lock the table in production
- Concurrency issues or duplicate writes

## Vue 3
- Respect the state management pattern already in use (Pinia, Composables, etc.)
- Prefer Composition API
- Extract reusable logic into composables
- Warn if a component mixes too many responsibilities

## Code
- Directly usable, no unnecessary scaffolding
- No complexity the problem doesn't justify
- Clarity over brevity

## When reviewing code — look for
- Real bugs and edge cases
- Incorrect null handling
- Missing validation on external inputs
- Authorization errors (missing policy/gate)
- Performance issues (DB, cache, memory)
- Silent failures (swallowed exceptions, responses without error handling)
- Do not suggest cosmetic changes that add no technical value
