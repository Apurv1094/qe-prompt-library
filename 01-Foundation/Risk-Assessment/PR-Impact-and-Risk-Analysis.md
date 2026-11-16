# PR Impact and Risk Analysis

## Purpose
Review a pull request from a QA perspective to identify affected functionality, regression risks, and focused testing needed before merge or release.

## When to use
Use when a pull request changes application code, APIs, configuration, database logic, or integrations and QA needs to assess test impact and regression scope.

## Inputs required
- `{{CHANGESET_OR_PR_DIFF}}` — **Required:** Provide an accessible PR diff or changed code/configuration with file paths. **Example:** `src/checkout/voucherValidator.ts` now rejects expired vouchers; include the actual diff for code-level conclusions.
- `{{CHANGE_CONTEXT}}` — **Required:** Explain why the change was made, its related story or defect, and expected behavior. **Example:** PR-142 / STORY-58: Expired vouchers must be rejected during checkout in release 2.5.

## Prompt
```text
Role: Act as a Senior QA Automation Engineer specializing in change-impact analysis and risk-based regression testing.

Task: Analyze the supplied PR diff and change context to identify affected functionality, risks, and the most relevant tests. Do not modify code or execute tests unless separately authorized.

Inputs:
CHANGESET_OR_PR_DIFF:
{{CHANGESET_OR_PR_DIFF}}
CHANGE_CONTEXT:
{{CHANGE_CONTEXT}}

Instructions:
1. Identify the changed files, methods, API contracts, database/configuration changes, and their intended behavior. Cite file paths and relevant diff lines where available.
2. Distinguish directly changed behavior from potentially impacted downstream workflows; label inferred impacts as unverified.
3. Map the change to user journeys, integrations, security/data concerns, and existing regression areas.
4. Assess each risk by Impact (1–3) and Likelihood (1–3), explain the rationale, and rank P1 (7–9), P2 (4–6), or P3 (1–3). Escalate critical security/data risks when appropriate.
5. Recommend focused positive, negative, boundary, API/UI, integration, and regression checks only where relevant. Include tests for unchanged behavior that could regress.
6. Identify existing automated tests that should be reviewed or executed if visible; otherwise say coverage is not verified.
7. Flag missing evidence, test gaps, and follow-up questions. State what additional review or execution would confirm each risk.

Rules:
- Inspect only the code and evidence actually accessible; never claim unseen files were reviewed.
- If only a change summary is provided instead of a diff, produce a provisional impact assessment and request the diff for code-level conclusions.
- Do not claim tests passed, coverage exists, or a PR is safe to merge without evidence.
- Separate observed changes from inferred impact and recommendations.
- Keep recommendations specific, prioritized, and suitable for a QA review comment.
```

## Expected output
1. **Change Summary:** What code or behavior changed. **Example:** Voucher validation now rejects expired codes.
2. **Changed Components:** Files, methods, APIs, or configurations affected. **Example:** `voucherValidator.ts` — expiry check updated.
3. **Impact and Risk Matrix:** Affected workflow, evidence, likelihood, impact, priority, and rationale. **Example:** Checkout discount calculation — P1 if an incorrect discount can alter order totals.
4. **Targeted Test Recommendations:** Specific high-value checks to run or add. **Example:** Expired voucher rejected; valid voucher still applies; boundary around expiry time.
5. **Regression and Automation Impact:** Existing tests potentially affected or missing. **Example:** Review voucher API regression and checkout UI tests; automation status unverified.
6. **Open Questions and Review Recommendation:** Missing evidence and next actions. **Example:** Confirm expiry timezone; request targeted test results before merge decision.

## Example
**Synthetic input:**
```text
CHANGESET_OR_PR_DIFF: Summary only — checkout validation now rejects expired vouchers; actual diff not supplied.
CHANGE_CONTEXT: Release 2.5; STORY-58 requires expired vouchers to be rejected without changing valid voucher behavior.
```

**Illustrative output (not executed):**

| Area | Possible impact | Priority* | Recommended check |
|---|---|---|---|
| Voucher validation | Expired codes may still be accepted | P1 | Reject expired voucher |
| Checkout totals | Valid discounts may regress | P1 | Verify valid voucher and final total |
| Expiry boundary | Timezone or cutoff behavior unclear | P2 | Test just before, at, and after expiry once rule is confirmed |

*Priorities are provisional. No code was inspected or tests executed. Obtain the actual diff and clarify expiry timezone before finalizing impact and merge recommendations.*

## Limitations
- A change summary is not a substitute for inspecting an actual diff.
- Static review cannot prove runtime behavior, test coverage, or release readiness.
- QA, development, and relevant reviewers must confirm high-impact risks and merge decisions.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
