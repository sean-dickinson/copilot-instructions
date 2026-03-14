---
applyTo: "{spec,test}/**/*.rb"
---

# Testing conventions

## Layer guidance
- Unit/model tests: validations, domain rules, query objects. Fast and focused.
- Request/integration tests: controller behavior, auth outcomes, redirects, param handling, multi-step flows. Default choice for most feature work.
- System tests: only for critical user journeys, Turbo/JS flows that must be verified in-browser, or regressions involving form interaction or navigation.

## What to avoid
- Do not add system tests for every CRUD path.
- Do not test private methods directly.
- Do not mock Active Record or Rails internals unnecessarily.
- Avoid brittle assertions tied to incidental markup.
- Avoid excessive fixture/setup complexity for simple cases.

## Preferred balance for a typical feature
1. Unit tests for new domain logic.
2. Request tests for endpoint behavior.
3. A system test only if the browser interaction itself could regress.

## Test Structure
- Tests should be explicit and self explanatory. Prefer duplication to ensure each test case is clearly readable in isolation
- Tests should follow a strict AAA pattern with each step separated by whitespace
- Test should only create the data that is strictly necessary to test the behaviour
- Prefer build and build_stubbed if data does not need to be persisted