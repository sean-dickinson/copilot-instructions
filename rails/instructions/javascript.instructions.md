---
applyTo: "app/javascript/**/*"
---

# JavaScript conventions

- Write the least JavaScript necessary.
- Prefer HTML and CSS solutions before JavaScript solutions.
- Prefer one small Stimulus controller over large custom JS modules.
- Keep Stimulus controllers focused on presentation behavior, not business logic.
- Do not move validation, authorization, or workflow rules into JavaScript.
- Do not propose polling or real-time updates unless clearly required.
- Do not add JavaScript dependencies without explicit approval.
- Prefer Turbo based solutions to ActionCable