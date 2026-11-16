# QE Metrics

## Purpose
Produce interpretable QE metrics from evidence.

## When to use
Use this prompt when analyzing testing data to calculate and report key Quality Engineering metrics such as test execution pass rate, defect density, defect leakage, automation coverage, and test flakiness to evaluate testing effectiveness and identify improvement opportunities.

## Inputs required
- `{{METRIC_SOURCE_DATA}}` — **Required:** Raw counts and evidence for executions, defects, coverage, and instability, including denominators.
- `{{REPORTING_PERIOD}}` — **Required:** Start and end dates, release, or sprint used to calculate and compare metrics.

## Prompt
```text
Act as a Senior Quality Metrics Analyst.
Task: Compute applicable pass rate, defect leakage, automation coverage and flakiness with formulas, denominators, caveats and trend if data permits.

Inputs:
METRIC_SOURCE_DATA:
{{METRIC_SOURCE_DATA}}
REPORTING_PERIOD:
{{REPORTING_PERIOD}}

Rules:
- Define metric formulas and reporting windows.
- distinguish counts, rates and trends.
- call out denominators and missing data.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
QE scorecard with metric formula, numerator, denominator, reporting window, computed result, interpretation, caveats, and comparison if baseline exists.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
METRIC_SOURCE_DATA: 90 passed out of 100 executed; 3 escaped defects; no prior period.
REPORTING_PERIOD: October 2026.
```

**Illustrative output (not executed):**

Pass rate | 90 / 100 | 90% | October 2026; trend unavailable without prior period

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- Metrics can be misleading without context.
- defect counts or pass rates alone do not measure product quality.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
