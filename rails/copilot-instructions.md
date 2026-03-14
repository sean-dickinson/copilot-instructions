# Rails – Core Conventions

## Philosophy
- Prefer simple, conventional Rails over clever abstractions.
- Favor server-rendered HTML and standard Rails patterns first.
- Keep JavaScript to a minimum.
- Do not introduce Action Cable, WebSockets, or real-time features unless explicitly requested.
- Optimize for maintainability, readability, and fast onboarding.

## Responsibility split
- Controllers: handle HTTP, load records, authorize, delegate business logic.
- Models: behavior intrinsic to a record, validations, scopes.
- Service objects: Prefer using the ActiveRecord::AssociatedObject gem
- Query objects: only when a query is complex and reused.

## Security
- Follow Rails secure defaults.
- Never bypass authentication, authorization, CSRF protection, or strong parameters.
- Do not expose sensitive data in logs, views, or serialized responses.
- Prefer allowlists over denylists.

## Dependencies
- Prefer the standard library and Rails built-ins before adding gems.
- When proposing a dependency, explain why built-ins are insufficient, the maintenance cost, and the scope of use.

## Testing strategy
- Every meaningful behavior change must include or update tests.
- Test at the lowest level that gives confidence: unit → request → system.
- Prefer fewer, high-value tests over many brittle ones.

## Code style
- Small methods with clear names. Guard clauses over deep nesting.
- Explicit names over abbreviations. No drive-by refactors.
- Add comments only to explain intent, tradeoffs, or non-obvious constraints.

## AI change guidelines
- Make the smallest change that fully solves the problem.
- Preserve existing architecture unless refactoring is the task.
- When uncertain, prefer the more conventional Rails solution with simpler tests.