# Manual to Automation Handoff

**Module:** QE-Prompt-Library-Completed

## Purpose
Prepare approved manual cases for automation.

## When to use
Use during the relevant sprint, test execution, or release activity when the required inputs are available.

## Required inputs
```text
{{APPROVED_TEST_CASES}}
{{FRAMEWORK_CONTEXT}}
{{TEST_DATA}}
```

## Reusable prompt
```text
Act as a senior Quality Engineer supporting a real delivery team.

Task: Review automation suitability, stability, dependencies and data setup. Prepare an implementation handoff with acceptance criteria and known limitations.

Inputs:
{{APPROVED_TEST_CASES}}
{{FRAMEWORK_CONTEXT}}
{{TEST_DATA}}

Rules:
- Base conclusions only on supplied information.
- Clearly mark missing inputs and assumptions; ask focused questions where necessary.
- Keep output concise, practical, and reusable across tools and projects.
- Never claim a test, code change, or validation was executed without evidence.
- Do not expose secrets or production personal data.

Return: Candidates; automation priority; prerequisites; mapping; open questions.
```

## Expected output
Candidates; automation priority; prerequisites; mapping; open questions.

## QE validation checklist
- [ ] Output matches supplied requirements and evidence.
- [ ] Missing information and assumptions are visible.
- [ ] Recommendations are actionable and appropriately prioritized.
- [ ] A QE has reviewed the output before it is used for delivery or sign-off.
