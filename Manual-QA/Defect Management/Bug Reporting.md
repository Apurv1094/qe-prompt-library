# Bug Reporting Prompt

## Purpose

Use this prompt to create a clear and actionable defect report from QA findings.

The report should explain **what went wrong, how to reproduce it, what was expected, and what actually happened**.

Do not guess the root cause or add information that is not provided.

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

ACCEPTANCE_CRITERIA:
"""
{ACCEPTANCE_CRITERIA}
"""

TEST_CASE_ID:
"""
{TEST_CASE_ID}
"""

TEST_CASE_DESCRIPTION:
"""
{TEST_CASE_DESCRIPTION}
"""

TEST_DATA:
"""
{TEST_DATA}
"""

TEST_ENVIRONMENT:
"""
{TEST_ENVIRONMENT}
"""

STEPS_PERFORMED:
"""
{STEPS_PERFORMED}
"""

EXPECTED_RESULT:
"""
{EXPECTED_RESULT}
"""

ACTUAL_RESULT:
"""
{ACTUAL_RESULT}
"""

EVIDENCE:
"""
{EVIDENCE}
"""

ADDITIONAL_OBSERVATIONS:
"""
{ADDITIONAL_OBSERVATIONS}
"""
```

## Prompt

```text
You are a senior QA engineer reporting a software defect.

Using the information provided, create a clear and developer-friendly defect report.

Keep the report factual and concise.

Do not:
- Guess the root cause.
- Invent defect IDs, severity, priority, evidence, or logs.
- Add steps or behavior that are not provided.
- Create test cases or test data.
- Include unnecessary sensitive data.

Analyze and provide:

1. Defect Title
   - Write a short title describing the issue and affected functionality.

2. Defect Summary
   - Briefly explain what is wrong.

3. Requirement / Acceptance Criteria Reference
   - Mention the requirement or acceptance criterion that is not met.

4. Preconditions
   - List any conditions required before reproducing the issue.

5. Steps to Reproduce
   - Provide clear numbered steps using the supplied information.

6. Expected Result
   - State what should happen.

7. Actual Result
   - State what actually happened.

8. Environment
   - Include relevant environment details such as browser, OS, version, device, etc.

9. Test Data
   - Include only relevant test data.

10. Evidence
   - Mention available screenshots, logs, videos, or other evidence.

11. Impact
   - Explain the user/business impact if it is clear from the input.
   - Otherwise write "Impact requires confirmation."

12. Severity / Priority
   - Use the provided values.
   - If not provided, write "Not provided."

13. Additional Observations
   - Include any useful factual observations.

Output exactly in this structure:

# Defect Report

## Defect Title

## Defect Summary

## Requirement / Acceptance Criteria Reference

## Preconditions

## Steps to Reproduce

## Expected Result

## Actual Result

## Environment

## Test Data

## Evidence

## Impact

## Severity / Priority

## Additional Observations
```

## Expected Output

The report should clearly answer:

- What is the defect?
- Which requirement is affected?
- How can it be reproduced?
- What was expected?
- What actually happened?
- Where was it found?
- What evidence is available?
- What is the impact?

## Scope Boundaries

### This prompt SHOULD:

- Create clear defect reports.
- Provide reproduction steps.
- Compare expected and actual behavior.
- Reference the affected requirement.
- Capture environment and evidence.
- Explain the impact when known.

### This prompt SHOULD NOT:

- Guess the root cause.
- Invent defect details or evidence.
- Create test cases.
- Create test data.
- Perform retesting or regression testing.
- Close or reopen defects.
- Include unnecessary sensitive information.

## Standard Input Contract

| Input | Purpose |
|---|---|
| `APP_OVERVIEW` | Application context |
| `EPIC_DESCRIPTION` | Business/feature context |
| `STORY_DESCRIPTION` | Requirement context |
| `ACCEPTANCE_CRITERIA` | Expected behavior |
| `TEST_CASE_ID` | Test case that found the issue |
| `TEST_CASE_DESCRIPTION` | Executed test description |
| `TEST_DATA` | Relevant test data |
| `TEST_ENVIRONMENT` | Execution environment |
| `STEPS_PERFORMED` | Reproduction steps |
| `EXPECTED_RESULT` | Expected behavior |
| `ACTUAL_RESULT` | Observed behavior |
| `EVIDENCE` | Supporting evidence |
| `ADDITIONAL_OBSERVATIONS` | Other useful observations |

# Example

## Example Input

```text
APP_OVERVIEW:
"""
E-commerce application where customers can manage orders.
"""

EPIC_DESCRIPTION:
"""
Order Management
"""

STORY_DESCRIPTION:
"""
Customer should be able to cancel an eligible order.
"""

ACCEPTANCE_CRITERIA:
"""
After cancellation, the order status should change from Confirmed
to Cancelled and a confirmation should be displayed.
"""

TEST_CASE_ID:
"""
TC-ORD-015
"""

TEST_CASE_DESCRIPTION:
"""
Verify cancellation of a confirmed order.
"""

TEST_DATA:
"""
Order ID: ORD-10025
Status: Confirmed
"""

TEST_ENVIRONMENT:
"""
QA Environment
Chrome 151
Windows 11
Application Version 2.5.0
"""

STEPS_PERFORMED:
"""
1. Login as a customer.
2. Open Order History.
3. Open ORD-10025.
4. Click Cancel Order.
5. Confirm cancellation.
"""

EXPECTED_RESULT:
"""
Order status should change to Cancelled and a confirmation should be displayed.
"""

ACTUAL_RESULT:
"""
Cancellation confirmation is displayed, but the order status remains Confirmed.
"""

EVIDENCE:
"""
Screenshot showing Confirmed status after cancellation.
"""

ADDITIONAL_OBSERVATIONS:
"""
Issue reproduced twice.
"""
```

---

## Example Output

```markdown
# Defect Report

## Defect Title

Order status remains Confirmed after cancellation

## Defect Summary

After cancelling an eligible order, the cancellation confirmation is displayed, but the order status remains Confirmed.

## Requirement / Acceptance Criteria Reference

The acceptance criteria requires the order status to change from Confirmed to Cancelled after cancellation.

## Preconditions

- Customer is logged in.
- An eligible Confirmed order is available.

## Steps to Reproduce

1. Login as a customer.
2. Open Order History.
3. Open order ORD-10025.
4. Click Cancel Order.
5. Confirm cancellation.
6. Check the order status.

## Expected Result

Order status should change to Cancelled and a cancellation confirmation should be displayed.

## Actual Result

Cancellation confirmation is displayed, but the order status remains Confirmed.

## Environment

- QA Environment
- Chrome 151
- Windows 11
- Application Version 2.5.0

## Test Data

- Order ID: ORD-10025
- Initial Status: Confirmed

## Evidence

Screenshot showing Confirmed status after cancellation.

## Impact

The customer sees an incorrect order status after cancellation.

## Severity / Priority

Not provided.

## Additional Observations

Issue was reproduced twice.
```

---

## Important

Keep the defect report focused on the **observed problem**.

**Correct:**  
`Order status remains Confirmed after cancellation.`

**Avoid:**  
`Database update API is failing because the transaction is not committed.`

Only mention a root cause when it is supported by logs or technical investigation.