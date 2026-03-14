---
applyTo: "app/views/**/*"
---

# View conventions

- Prefer ERB and server-rendered responses.
- Use standard Rails helpers and partials for reusable UI.
- Use Turbo for navigation/form enhancements when it keeps code simpler.
- Use Stimulus only for small, isolated UI behavior that cannot be handled cleanly server-side.
- Do not build SPA-style flows.
- Do not introduce frontend frameworks.
- Do not add JavaScript dependencies unless explicitly approved.
- Keep client-side state to a minimum.
- If a feature works well with a normal request/response cycle, use that.