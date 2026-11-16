# Application Understanding

## Purpose
Understand application modules, users, integrations and critical workflows.

## When to use
Use when the required inputs are available and this activity is relevant to the QE lifecycle.

## Inputs required
- `{{APP_OVERVIEW}}` — **Required:** Provide the application purpose, intended users, major features, workflows, and known integrations.

## Prompt
```text
Act as a Senior Business Systems Analyst supporting a real software delivery team. Base your analysis on the supplied evidence and clearly label assumptions.
Task: Produce a concise application map: purpose, roles, modules, dependencies, critical journeys and open questions.

Inputs:
APP_OVERVIEW:
{{APP_OVERVIEW}}

Rules:
- Identify modules, actors, integrations and critical user journeys.
- Separate documented behavior from inferred behavior.
- Map unanswered questions to stakeholders.
```

## Expected output
- Application capability map.
- Actor-to-workflow matrix.
- Integrations/dependencies.
- Assumptions and clarification questions.

## Example
**Synthetic input:**
```text
APP_OVERVIEW: Demo school portal with staff login, attendance and gradebook.
```
**Illustrative response outline (synthetic, not executed):**
- Application capability map.
- Actor-to-workflow matrix.
- Integrations/dependencies.
- Assumptions and clarification questions.

Populate each field using the sample input; mark unavailable evidence as `Not provided` rather than inventing values.

## Limitations
- A high-level overview cannot verify implemented behavior.
- Undocumented integrations may be missed.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.1.0
- Status: Draft for team review
