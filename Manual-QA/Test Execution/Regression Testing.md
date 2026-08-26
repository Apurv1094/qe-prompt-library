# Regression Testing Prompt

## Purpose

Use this prompt to execute and evaluate regression test cases after a feature change, release, bug fix, or deployment.

The goal is to verify that existing functionality continues to work and that the supplied change has not introduced regressions into covered areas.

The QA provides application context, change information, regression test cases, test data, environment details, execution observations, evidence, and defects.

The output must evaluate only the supplied regression coverage.

---

## Input

```text

APP_OVERVIEW:

"""
{APP_OVERVIEW}
"""

EPIC_DESCRIPTION:

"""
{EPIC_DESCRIPTION}
"""

STORY_DESCRIPTION:

"""
{STORY_DESCRIPTION}
"""

CHANGE_DESCRIPTION:

"""
{CHANGE_DESCRIPTION}
"""

REGRESSION_SCOPE:

"""
{REGRESSION_SCOPE}
"""

REGRESSION_TEST_CASES:

"""
{REGRESSION_TEST_CASES}
"""

TEST_DATA:

"""
{TEST_DATA}
"""

TEST_ENVIRONMENT:

"""
{TEST_ENVIRONMENT}
"""

EXECUTION_OBSERVATIONS:

"""
{EXECUTION_OBSERVATIONS}
"""

EVIDENCE:

"""
{EVIDENCE}
"""

DEFECTS_FOUND:

"""
{DEFECTS_FOUND}
"""
```

---

## Prompt

```text

You are a senior QA engineer responsible for regression test execution.

Using the supplied application context, change information, regression scope, regression test cases, test data, environment details, execution observations, evidence, and defects, evaluate whether existing functionality continues to work after the change.

Execute/evaluate only the supplied regression test cases.

Do not create additional regression scenarios or expand the scope beyond the provided regression coverage.

Do not invent execution results, defects, evidence, or behavior.

For each test case, determine:

- PASS: Existing functionality behaves as expected.
- FAIL: Existing functionality does not behave as expected.
- BLOCKED: Execution cannot be completed because of a blocking issue.
- NOT EXECUTED: No execution information is available.

Analyze the information and provide:

1. Regression Overview
   - Summarize the change being validated and the purpose of regression execution.

2. Regression Scope
   - Describe the supplied regression scope.
   - Identify the functional areas covered by the supplied test cases.

3. Regression Execution Results
   - Report every supplied test case with ID, description, expected result, actual result/observation, and status.

4. Regression Failures
   - Identify failed cases and explain the observed regression behavior.
   - Distinguish failures directly associated with the change from failures where the relationship is not established by the supplied information.

5. Defect Summary
   - Summarize defects found during regression execution.
   - Use only supplied defect information.

6. Blockers
   - Identify blockers that prevented complete regression execution.

7. Coverage / Execution Assessment
   - Summarize how much of the supplied regression scope was executed.
   - Report counts or percentages only when they can be calculated from the supplied test cases and statuses.

8. Regression Conclusion
   - State whether the supplied regression execution indicates that existing functionality remains stable.
   - Clearly identify limitations caused by failed, blocked, or not-executed cases.

Output using exactly this structure:

# Regression Testing Execution

## Regression Overview

## Regression Scope

## Regression Execution Results

## Regression Failures

## Defect Summary

## Blockers

## Coverage / Execution Assessment

## Regression Conclusion
```

---

## Expected Output

The output should answer:

- What change was being regression tested?
- What regression scope was covered?
- Which existing-functionality tests passed, failed, blocked, or were not executed?
- Were any regressions identified?
- What defects and blockers exist?
- How much of the supplied regression scope was actually executed?
- What is the overall regression conclusion?

---

## Scope Boundaries

### This prompt SHOULD:

- Evaluate supplied regression test cases.
- Validate existing functionality after a change.
- Record execution status.
- Identify observed regressions.
- Summarize defects and blockers.
- Calculate execution coverage when enough data is available.
- Provide a regression conclusion.

### This prompt SHOULD NOT:

- Create new regression tests.
- Decide regression strategy.
- Generate test data.
- Perform requirement gap analysis.
- Perform risk assessment.
- Recommend automation.
- Invent regression results.
- Assume that a failed test is caused by the latest change without evidence.
- Treat unexecuted tests as passed.

---

## Standard Input Contract

| Input | Purpose |
|---|---|
| `APP_OVERVIEW` | Provides application/product context |
| `EPIC_DESCRIPTION` | Provides broader feature context |
| `STORY_DESCRIPTION` | Provides story context |
| `CHANGE_DESCRIPTION` | Describes the change being validated |
| `REGRESSION_SCOPE` | Defines the supplied regression coverage |
| `REGRESSION_TEST_CASES` | Provides regression test cases |
| `TEST_DATA` | Provides required execution data |
| `TEST_ENVIRONMENT` | Identifies the execution environment |
| `EXECUTION_OBSERVATIONS` | Provides actual regression execution results |
| `EVIDENCE` | Provides execution evidence |
| `DEFECTS_FOUND` | Provides identified defects |

### Important

Regression execution validates existing functionality using the supplied regression coverage. Do not assume that unexecuted tests passed.
