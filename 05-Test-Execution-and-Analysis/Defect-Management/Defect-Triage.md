# Defect Triage

## Purpose
Prioritize defects for action.

## When to use
Use this prompt when reviewing reported defects to assess their validity, severity, priority, business impact, potential duplication, and recommended resolution order.

## Inputs required
- `{{DEFECT_LIST}}` — **Required:** Defect IDs, descriptions, severity evidence, frequency, and current states.
- `{{RELEASE_CONTEXT}}` — **Required:** Release timeline, impacted features, customer exposure, and blocking criteria.

## Prompt
```text
Act as a Senior Quality Analyst Lead.
Task: Assess severity, priority, reproducibility, customer impact, workaround and ownership recommendations; avoid final business decisions.

Inputs:
DEFECT_LIST:
{{DEFECT_LIST}}
RELEASE_CONTEXT:
{{RELEASE_CONTEXT}}

Rules:
- Group duplicate issues.
- prioritize by user impact, frequency, workaround and release risk.
- distinguish severity from urgency.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
Prioritized triage table: defect ID, severity, priority, impact, reproducibility, workaround, suggested owner, disposition, and supporting rationale.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
DEFECT_LIST: BUG-01 checkout fails for all users; BUG-02 tooltip clipped on hover.
RELEASE_CONTEXT: Checkout release tomorrow.
```

**Illustrative output (not executed):**

BUG-01 | Critical severity | P0 proposed | Blocks purchase | Owner: checkout team | Escalate; validate scope

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- Priority is a team decision.
- incomplete reproduction evidence may change classification.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
