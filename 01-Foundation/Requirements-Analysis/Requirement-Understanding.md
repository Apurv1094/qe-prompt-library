# Requirement Understanding

## Purpose
Explain a story and acceptance criteria in plain language.

## When to use
Use when the required inputs are available and this activity is relevant to the QE lifecycle.

## Inputs required
- `{{STORY_DESCRIPTION}}` — **Required:** Provide the complete user story, including the user goal, business context, and expected capability.
- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Provide the numbered acceptance criteria describing the expected, testable behavior.

## Prompt
```text
Act as a Senior Quality Analyst supporting a real software delivery team. Base your analysis on the supplied evidence and clearly label assumptions.
Task: Summarize business goal, expected behavior, rules, dependencies and ambiguities; do not generate tests.

Inputs:
STORY_DESCRIPTION:
{{STORY_DESCRIPTION}}
ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}

Rules:
- Break requirements into actors, triggers, preconditions, business rules and outcomes.
- Cite source IDs for every interpreted rule.
```

## Expected output
- Plain-language feature summary.
- Business-rule inventory.
- Dependency list.
- Assumptions and questions.

## Example
**Synthetic input:**
```text
STORY_DESCRIPTION: Teachers can save attendance. ACCEPTANCE_CRITERIA: Only authorized teachers may save.
```
**Illustrative response outline (synthetic, not executed):**
- Plain-language feature summary.
- Business-rule inventory.
- Dependency list.
- Assumptions and questions.

Populate each field using the sample input; mark unavailable evidence as `Not provided` rather than inventing values.

## Limitations
- Interpretations are provisional when source requirements conflict or omit business rules.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.1.0
- Status: Draft for team review
