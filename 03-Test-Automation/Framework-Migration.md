# Framework Migration

## Purpose
Plan or implement migration to another test technology.

## When to use
Use this prompt when assess and plan migration between automation frameworks with controlled validation. Ensure the required inputs are available.

## Inputs required
- `{{CURRENT_FRAMEWORK}}` — **Required:** Existing automation tool, language, test runner, architecture and assets.
- `{{TARGET_FRAMEWORK}}` — **Required:** Requested target tool, language, runner and design constraints.
- `{{MIGRATION_SCOPE}}` — **Required:** Suites, integrations, environments, deadlines and exclusions in scope.

## Prompt
```text
Role: Act as a Senior Test Automation Architect.

Task: Assess and plan migration between automation frameworks with controlled validation.

Inputs:
CURRENT_FRAMEWORK:
{{CURRENT_FRAMEWORK}}
TARGET_FRAMEWORK:
{{TARGET_FRAMEWORK}}
MIGRATION_SCOPE:
{{MIGRATION_SCOPE}}

Rules:
- Inventory existing tests, helpers, reporting, CI and integration dependencies.
- Identify target equivalents, unsupported features and required rewrites.
- Recommend incremental phases with pilot, parallel validation and rollback criteria.
- Distinguish proven compatibility from assumptions; do not promise one-to-one conversion.
- Do not modify or delete existing framework files without explicit authorization.

Deliverables:
- Current-to-target capability mapping
- Reusable assets, rewrite candidates and compatibility gaps
- Phased migration plan with pilot, acceptance gates, risks and rollback
- Open decisions and evidence needed for estimates
```

## Expected output
- Current-to-target capability mapping
- Reusable assets, rewrite candidates and compatibility gaps
- Phased migration plan with pilot, acceptance gates, risks and rollback
- Open decisions and evidence needed for estimates
- Clearly label assumptions, missing evidence, and whether files were created or tests executed.

## Example
**Synthetic input:**
```text
CURRENT_FRAMEWORK: Selenium Java + TestNG with Page Objects; TARGET_FRAMEWORK: Playwright TypeScript; MIGRATION_SCOPE: 20 login and checkout tests, CI integration.
```

**Illustrative output (not executed):**
> Phase 1 inventory 20 tests and helpers; Phase 2 migrate 3 login pilot cases; gate: equivalent assertions and green CI; risk: Java helpers require TypeScript rewrite; rollback: retain Selenium job.

The example is illustrative only; use actual input evidence for real deliverables.

## Limitations
- Results depend on supplied requirements, repository access, tool availability and authorization.
- Generated code or recommendations are not verified until explicitly checked or executed.
- Shared privacy, evidence, authorization and human-review requirements: `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
