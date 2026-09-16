# Log Analysis Prompt

## Purpose

Use this prompt to analyze application logs and identify useful information related to a test failure, error, or unexpected behavior.

## QA Inputs

- Application / Module
- Requirement / Story
- Test Case ID
- Test Scenario
- Environment / Build
- Timestamp
- Log Type
- Log Content
- Error Message
- Expected vs Actual Result
- Additional Observations

## Prompt

Act as a Senior QA Engineer and analyze the provided logs.

Your analysis should:

1. Summarize the important log events.
2. Identify errors, warnings, exceptions, and failures.
3. Correlate the logs with the reported test failure or behavior.
4. Identify the likely failure area or component.
5. Highlight relevant timestamps, error messages, request/response details, or transaction flow.
6. Separate confirmed facts from assumptions.
7. Suggest the next investigation or QA action.
8. Do not invent missing log details or claim a root cause without evidence.

Keep the analysis clear, concise, and easy for QA, developers, BA, and Product Owners to understand.

## Input

APP_MODULE:
REQUIREMENT:
TEST_CASE_ID:
TEST_SCENARIO:
ENVIRONMENT_BUILD:
TIMESTAMP:
LOG_TYPE:
LOG_CONTENT:
ERROR_MESSAGE:
EXPECTED_RESULT:
ACTUAL_RESULT:
ADDITIONAL_OBSERVATIONS:

## Expected Output

### Log Summary
Briefly summarize the relevant log activity.

### Key Findings
List important errors, warnings, exceptions, or events.

### Failure Correlation
Explain how the logs relate to the reported issue.

### Suspected Area
Identify the affected component, service, API, database, or process if supported by the logs.

### Evidence
Mention the exact log details supporting the analysis.

### Root Cause Status
- Confirmed
- Likely
- Not Determined

### Recommended Action
Mention the next step for QA / Development.

### Additional Checks
List any logs, APIs, services, data, or environment details that should be checked next.
