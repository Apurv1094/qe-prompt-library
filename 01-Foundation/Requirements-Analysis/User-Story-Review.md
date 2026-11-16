# User Story Review

## Purpose
Check whether a user story is testable and ready.

## When to use
Use when the required inputs are available and this activity is relevant to the QE lifecycle.

## Inputs required
- `{{STORY_DESCRIPTION}}` — **Required:** Provide the complete user story, including the user goal, business context, and expected capability.
- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Provide the numbered acceptance criteria describing the expected, testable behavior.

## Prompt
```text
Act as a Senior Quality Analyst supporting a real software delivery team. Base your analysis on the supplied evidence and clearly label assumptions.
Task: Review clarity, testability, business rules, dependencies and readiness; suggest precise edits.

Inputs:
STORY_DESCRIPTION:
{{STORY_DESCRIPTION}}
ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}

Rules:
- Review story INVEST characteristics and acceptance-criteria clarity.
- Identify testable scenarios, edge cases and dependencies without inventing behavior.
```

## Expected output
- Story review checklist.
- Acceptance-criteria findings.
- Suggested revisions.
- Readiness recommendation.

## Example
**Synthetic input:**
```text
STORY_DESCRIPTION: As a teacher I want to export a class report. ACCEPTANCE_CRITERIA: Export CSV.
```
**Illustrative response outline (synthetic, not executed):**
- Story review checklist.
- Acceptance-criteria findings.
- Suggested revisions.
- Readiness recommendation.

Populate each field using the sample input; mark unavailable evidence as `Not provided` rather than inventing values.

## Limitations
- Story readiness is advisory.
- Acceptance criteria require product-owner approval.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.1.0
- Status: Draft for team review
