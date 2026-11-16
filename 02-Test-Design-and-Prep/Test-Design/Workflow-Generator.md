# Workflow Generator

## Purpose
Organize related test cases into efficient, traceable execution workflows.

## When to use
When existing test cases need an ordered journey for execution or automation planning.

## Inputs required
- `{{TEST_CASES}}` — **Required:** Test IDs, prerequisites, steps, assertions, and any shared state or data.
- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Criteria the workflow must continue to verify without losing individual coverage.

## Prompt
```text
Act as a Senior End-to-End Test Architect working with a delivery team.
Task: Organize related test cases into efficient, traceable execution workflows.

Inputs:
TEST_CASES:
{{TEST_CASES}}
ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}

Instructions:
- Group only compatible cases by shared user journey, setup, and state dependencies.
- Specify ordered case IDs, setup, assertion checkpoints, teardown, and data handoffs.
- Preserve original test IDs and independent assertions; identify cases that should remain isolated.
- Mark dependencies that are not evidenced in inputs as unverified.
- Do not require page objects or selectors to produce a workflow design.

Output format:
1. **Workflow table:** Workflow ID, purpose, ordered case IDs, prerequisites, state/data dependencies, checkpoints, cleanup.
2. **Coverage map:** AC-to-workflow/test ID mapping.
3. **Isolation notes:** tests that should remain independently executable and risks of coupled failures.
```

## Expected output
1. **Workflow table:** Workflow ID, purpose, ordered case IDs, prerequisites, state/data dependencies, checkpoints, cleanup.
2. **Coverage map:** AC-to-workflow/test ID mapping.
3. **Isolation notes:** tests that should remain independently executable and risks of coupled failures.

## Example
**Synthetic input:**
```text
TEST_CASES:
TC-01: Sign in successfully; expect dashboard.
TC-02: Verify dashboard header; requires signed-in user.
TC-03: Verify dashboard cards; requires signed-in user.
ACCEPTANCE_CRITERIA:
AC-01: Dashboard is visible after successful login.
```

**Illustrative output (not executed):**
| Workflow | Ordered tests | Setup | Checkpoints | Cleanup |
|---|---|---|---|---|
| WF-01 Dashboard smoke | TC-01 → TC-02 → TC-03 | Fresh signed-out session | TC-01 dashboard visible; TC-02 header; TC-03 cards | Sign out/reset session |

**Coverage:** AC-01 → WF-01 / TC-01. TC-02 and TC-03 are supplementary checks without separately supplied ACs.

**Isolation note:** Keep TC-02 and TC-03 independently runnable with their own sign-in fixture so TC-01 failure does not mask their results.

## Limitations
- Generated artifacts are design recommendations, not proof of execution or verified application behavior.
- Do not invent requirements, business rules, observed results, or credentials. Flag gaps for human review.
- Follow `00-Library-Guide/Guardrails-Data-Privacy.md` for privacy, evidence, authorization, and review requirements.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.1.0
- Status: Draft for team review
