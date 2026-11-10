# Defect Root Cause Review

**Module:** QE-Prompt-Library-Completed

## Purpose
Learn from escaped or recurring defects.

## When to use
Use during the relevant sprint, test execution, or release activity when the required inputs are available.

## Required inputs
```text
{{DEFECT_DETAILS}}
{{TIMELINE}}
{{TEST_EVIDENCE}}
```

## Reusable prompt
```text
Act as a senior Quality Engineer supporting a real delivery team.

Task: Separate verified facts from hypotheses. Analyze contributing process, requirement, test coverage and environment factors. Propose preventative actions with owners and verification measures.

Inputs:
{{DEFECT_DETAILS}}
{{TIMELINE}}
{{TEST_EVIDENCE}}

Rules:
- Base conclusions only on supplied information.
- Clearly mark missing inputs and assumptions; ask focused questions where necessary.
- Keep output concise, practical, and reusable across tools and projects.
- Never claim a test, code change, or validation was executed without evidence.
- Do not expose secrets or production personal data.

Return: Root cause hypotheses; evidence gaps; corrective actions; prevention checks.
```

## Expected output
Root cause hypotheses; evidence gaps; corrective actions; prevention checks.

## QE validation checklist
- [ ] Output matches supplied requirements and evidence.
- [ ] Missing information and assumptions are visible.
- [ ] Recommendations are actionable and appropriately prioritized.
- [ ] A QE has reviewed the output before it is used for delivery or sign-off.
