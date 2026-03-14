---
applyTo: "app/models/**/*.rb"
---

# Model conventions

- Models may contain domain behavior, validations, scopes, and persistence logic.
- Avoid fat models full of unrelated procedural workflows.
- Prefer well-named instance and class methods over callback-heavy designs.
- Use callbacks sparingly: only when straightforward and predictable.
- Avoid callbacks that trigger external side effects or hide workflow behavior.
- Prefer explicit, boring code over metaprogramming.

## Unit tests (spec/models or test/models)
- Test validations, domain rules, scopes, and small business logic methods.
- Tests should be fast and focused.
- Do not test private methods directly.