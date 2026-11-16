# Release Readiness Assessment

## Purpose
Assess whether exit criteria are met.

## When to use
Use this prompt when evaluating whether a software release is ready for deployment by reviewing test execution results, requirement coverage, unresolved defects, regression status, known risks, and release exit criteria to support Go/No-Go decisions.

## Inputs required
- `{{RELEASE_SCOPE}}` — **Required:** Provide the relevant release scope details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{TEST_RESULTS}}` — **Required:** Test IDs, statuses, failure details, environment, and execution timestamps.
- `{{OPEN_DEFECTS}}` — **Required:** Provide the relevant open defects details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{EXIT_CRITERIA}}` — **Required:** Provide the relevant exit criteria details, including scope, identifiers, dates, and supporting evidence where applicable.

## Prompt
```text
Act as a Senior Release Quality Manager.
Task: Compare evidence to each criterion; state blockers and residual risk; recommend Go, Conditional Go or No-Go without claiming sign-off authority.

Inputs:
RELEASE_SCOPE:
{{RELEASE_SCOPE}}
TEST_RESULTS:
{{TEST_RESULTS}}
OPEN_DEFECTS:
{{OPEN_DEFECTS}}
EXIT_CRITERIA:
{{EXIT_CRITERIA}}

Rules:
- Compare actual evidence against exit criteria.
- review open defects, risk acceptance, coverage and rollback readiness.
- flag unresolved blockers.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
Gate-by-gate readiness matrix, evidence, unresolved risks, blocking defects, dependencies, and conditional recommendation requiring owner approval.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
RELEASE_EVIDENCE: 98/100 tests passed; 2 failed; one P1 defect open.
RELEASE_CRITERIA: No open P1 defects.
```

**Illustrative output (not executed):**

Gate: No open P1 | FAIL | One P1 open | Recommendation: hold pending resolution and release owner decision

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- The prompt cannot authorize deployment.
- final go/no-go requires designated stakeholder approval.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
