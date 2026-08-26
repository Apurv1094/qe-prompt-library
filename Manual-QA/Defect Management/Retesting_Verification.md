# Retesting / Verification Prompt

## Purpose

Use this prompt to verify a previously reported defect after a fix or new build is available.

The goal is to confirm whether the original issue is fixed based on actual retest results and evidence.

Do not assume the defect is fixed just because a new build is available.

## Input

```text
APP_OVERVIEW:
"""
{APP_OVERVIEW}
"""

DEFECT_ID:
"""
{DEFECT_ID}
"""

DEFECT_TITLE:
"""
{DEFECT_TITLE}
"""

ORIGINAL_DEFECT_DESCRIPTION:
"""
{ORIGINAL_DEFECT_DESCRIPTION}
"""

ORIGINAL_EXPECTED_RESULT:
"""
{ORIGINAL_EXPECTED_RESULT}
"""

FIX_DESCRIPTION:
"""
{FIX_DESCRIPTION}
"""

BUILD_VERSION:
"""
{BUILD_VERSION}
"""

TEST_ENVIRONMENT:
"""
{TEST_ENVIRONMENT}
"""

TEST_DATA:
"""
{TEST_DATA}
"""

RETEST_STEPS:
"""
{RETEST_STEPS}
"""

RETEST_OBSERVATION:
"""
{RETEST_OBSERVATION}
"""

RETEST_EVIDENCE:
"""
{RETEST_EVIDENCE}
"""

ADDITIONAL_OBSERVATIONS:
"""
{ADDITIONAL_OBSERVATIONS}
"""
```
## Prompt

```text
You are a senior QA engineer performing defect retesting.

Review the original defect and the current retest results to determine whether the issue is fixed.

Compare the original expected behavior with the actual retest result.

Do not:
- Assume the defect is fixed without evidence.
- Invent test results or evidence.
- Create a new defect automatically.
- Guess the root cause.

Set the retest status as one of:

- VERIFIED / PASS — Issue is fixed and expected behavior works.
- FAILED / NOT FIXED — Original issue still occurs.
- BLOCKED — Retesting could not be completed due to a blocker.
- NOT EXECUTED — No retest result is available.

Also mention any related or regression observation if provided.

Output exactly:

# Retesting / Verification

## Defect Verification Overview

## Original Defect

## Retest Execution

## Expected vs Actual

## Evidence

## Retest Status

## Related / Regression Observation

## Verification Conclusion

## Recommended Next Action
```

## Expected Output

The result should clearly show:

- Which defect was retested?
- What was the original issue?
- What should happen?
- What happened after the fix?
- Is the issue fixed?
- What evidence supports the result?
- Is there any related issue?
- What should QA do next?

## Scope Boundaries

### Should

- Verify the original defect.
- Compare expected and actual behavior.
- Review retest evidence.
- Set the correct retest status.
- Mention related observations.
- Suggest the next QA action.

### Should Not

- Guess the root cause.
- Invent results or evidence.
- Create new test cases.
- Perform full regression testing.
- Automatically create a new defect.
- Close a defect without sufficient evidence.

## Standard Input Contract

| Input | Purpose |
|---|---|
| `APP_OVERVIEW` | Application context |
| `DEFECT_ID` | Defect being retested |
| `DEFECT_TITLE` | Original defect title |
| `ORIGINAL_DEFECT_DESCRIPTION` | Original issue |
| `ORIGINAL_EXPECTED_RESULT` | Expected behavior |
| `FIX_DESCRIPTION` | Fix/change provided |
| `BUILD_VERSION` | Build being tested |
| `TEST_ENVIRONMENT` | Retest environment |
| `TEST_DATA` | Data used for retest |
| `RETEST_STEPS` | Steps performed |
| `RETEST_OBSERVATION` | Current result |
| `RETEST_EVIDENCE` | Supporting evidence |
| `ADDITIONAL_OBSERVATIONS` | Other useful findings |

# Example

## Example Input

```text
DEFECT_ID:
"""
DEF-102
"""

DEFECT_TITLE:
"""
Order status remains Confirmed after cancellation
"""

ORIGINAL_DEFECT_DESCRIPTION:
"""
Order status remained Confirmed after cancellation.
"""

ORIGINAL_EXPECTED_RESULT:
"""
Order status should change to Cancelled.
"""

FIX_DESCRIPTION:
"""
Updated order cancellation status handling.
"""

BUILD_VERSION:
"""
2.5.1
"""

TEST_ENVIRONMENT:
"""
QA Environment
Chrome 151
Windows 11
"""

TEST_DATA:
"""
Order ID: ORD-10025
"""

RETEST_STEPS:
"""
1. Login.
2. Open Order History.
3. Open ORD-10025.
4. Cancel the order.
5. Confirm cancellation.
6. Check order status.
"""

RETEST_OBSERVATION:
"""
Order status changed to Cancelled after cancellation.
"""

RETEST_EVIDENCE:
"""
Screenshot showing Cancelled status.
"""

ADDITIONAL_OBSERVATIONS:
"""
Issue was not reproduced during retest.
"""

## Example Output

# Retesting / Verification

## Defect Verification Overview

DEF-102 was retested on build 2.5.1 in the QA environment.

## Original Defect

Order status remained Confirmed after cancellation.

Expected behavior: Status should change to Cancelled.

## Retest Execution

The cancellation flow was executed using order ORD-10025.

## Expected vs Actual

| | Result |
|---|---|
| Expected | Status changes to Cancelled |
| Actual | Status changed to Cancelled |

## Evidence

Screenshot showing the order status as Cancelled.

## Retest Status

**VERIFIED / PASS**

The original issue was not reproduced.

## Related / Regression Observation

No related issue was observed.

## Verification Conclusion

DEF-102 is verified as fixed based on the retest result and available evidence.

## Recommended Next Action

Update the defect as verified/closed according to the team's defect workflow.

## Simple Flow

Original Defect
      ↓
Fix / New Build
      ↓
Retest
      ↓
Expected vs Actual
      ↓
Evidence
      ↓
PASS / FAILED / BLOCKED / NOT EXECUTED
```
