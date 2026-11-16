# Test Case Generator

## Purpose
Translate requirements into reviewable, step-by-step manual test cases.

## When to use
After acceptance criteria are defined and detailed manual execution steps are needed.

## Inputs required
- `{{STORY_DESCRIPTION}}` — **Required:** User goal, feature behavior, actors, and scope.
- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Numbered conditions of satisfaction with observable expected results.

## Prompt
```text
Act as a Senior Quality Analyst working with a delivery team.
Task: Translate requirements into reviewable, step-by-step manual test cases.

Inputs:
STORY_DESCRIPTION:
{{STORY_DESCRIPTION}}
ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}

Instructions:
- Derive cases from supplied acceptance criteria; map every case to an AC ID.
- Cover positive, negative, boundary, and state cases only where supported by requirements.
- Write reproducible preconditions, numbered actions, and matching expected results.
- Assign unique IDs and a justified priority; use fictional test data.
- Mark missing behavior as Clarification needed instead of guessing.

Output format:
1. **Test case table:** Test ID, title, AC reference, category, priority, preconditions, test data, steps, expected results.
2. **Coverage check:** ACs covered and any unaddressed criteria.
3. **Clarifications:** unspecified messages, limits, or workflows that block reliable expected results.
```

## Expected output
1. **Test case table:** Test ID, title, AC reference, category, priority, preconditions, test data, steps, expected results.
2. **Coverage check:** ACs covered and any unaddressed criteria.
3. **Clarifications:** unspecified messages, limits, or workflows that block reliable expected results.

## Example
**Synthetic input:**
```text
STORY_DESCRIPTION: Users can update the email address in their profile.
ACCEPTANCE_CRITERIA:
AC-01: An email address without @ is rejected and the profile is not updated.
```

**Illustrative output (not executed):**
| ID | Title | AC | Type | Priority |
|---|---|---|---|---|
| TC-01 | Reject malformed profile email | AC-01 | Negative | High |

**Preconditions:** User is signed in and can edit their profile. **Test data:** `invalid.example.com` (fictional).

1. Open profile editing. **Expected:** Email editing control is available.
2. Enter `invalid.example.com` and submit. **Expected:** The email is rejected; the stored profile email remains unchanged.

**Coverage:** AC-01 covered. **Clarification:** Exact error wording and presentation are not specified; do not assert a particular message.

## Limitations
- Generated artifacts are design recommendations, not proof of execution or verified application behavior.
- Do not invent requirements, business rules, observed results, or credentials. Flag gaps for human review.
- Follow `00-Library-Guide/Guardrails-Data-Privacy.md` for privacy, evidence, authorization, and review requirements.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.1.0
- Status: Draft for team review
