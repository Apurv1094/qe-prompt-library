# Regression Suite Improvement

## Purpose
Analyze an existing automation regression suite and its execution history to identify redundant, slow, unstable, or missing tests, and recommend risk-based improvements without reducing important coverage.

## When to use
Use during regression-suite maintenance, sprint retrospectives, CI optimization, or before a major release when the automation repository and execution results are accessible.

## Inputs required

- `{{AUTOMATION_REPOSITORY_PATH}}` — **Required:** Accessible path or repository containing the existing automated regression tests.
- `{{EXECUTION_REPORTS_PATH}}` — **Required:** Location of historical execution reports and their date range.
- `{{REQUIREMENTS_OR_TEST_MAPPING}}` — **Optional:** Optional requirement-to-test links or business-critical workflow inventory.
- `{{IMPROVEMENT_GOAL}}` — **Optional:** Optional measurable optimization target such as runtime, stability, or duplication reduction.

## Prompt

```text
Act as a Senior Regression Automation Architect.

Objective:
Inspect the existing automation repository and available execution history. Build an evidence-based regression suite health assessment and a prioritized improvement plan. Do not modify or delete tests unless explicitly authorized.

Inputs:
AUTOMATION_REPOSITORY_PATH: {{AUTOMATION_REPOSITORY_PATH}}
EXECUTION_REPORTS_PATH: {{EXECUTION_REPORTS_PATH}}
REQUIREMENTS_OR_TEST_MAPPING: {{REQUIREMENTS_OR_TEST_MAPPING}}
IMPROVEMENT_GOAL: {{IMPROVEMENT_GOAL}}

Process:
1. Verify access to the repository and reports. If unavailable, state exactly what is inaccessible and request an export or relevant files. Never pretend to have scanned inaccessible content.
2. Discover tests programmatically using the framework's test listing, repository search, or a lightweight parsing script. Capture test ID/name, file path, module, tags/priority (if present), and relevant assertion or workflow evidence. Deduplicate test identities across report runs.
3. Parse available execution reports and correlate records to tests. Calculate run count, pass/fail/skip counts, failure frequency, retry outcomes (if present), and runtime statistics. Identify reporting window, missing runs, and unmatched test IDs. Use a script for aggregation when the suite is large; do not paste every test into the model context.
4. Flag potential duplicate tests by comparing business intent, setup, steps, assertions, and coverage. Similar titles alone do not prove duplication.
5. Identify slow tests using measured durations, preferably median and p95 where enough samples exist. Distinguish summed test duration from actual parallel CI wall-clock time.
6. Identify unstable/flaky candidates using inconsistent outcomes across comparable runs, retries, and failure evidence. Do not equate every failed test with a flaky test. Distinguish application defects from test/environment instability when evidence permits.
7. Assess business criticality and coverage gaps using requirements or traceability when available. If mappings are missing, label coverage conclusions provisional and list validation needed before pruning.
8. Recommend a decision for each prioritized candidate: RETAIN, REFACTOR, COMBINE, INVESTIGATE, or RETIRE-CANDIDATE. Explain evidence, risk, estimated benefit, and coverage safeguards. Never recommend unconditional removal of critical coverage.
9. Produce an actionable backlog with priority, proposed owner role, validation steps, and measurable targets. Mark unsupported estimates as estimates, not measured results.

Rules:
- Remain read-only unless the user explicitly approves implementation.
- Never run destructive tests or modify CI settings without approval.
- Cite file paths, test IDs, report filenames, and line numbers when available.
- Do not expose secrets, credentials, or personal data found in source or logs.
- State the exact analyzed period and the number of tests and execution records examined.
- Use 'Not provided' for missing evidence; do not invent counts, coverage, owners, or trends.
- Separate confirmed findings from hypotheses and proposed improvements.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output

1. **Scope and evidence:** repository/framework, reporting period, test count, execution record count, data gaps.
2. **Suite health scorecard:** pass/fail/skip distribution, failure frequency, flaky candidates, slow tests, measured runtimes, and coverage confidence; include formulas and denominators.
3. **Candidate findings:** test ID/file, issue type, supporting evidence, severity, and proposed action.
4. **Prioritized improvement backlog:** retain/refactor/combine/investigate/retire-candidate, expected benefit, suggested owner role, and validation steps.
5. **Coverage safeguards:** critical workflows protected, traceability gaps, and approval requirements before any retirement.
6. **Before/after targets:** baseline, measurable goal, measurement method, and follow-up validation plan.

## Example inputs

```text
AUTOMATION_REPOSITORY_PATH: ./tests/
EXECUTION_REPORTS_PATH: ./test-results/history/
REQUIREMENTS_OR_TEST_MAPPING: Not provided
IMPROVEMENT_GOAL: Reduce regression CI wall-clock time by 20%, investigate flaky tests, and preserve critical checkout and authentication coverage.
```

**Example response outline (illustrative, not executed):**
- Repository/report access: Not yet verified.
- Inventory and runtime metrics: Pending source inspection.
- Potential duplication: Requires test behavior and assertion comparison.
- Coverage confidence: Limited until requirement mapping is supplied.
- Next step: Scan the accessible repository and reports, then produce the scorecard and prioritized backlog.

## Limitations
- Repository access and report parsing require an enabled coding agent or scripts; a text-only chat cannot inspect local paths automatically.
- Static similarity does not prove two tests are redundant.
- Failure counts alone cannot establish flakiness or root cause.
- Historical timings may not predict future parallel CI runtime.
- Missing traceability limits confidence in test retirement decisions.

Shared privacy, evidence, authorization, and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
