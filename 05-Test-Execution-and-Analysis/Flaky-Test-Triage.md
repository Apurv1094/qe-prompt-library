# Flaky Test Triage

## Purpose
Identify and prioritize intermittent tests.

## When to use
Use this prompt when automated tests produce inconsistent results across executions, such as intermittent failures or pass-on-retry behavior, to identify potential causes and recommend stabilization actions.

## Inputs required
- `{{EXECUTION_HISTORY}}` — **Required:** Provide the relevant execution history details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{FAILURE_EVIDENCE}}` — **Required:** Provide the relevant failure evidence details, including scope, identifiers, dates, and supporting evidence where applicable.

## Prompt
```text
Act as a Senior QA Automation Engineer.
Task: Calculate observed pass/fail variation where possible; group likely causes, assess confidence, suggest reproduction and fixes; do not label flaky from a single failure.

Inputs:
EXECUTION_HISTORY:
{{EXECUTION_HISTORY}}
FAILURE_EVIDENCE:
{{FAILURE_EVIDENCE}}

Rules:
- Use multiple execution runs.
- compute pass/fail rate and transitions.
- distinguish intermittent behavior from consistently failing tests.
- correlate failure signatures.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
Test stability summary, flaky candidates with run denominators, evidence signatures, probable contributing factors, and prioritized investigation steps.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
TEST_EXECUTION_HISTORY: LOGIN-03 passed 7/10 comparable runs, failed 3/10.
FAILURE_LOGS: Timeout waiting for login button on failed runs.
```

**Illustrative output (not executed):**

LOGIN-03 | 3 failures / 10 runs | Flaky candidate | Timeout signature | Investigate readiness and environment; root cause unconfirmed

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- One failure cannot establish flakiness.
- retries alone do not prove root cause.
- small samples reduce confidence.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
