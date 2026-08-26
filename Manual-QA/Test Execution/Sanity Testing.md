# Sanity Testing Prompt

## Purpose

Use this prompt to perform focused sanity test execution after a specific change, fix, enhancement, or impacted-area update.

The goal is to confirm that the targeted functionality and closely related behavior work as expected after the change.

The QA provides the change context, affected functionality, relevant test cases, test data, environment details, execution observations, and evidence.

The output must remain focused on the changed or impacted area and must not become a full regression assessment.

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

IMPACTED_AREA:

"""
{IMPACTED_AREA}
"""

SANITY_TEST_CASES:

"""
{SANITY_TEST_CASES}
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

You are a senior QA engineer responsible for sanity test execution.

Using the supplied requirement, change description, impacted area, sanity test cases, test data, environment, execution observations, evidence, and defects, evaluate whether the targeted functionality is behaving correctly after the change.

Sanity testing should remain focused on the changed functionality and its directly impacted behavior.

Execute/evaluate only the provided sanity test cases.

Do not create additional test cases or expand the assessment into a full regression suite.

Do not invent actual results, evidence, defects, or impacted functionality.

For each supplied test case, determine:

- PASS: The targeted behavior works as expected.
- FAIL: The observed behavior does not satisfy the expected result.
- BLOCKED: Execution cannot be completed because of a blocking issue.
- NOT EXECUTED: No execution information is available.

Analyze the information and provide:

1. Change Overview
   - Summarize what was changed, fixed, or enhanced.
   - Identify the impacted area.

2. Sanity Coverage
   - List the supplied sanity test cases and explain what changed behavior they validate.

3. Sanity Execution Results
   - Report test case ID, description, expected result, actual result/observation, and status.

4. Impacted Functionality Validation
   - Explain whether the targeted changed behavior works as expected.
   - Identify any directly impacted behavior that failed based on supplied evidence.

5. Defect Summary
   - Summarize defects identified during sanity execution.
   - Do not invent defect IDs, severity, or priority.

6. Blockers
   - List any issues preventing completion of sanity execution.

7. Sanity Conclusion
   - State whether the targeted change appears acceptable based on the supplied execution results.
   - Clearly identify failed, blocked, or not-executed cases.

Output using exactly this structure:

# Sanity Testing Execution

## Change Overview

## Sanity Coverage

## Sanity Execution Results

## Impacted Functionality Validation

## Defect Summary

## Blockers

## Sanity Conclusion
```

---

## Expected Output

The output should answer:

- What change was validated?
- Which impacted-area tests were executed?
- Did the changed functionality behave correctly?
- Were directly impacted behaviors affected?
- What defects or blockers were found?
- Is the change acceptable based on the supplied sanity results?

---

## Scope Boundaries

### This prompt SHOULD:

- Focus on a specific change or impacted area.
- Evaluate supplied sanity test cases.
- Compare actual behavior with expected behavior.
- Identify failures and blockers.
- Summarize defects.
- Provide a focused sanity conclusion.

### This prompt SHOULD NOT:

- Perform full regression testing.
- Create new test cases.
- Generate test data.
- Perform detailed requirement gap analysis.
- Assess unrelated application areas.
- Define test strategy.
- Recommend automation.
- Invent impacted functionality or execution results.

---

## Standard Input Contract

| Input | Purpose |
|---|---|
| `APP_OVERVIEW` | Provides application/product context |
| `EPIC_DESCRIPTION` | Provides feature context |
| `STORY_DESCRIPTION` | Provides story context |
| `CHANGE_DESCRIPTION` | Describes the fix, enhancement, or change |
| `IMPACTED_AREA` | Identifies the functionality affected by the change |
| `SANITY_TEST_CASES` | Provides focused sanity tests |
| `TEST_DATA` | Provides execution data |
| `TEST_ENVIRONMENT` | Identifies the execution environment |
| `EXECUTION_OBSERVATIONS` | Provides actual execution information |
| `EVIDENCE` | Provides execution evidence |
| `DEFECTS_FOUND` | Provides identified defects |

### Important

Sanity testing is focused validation of a change. Do not expand the execution into unrelated functionality or a complete regression suite.
