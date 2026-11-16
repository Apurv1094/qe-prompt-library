# Defect Root Cause Review

## Purpose
Review root causes of recurring or escaped defects.

## When to use
Use this prompt when reviewing reported or resolved defects to investigate their underlying causes, identify gaps in requirements, development, testing, or processes, and recommend corrective and preventive actions to reduce similar defects in future releases.

## Inputs required
- `{{DEFECT_DETAILS}}` — **Required:** Provide the relevant defect details details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{TIMELINE}}` — **Required:** Provide the relevant timeline details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{TEST_EVIDENCE}}` — **Required:** Provide the relevant test evidence details, including scope, identifiers, dates, and supporting evidence where applicable.

## Prompt
```text
Act as a Senior Software Quality Root Cause Analyst.
Task: Separate confirmed facts and hypotheses; analyze requirement, process, code, environment and coverage factors; propose measurable actions.

Inputs:
DEFECT_DETAILS:
{{DEFECT_DETAILS}}
TIMELINE:
{{TIMELINE}}
TEST_EVIDENCE:
{{TEST_EVIDENCE}}
RELEVANT_TEST_CASES
{{RELEVANT_TEST_CASES}}

Rules:
- Use evidence and a structured causal method.
- separate trigger, contributing conditions and systemic process gaps.
- avoid blame.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
Evidence-backed cause-and-effect timeline, contributing factors, confirmed versus suspected causes, corrective actions, owners, and validation measures.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
DEFECT_HISTORY: Payment rounding defect found after deployment; fix in progress.
PROCESS_CONTEXT: No currency rounding boundary tests recorded.
```

**Illustrative output (not executed):**

Finding: rounding coverage absent from supplied test inventory | Root cause unconfirmed | Action: add currency boundary review

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- Root cause is a hypothesis until supported by evidence.
- multiple contributing factors may coexist.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
