# Project: Flutter + Firebase (greenfield)

## Context
New project under active construction. Focus is on implementing features correctly with solid foundations, not premature optimization.

## Stack
- Flutter (Dart) + Firebase (Firestore, Auth, Storage, Cloud Functions)
- State management: [specify: Riverpod / BLoC / Provider]
- Architecture: [specify: feature-first / layer-first / etc.]

## How to respond
- Go straight to the solution
- If there are multiple approaches, state which you recommend and why in one line
- Directly usable code, no unnecessary scaffolding
- If context is missing to implement correctly, ask only for what you need

## When implementing
- Follow the state management pattern and architecture already in use
- Stay consistent with existing widgets and conventions
- Prefer clarity over brevity — the project is growing and others will read it
- Do not add abstraction layers that aren't needed yet (real YAGNI)
- Prefer composition over inheritance in widgets
- Keep UI / logic / data access separated without over-engineering

## Flutter — patterns to respect
- Use the state management layer chosen for the project — don't mix patterns
- Extract widgets when a build() method grows too large
- Design composable widgets: one widget, one responsibility
- Warn if something may cause unnecessary rebuilds or visible jank
- Always flag when a stream or listener needs to be cancelled in dispose

## Firebase — when implementing
- Design document structure around real queries, not pure normalization
- Flag if a query will need a composite index before implementing it
- Use batch or transaction for multiple writes when appropriate
- Flag if an operation may have eventual consistency issues

## When reviewing code — look for
- Uncancelled streams or listeners (memory leaks)
- Unnecessary UI rebuilds
- Poorly structured queries or missing indexes
- Incorrect null safety
- Shared state without proper synchronization
- Silent failures in Futures without error handling
- Do not suggest cosmetic changes that add no technical value

## Out of scope for now
- Firebase cost or quota analysis
- Large-scale production warnings
- Refactors of code that already works
