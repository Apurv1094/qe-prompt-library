# Escaped Defect Analysis

## Purpose
Learn from production issues missed by testing.

## When to use
Use this prompt when defects are discovered in production or downstream environments after passing earlier testing stages to understand why they were missed, identify gaps in test coverage or quality processes, and recommend preventive improvements.

## Inputs required
- `{{PRODUCTION_ISSUE}}` — **Required:** Provide the relevant production issue details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{RELEASE_TEST_EVIDENCE}}` — **Required:** Provide the relevant release test evidence details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{INCIDENT_TIMELINE}}` — **Required:** Provide the relevant incident timeline details, including scope, identifiers, dates, and supporting evidence where applicable.

## Prompt
```text
Act as a Senior Defect Prevention Analyst.
Task: Map escape point, detection gap, impact and contributing factors; propose prevention with owners, verification and non-blaming language.

Inputs:
PRODUCTION_ISSUE:
{{PRODUCTION_ISSUE}}
RELEASE_TEST_EVIDENCE:
{{RELEASE_TEST_EVIDENCE}}
INCIDENT_TIMELINE:
{{INCIDENT_TIMELINE}}
TEST_INVENTORY
{TEST_INVENTORY}

Rules:
- Trace production issue to missed detection opportunities.
- assess requirement, test, environment and release controls.
- recommend preventive actions.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
Escaped defect register, missed detection opportunities, coverage/process gaps, impact, hypotheses, preventive controls, and measurable follow-up.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
ESCAPED_DEFECTS: PROD-12 coupon discount incorrect for zero-value cart.
TEST_COVERAGE: Only positive coupon tests documented.
```

**Illustrative output (not executed):**

PROD-12 | Missed zero-value boundary | Proposed prevention: add boundary scenario | Validate against requirements

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- Production evidence may be incomplete.
- hindsight must not be treated as proof that a defect was easily detectable.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
