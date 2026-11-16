# Log Analysis

## Purpose
Analyze sanitized logs for failure patterns.

## When to use
Use this prompt when investigating manual or automated test failures, application errors, API failures, integration issues, or unexpected system behavior by analyzing logs to identify failure patterns and potential root causes.

## Inputs required
- `{{SANITIZED_LOGS}}` — **Required:** Time-stamped logs with secrets and personal data removed, plus correlation identifiers if available.
- `{{INCIDENT_CONTEXT}}` — **Required:** Affected environment, build, time window, symptoms, and business impact.

## Prompt
```text
Act as a Senior Quality Assurance Engineer.
Task: Build timeline, extract error signatures, correlate evidence, distinguish hypotheses and recommend diagnostics.

Inputs:
SANITIZED_LOGS:
{{SANITIZED_LOGS}}
INCIDENT_CONTEXT:
{{INCIDENT_CONTEXT}}

Rules:
- Normalize timestamps and correlation IDs.
- group repeated error signatures.
- build an event timeline and distinguish symptoms from causes.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
Normalized incident timeline, error-signature groups with counts, affected components, evidence references, competing hypotheses, and next diagnostics.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
SANITIZED_LOGS: 10:02 request timeout; 10:03 retry failed; 10:04 upstream unavailable.
INCIDENT_CONTEXT: Staging smoke test, build 42.
```

**Illustrative output (not executed):**

10:02 timeout → 10:03 retry failure → 10:04 upstream unavailable | Hypothesis: upstream outage; needs correlation

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- Missing log coverage and clock drift may distort causality.
- redact tokens and identifiers before analysis.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
