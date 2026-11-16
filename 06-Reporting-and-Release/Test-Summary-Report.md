# Test Summary Report

## Purpose
Summarize testing progress and release risks.

## When to use
Use this prompt after completing a testing cycle, sprint, or release to summarize testing activities, execution results, test coverage, defect status, outstanding risks, and overall testing outcomes for stakeholders.

## Inputs required
- `{{TEST_EXECUTION_RESULTS}}` — **Required:** Provide the relevant test execution results details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{DEFECT_STATUS}}` — **Required:** Provide the relevant defect status details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{TEST_SCOPE}}` — **Required:** Provide the relevant test scope details, including scope, identifiers, dates, and supporting evidence where applicable.

## Prompt
```text
Act as a Senior QA Reporting Lead.
Task: Provide execution totals, pass/fail/blocked counts, coverage, outstanding issues, risks, next steps and evidence gaps; do not invent totals.

Inputs:
TEST_EXECUTION_RESULTS:
{{TEST_EXECUTION_RESULTS}}
DEFECT_STATUS:
{{DEFECT_STATUS}}
TEST_SCOPE:
{{TEST_SCOPE}}

Rules:
- Summarize planned vs executed tests, outcomes, blockers and defect trends for a stated build/time window.
- reconcile totals.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
Executive test summary: scope, environment, execution totals, coverage, defect breakdown, residual risks, limitations, and next actions.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
TEST_EXECUTION_DATA: 100 tests; 92 passed, 6 failed, 2 blocked.
DEFECT_SUMMARY: One P1 and two P2 open.
```

**Illustrative output (not executed):**

Execution: 92/100 passed (92% of planned tests); 6 failed; 2 blocked | Release risk: P1 open

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- A report reflects only available execution data.
- stale or incomplete reports can misrepresent readiness.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
