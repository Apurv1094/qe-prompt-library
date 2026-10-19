#### Plan or Execute a Framework Migration

```text
Review the existing automation framework and assess the migration request.

Migration goal:
{{MIGRATION_GOAL}}

Inspect the current tool, language, framework architecture, dependencies,
test coverage, page objects, test-data handling, reporting, and CI/CD.

If the target tool or language has already been decided, use that target.
Otherwise, recommend suitable options with their trade-offs and ask for a
decision only if it is necessary to proceed.

Provide a phased migration plan covering reusable components, required
changes, compatibility, risks, coexistence of old and new implementations,
and estimated effort.

If implementation is requested, migrate one representative example first,
validate it, and then recommend the next step.

Do not assume that every component must be rewritten. Identify what can
be reused and explain any limitations.