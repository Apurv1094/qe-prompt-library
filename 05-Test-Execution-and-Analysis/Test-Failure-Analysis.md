# Test Failure Analysis

## Purpose
Classify failed test executions and next actions.

## When to use
Use this prompt when manual or automated test cases fail during execution and the QA team needs to analyze failure evidence, distinguish application defects from test script or environment issues, and recommend corrective actions.

## Inputs required
- `{{FAILED_TEST_RESULTS}}` — **Required:** Provide the relevant failed test results details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{EXECUTION_CONTEXT}}` — **Required:** Provide the relevant execution context details, including scope, identifiers, dates, and supporting evidence where applicable.

## Prompt
```text
Act as a Senior Test Failure Diagnostics Engineer.
Task: Separate application defect, test defect, data, environment and unknown; cite evidence and recommend reproducible next checks.

Inputs:
FAILED_TEST_RESULTS:
{{FAILED_TEST_RESULTS}}
EXECUTION_CONTEXT:
{{EXECUTION_CONTEXT}}

Rules:
- Classify each failed test using assertion, environment, data, timeout or dependency evidence.
- identify reproducibility and owner.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
Failure inventory with evidence, classification, suspected causes versus confirmed causes, investigation actions, and ownership suggestions.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
TEST_RESULTS: ORDER-04 failed with expected 201, actual 500.
BUILD_CONTEXT: CI build 42, staging.
```

**Illustrative output (not executed):**

ORDER-04 | API status mismatch | Confirmed: 500 response | Cause: unknown | Next: inspect server logs and request correlation ID

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- A stack trace alone rarely proves root cause.
- distinguish product defects from test or environment faults.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
