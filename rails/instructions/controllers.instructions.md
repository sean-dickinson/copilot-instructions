---
applyTo: "app/controllers/**/*.rb"
---

# Controller conventions

- One responsibility: translate request to response.
- Do not place business workflows directly in actions.
- Keep actions concise and readable.
- Always use strong parameters.
- Handle unhappy paths explicitly with clear flash/error messages.
- Prefer redirects/rendering over complicated branching.
- Avoid non-RESTful member/collection actions unless clearly justified.

## Request/integration tests
- Prefer request tests for controller behavior: auth outcomes, redirects, responses, param handling.
- For most feature work, request tests are the default — not system tests.