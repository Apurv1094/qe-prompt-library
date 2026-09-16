# Test Failure Analysis Prompt

## Purpose

Use this prompt to analyze a failed test case and identify the most likely reason for the failure.

## QA Inputs

- Application / Module
- Requirement / Story
- Test Case ID
- Test Case Description
- Expected

 Result
- Actual Result
- Test Data
- Environment / Build
- Error Message / Logs
- Evidence / Screenshots
- Additional Observations

## Prompt

Act as a Senior QA Engineer and analyze the failed test case using the information provided.

Your analysis should:

1. Summarize what failed.
2. Compare the expected and actual results.
3. Identify the most likely failure category:
   - Application Defect
   - Test Data Issue
   - Environment Issue
   - Configuration Issue
   - Test Case Issue
   - Automation / Scripting Issue
   - Requirement / Specification Issue
4. Explain the reasoning based only on the available information.
5. Mention the evidence supporting the conclusion.
6. Recommend the next action for QA.
7. If a defect is likely, state whether it should be raised or needs further investigation.
8. Do not invent root causes, logs, or missing information.

Keep the analysis clear, concise, and easy for QA, developers, BA, and Product Owners to understand.

## Input

APP_MODULE:
REQUIREMENT:
TEST_CASE_ID:
TEST_CASE_DESCRIPTION:
EXPECTED_RESULT:
ACTUAL_RESULT:
TEST_DATA:
ENVIRONMENT_BUILD:
ERROR_LOG:
EVIDENCE:
ADDITIONAL_OBSERVATIONS:

## Expected Output

### Failure Summary
Briefly explain what failed.

### Expected vs Actual
- Expected:
- Actual:

### Failure Category
Select the most appropriate category.

### Analysis
Explain the likely reason for the failure.

### Evidence
List the supporting evidence.

### Recommended Action
Mention the next action QA should take.

### Defect Recommendation
- Raise Defect: Yes / No / Need More Investigation
- Reason:
