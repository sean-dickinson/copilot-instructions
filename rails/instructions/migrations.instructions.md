---
applyTo: "db/migrate/**/*.rb"
---

# Migration conventions

- Migrations must be reversible and easy to understand.
- Avoid mixing schema changes with data migrations unless necessary.
- Be explicit about nullability, defaults, indexes, and foreign keys.
- Add indexes for all foreign keys and frequently queried columns.
- Do not perform drive-by schema changes unrelated to the task.
- Use database constraints for important invariants in addition to model validations.