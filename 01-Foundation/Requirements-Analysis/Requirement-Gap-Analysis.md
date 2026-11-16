# Requirement Gap Analysis

## Purpose
Identify missing or ambiguous requirements.

## When to use
Use when the required inputs are available and this activity is relevant to the QE lifecycle.

## Inputs required
- `{{STORY_DESCRIPTION}}` — **Required:** Provide the complete user story, including the user goal, business context, and expected capability.
- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Provide the numbered acceptance criteria describing the expected, testable behavior.

## Prompt
```text
Act as a Senior Quality Analyst supporting a real software delivery team. Base your analysis on the supplied evidence and clearly label assumptions.
Task: List gaps, their testing impact, and specific clarification questions; distinguish facts from assumptions.

Inputs:
STORY_DESCRIPTION:
{{STORY_DESCRIPTION}}
ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}

Rules:
- Check each requirement for ambiguity, testability, missing validation, conflicting conditions and error handling.
- Assign gap IDs and severity.
```

## Expected output
- Gap register with requirement reference, issue, impact, suggested clarification, owner and priority.

## Example
**Synthetic input:**
```text
STORY_DESCRIPTION: Users can reset passwords. ACCEPTANCE_CRITERIA: Reset link expires.
```
**Illustrative response outline (synthetic, not executed):**
- Gap register with requirement reference, issue, impact, suggested clarification, owner and priority.

Populate each field using the sample input; mark unavailable evidence as `Not provided` rather than inventing values.

## Limitations
- Missing details cannot be resolved without product-owner decisions.
- Proposed wording is not an approved requirement.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.1.0
- Status: Draft for team review
