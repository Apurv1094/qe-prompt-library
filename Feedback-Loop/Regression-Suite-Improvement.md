# Regression Suite Improvement

**Module:** QE-Prompt-Library-Completed

## Purpose
Improve regression efficiency using execution evidence.

## When to use
Use during the relevant sprint, test execution, or release activity when the required inputs are available.

## Required input
```text
{{REGRESSION_HISTORY}}
{{DEFECT_HISTORY}}
{{CURRENT_SUITE}}
```

## Reusable prompt
```text
Act as a senior Quality Engineer supporting a real delivery team.

Task: Identify redundant, flaky, slow and high-value tests using provided evidence. Recommend additions, removals or prioritization; do not remove tests without risk review.

Inputs:
{{REGRESSION_HISTORY}}
{{DEFECT_HISTORY}}
{{CURRENT_SUITE}}

Rules:
- Base conclusions only on supplied information.
- Clearly mark missing inputs and assumptions; ask focused questions where necessary.
- Keep output concise, practical, and reusable across tools and projects.
- Never claim a test, code change, or validation was executed without evidence.
- Do not expose secrets or production personal data.

Return: Optimization candidates; impact; priority; validation plan.
```

## Expected output
Optimization candidates; impact; priority; validation plan.

## QE validation checklist
- [ ] Output matches supplied requirements and evidence.
- [ ] Missing information and assumptions are visible.
- [ ] Recommendations are actionable and appropriately prioritized.
- [ ] A QE has reviewed the output before it is used for delivery or sign-off.
