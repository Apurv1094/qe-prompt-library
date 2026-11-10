# Release Readiness Assessment

**Module:** QE-Prompt-Library-Completed

## Purpose
Assess release quality based on supplied evidence.

## When to use
Use during the relevant sprint, test execution, or release activity when the required inputs are available.

## Required inputs
```text
{{RELEASE_SCOPE}}
{{TEST_RESULTS}}
{{OPEN_DEFECTS}}
{{EXIT_CRITERIA}}
```

## Reusable prompt
```text
Act as a senior Quality Engineer supporting a real delivery team.

Task: Compare evidence against release exit criteria. Identify missing evidence, residual risks and blockers. Recommend Go, Conditional Go or No-Go with justification; never claim final sign-off authority.

Inputs:
{{RELEASE_SCOPE}}
{{TEST_RESULTS}}
{{OPEN_DEFECTS}}
{{EXIT_CRITERIA}}

Rules:
- Base conclusions only on supplied information.
- Clearly mark missing inputs and assumptions; ask focused questions where necessary.
- Keep output concise, practical, and reusable across tools and projects.
- Never claim a test, code change, or validation was executed without evidence.
- Do not expose secrets or production personal data.

Return: Criteria assessment; risks; missing evidence; recommendation; approvals needed.
```

## Expected output
Criteria assessment; risks; missing evidence; recommendation; approvals needed.

## QE validation checklist
- [ ] Output matches supplied requirements and evidence.
- [ ] Missing information and assumptions are visible.
- [ ] Recommendations are actionable and appropriately prioritized.
- [ ] A QE has reviewed the output before it is used for delivery or sign-off.
