# Testability Assessment Prompt

## Purpose

Run this **after** Requirement Understanding and Gap Analysis, **before** Test Design.

It answers a different question than Gap Analysis:

> "Even if this requirement is well-defined, can we actually set it up and verify it in our test environment?"

It does not judge requirement quality and does not create test cases.

---

## Inputs

| Input | Required? |
|---|---|
| `APP_OVERVIEW` | Yes |
| `EPIC_DESCRIPTION` | Yes |
| `STORY_DESCRIPTION` | Yes |
| `ACCEPTANCE_CRITERIA` | Yes |
| `SYSTEM_TEST_ENVIRONMENT_CONTEXT` | Optional — what's controllable/observable in test (e.g., can you force an order into a given status? is the payment/logistics service mocked or live? are logs/DB access available?). If not provided, mark related items as **Unknown**, not blocked. |
| `GAP_ANALYSIS_OUTPUT` | Optional — prior unresolved gaps, so they aren't repeated here |

### Example Input

```text
APP_OVERVIEW:
""""

EPIC_DESCRIPTION:
""""
STORY_DESCRIPTION:
""""
ACCEPTANCE_CRITERIA:
""""
SYSTEM_TEST_ENVIRONMENT_CONTEXT:
""""

GAP_ANALYSIS_OUTPUT:
""""
(Paste unresolved gaps/questions from the Gap Analysis output here, if available.)
```

---

## Prompt

```text
You are a senior QA engineer assessing testability, not requirement quality.

Given APP_OVERVIEW, EPIC_DESCRIPTION, STORY_DESCRIPTION, ACCEPTANCE_CRITERIA, and
optionally SYSTEM_TEST_ENVIRONMENT_CONTEXT and GAP_ANALYSIS_OUTPUT, assess whether
the described behavior can be set up, executed, and verified in the test environment.

Do not re-analyze requirement clarity/completeness (that's Gap Analysis's job).
Do not write test cases, test data, or automation recommendations (that's Test Design's job).
If SYSTEM_TEST_ENVIRONMENT_CONTEXT doesn't cover something, mark it Unknown — never assume.

Assess:
1. Controllability — can required preconditions/states be set up directly, or only via a full end-to-end flow?
2. Observability — can expected outcomes be verified (UI, API, DB, logs)?
3. Dependency testability — can external systems (payment, logistics, etc.) be tested in isolation (sandbox/mock), or only live?
4. Determinism — is the behavior reliably repeatable, or timing/async-dependent?
5. Test data feasibility — can the needed data/states be created on demand?

For each issue found, provide:
- **Type:** Controllability / Observability / Dependency / Determinism / Test Data
- **Priority:** High / Medium / Low
- **Requirement Reference**
- **Issue**
- **Why It Matters**
- **Clarification Needed** (for QA Lead / DevOps / Engineering — not the BA/PO)

Output using this structure:

# Testability Assessment

## Overall Testability
(Testable As-Is / Testable With Setup Needed / Not Reliably Testable Without Clarification)

## Identified Issues
(list using the format above; if none, say so)

## Dependency Testability Summary
(one line per external system: confirmed / unknown / blocked)

## Clarification Questions
(consolidated list for QA Lead/DevOps/Engineering)

## Recommendation
(ready for Test Design or not, and why)
```

---

# Key Principles

1. **Unknown ≠ Not Testable.** Missing environment info is a question to ask, not a confirmed blocker.
2. **Don't repeat Gap Analysis.** If something is untestable only because the requirement itself is undefined, note the dependency in one line — don't re-analyze it.
3. **Don't drift into Test Design.** "Can we verify X?" is testability. "Verify X with these inputs" is a test case.
4. **Only flag what matters.** Skip trivial tooling inconveniences that won't affect test design.

---

# Where It Fits

Requirement Understanding → Gap Analysis → **Testability Assessment** → Test Design

Same `APP_OVERVIEW` / `EPIC_DESCRIPTION` / `STORY_DESCRIPTION` / `ACCEPTANCE_CRITERIA` inputs are reused across all stages so they can run sequentially without reformatting.