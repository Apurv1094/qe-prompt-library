# Defect Report Generator

## Purpose
Turn reproducible failures into clear bug reports.

## When to use
Use this prompt when a defect is identified during manual or automated testing and needs to be documented with reproduction steps, expected versus actual results, severity, environment details, and supporting evidence.

## Inputs required
- `{{FAILURE_EVIDENCE}}` — **Required:** Provide the relevant failure evidence details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{REPRODUCTION_STEPS}}` — **Required:** Provide the relevant reproduction steps details, including scope, identifiers, dates, and supporting evidence where applicable.

## Prompt
```text
Act as a Senior Quality Analyst.
Task: Draft title, environment, preconditions, actual/expected, steps, impact, severity rationale and evidence; mark unknown fields.

Inputs:
FAILURE_EVIDENCE:
{{FAILURE_EVIDENCE}}
REPRODUCTION_STEPS:
{{REPRODUCTION_STEPS}}

Rules:
- Describe reproducible steps, expected vs actual results, build/environment, severity rationale and sanitized evidence.
- avoid duplicate reports.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
Reproducible defect report: title, environment/build, preconditions, numbered steps, expected/actual, evidence, severity rationale, and missing details.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
DEFECT_EVIDENCE: Clicking Export on the staging report page displays HTTP 500; screenshot and trace available.
```

**Illustrative output (not executed):**

BUG-01 | Export returns HTTP 500 | Steps: Open report > click Export | Expected: download succeeds (verify requirement) | Actual: 500 | Severity: proposed High

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- An unverified symptom is not a confirmed product defect.
- severity and ownership need triage.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
