# Requirement to Test Traceability

## Purpose
Assess whether each stated acceptance criterion has evidenced test coverage.

## When to use
After requirements and test cases are available, before coverage review or release readiness decisions.

## Inputs required
- `{{STORY_DESCRIPTION}}` — **Required:** Feature goal, user journey, and scope of the story.
- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Numbered, testable acceptance criteria and expected behavior.
- `{{TEST_CASES}}` — **Required:** Existing test IDs, descriptions, steps, and expected results to map against criteria.

## Prompt
```text
Act as a Senior Quality Analyst working with a delivery team.
Task: Assess whether each stated acceptance criterion has evidenced test coverage.

Inputs:
STORY_DESCRIPTION:
{{STORY_DESCRIPTION}}
ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}
TEST_CASES:
{{TEST_CASES}}

Instructions:
- Map each AC to existing test IDs only when the case actually verifies its behavior.
- Mark each AC Full, Partial, or Missing; explain the evidence and uncovered conditions.
- List orphan tests with no clear AC mapping and propose additional tests for gaps.
- Never confuse test design coverage with execution success.

Output format:
1. **Traceability matrix:** AC ID, requirement summary, mapped test IDs, coverage status (Full/Partial/Missing), evidence/rationale, gap.
2. **Coverage summary:** total ACs and counts by coverage status; calculate percentages only when denominator is known.
3. **Follow-up actions:** missing test suggestions, orphan test IDs, and open questions.
```

## Expected output
1. **Traceability matrix:** AC ID, requirement summary, mapped test IDs, coverage status (Full/Partial/Missing), evidence/rationale, gap.
2. **Coverage summary:** total ACs and counts by coverage status; calculate percentages only when denominator is known.
3. **Follow-up actions:** missing test suggestions, orphan test IDs, and open questions.

## Example
**Synthetic input:**
```text
STORY_DESCRIPTION: Users can sign in; locked accounts must not gain access.
ACCEPTANCE_CRITERIA:
AC-01: Valid active account can sign in.
AC-02: Locked account is rejected.
TEST_CASES:
TC-01: Enter valid active credentials; expect dashboard.

```

**Illustrative output (not executed):**
| AC | Mapped tests | Coverage | Evidence / gap |
|---|---|---|---|
| AC-01 | TC-01 | Full | Valid sign-in and dashboard assertion |
| AC-02 | None | Missing | No locked-account test |

Summary: 1/2 ACs fully covered (50%); 1 missing. Suggested test: TC-02 — locked account sign-in is rejected. Orphan tests: None.

## Limitations
- Generated artifacts are design recommendations, not proof of execution or verified application behavior.
- Do not invent requirements, business rules, observed results, or credentials. Flag gaps for human review.
- Follow `00-Library-Guide/Guardrails-Data-Privacy.md` for privacy, evidence, authorization, and review requirements.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.1.0
- Status: Draft for team review
