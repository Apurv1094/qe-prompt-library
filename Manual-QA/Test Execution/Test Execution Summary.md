# Test Execution Summary Prompt

## Purpose

Use this prompt to consolidate the results of Functional Testing, Smoke Testing, Sanity Testing, and Regression Testing into one clear QA execution summary.

The purpose of this prompt is to provide the final execution picture after the individual test execution activities are completed.

It must use the execution results provided by QA as the source of truth. It must not create new test cases, invent execution results, or declare missing tests as passed.

---

## Input

```text

APP_OVERVIEW:

"""
{APP_OVERVIEW}
"""

RELEASE_VERSION:

"""
{RELEASE_VERSION}
"""

TEST_ENVIRONMENT:

"""
{TEST_ENVIRONMENT}
"""

FUNCTIONAL_TESTING_RESULTS:

"""
{FUNCTIONAL_TESTING_RESULTS}
"""

SMOKE_TESTING_RESULTS:

"""
{SMOKE_TESTING_RESULTS}
"""

SANITY_TESTING_RESULTS:

"""
{SANITY_TESTING_RESULTS}
"""

REGRESSION_TESTING_RESULTS:

"""
{REGRESSION_TESTING_RESULTS}
"""

DEFECT_SUMMARY:

"""
{DEFECT_SUMMARY}
"""

BLOCKERS:

"""
{BLOCKERS}
"""

EVIDENCE_SUMMARY:

"""
{EVIDENCE_SUMMARY}
"""

EXECUTION_NOTES:

"""
{EXECUTION_NOTES}
"""
```

---

## Prompt

```text

You are a senior QA engineer responsible for preparing the final Test Execution Summary.

The individual test execution activities have already been performed.

Using the Functional Testing, Smoke Testing, Sanity Testing, and Regression Testing results provided below, consolidate the results into one accurate and structured QA execution summary.

The individual execution results are the source of truth.

Do not create new test cases.
Do not create new test scenarios.
Do not invent test results.
Do not assume that missing execution information means PASS.
Do not invent defect IDs, severity, priority, blockers, or evidence.
Do not modify the status of any supplied test case.

For each testing category:

1. Functional Testing
   - Summarize total test cases when available.
   - Summarize PASS, FAIL, BLOCKED, and NOT EXECUTED.
   - Highlight important functional failures.

2. Smoke Testing
   - Summarize critical smoke execution.
   - State whether critical functionality passed, failed, or was blocked.
   - Assess build stability only from supplied results.

3. Sanity Testing
   - Summarize validation of the changed/fixed functionality.
   - Highlight failures or blockers in the impacted area.

4. Regression Testing
   - Summarize regression execution.
   - Identify regressions, failures, blocked cases, and incomplete coverage.
   - Do not claim that a failure is caused by the latest change unless the supplied information establishes that relationship.

Then provide:

5. Overall Execution Metrics
   - Calculate total test cases across categories only when the individual results provide reliable counts.
   - Calculate total PASS, FAIL, BLOCKED, and NOT EXECUTED.
   - Calculate execution percentage and pass percentage only when the required numbers are available.
   - Clearly state when a metric cannot be calculated.

6. Defect Summary
   - Consolidate supplied defects.
   - Group or summarize by severity/priority only when provided.
   - Do not invent defect classifications.

7. Blocker Summary
   - Consolidate execution blockers.
   - Explain their impact on execution completion.

8. Key Observations
   - Highlight the most important QA findings.
   - Keep observations factual and traceable to supplied execution results.

9. Overall QA Execution Conclusion
   - State whether execution is complete, partially complete, or incomplete.
   - State whether major failures or blockers remain.
   - Do not declare the release defect-free unless explicitly supported by the inputs.
   - Do not give a release sign-off unless the supplied information supports it.

10. Recommended Next Action
   - Recommend only actions justified by the supplied execution results.
   - Examples:
     * Re-test failed defects after fixes.
     * Execute blocked test cases after blocker resolution.
     * Complete pending regression cases.
     * Review QA sign-off criteria.
     * Proceed to the next release stage if all supplied criteria are satisfied.

Output using exactly this structure:

# Test Execution Summary

## Execution Overview

## Execution Status Summary

## Overall Execution Metrics

## Defect Summary

## Blocker Summary

## Coverage / Completion Assessment

## Key Observations

## Overall QA Execution Conclusion

## Recommended Next Action
```

---

## Expected Output

The output should provide one consolidated view of the complete test execution.

It should answer:

- What build/release was tested?
- Which testing activities were completed?
- How many tests passed, failed, were blocked, or were not executed?
- What was the overall execution completion?
- What defects were identified?
- What blockers remain?
- Were any important regressions or functional failures found?
- Is testing complete?
- What should happen next?

---

## Scope Boundaries

### This prompt SHOULD:

- Consolidate Functional, Smoke, Sanity, and Regression execution results.
- Calculate reliable execution metrics.
- Summarize defects and blockers.
- Identify incomplete execution.
- Highlight important QA observations.
- Provide an overall execution conclusion.
- Recommend the next logical action based on supplied results.

### This prompt SHOULD NOT:

- Create test cases.
- Create test scenarios.
- Generate test data.
- Execute tests itself.
- Invent missing results.
- Treat NOT EXECUTED as PASS.
- Perform requirement gap analysis.
- Perform risk assessment.
- Define test strategy.
- Decide manual vs automation.
- Replace detailed test execution reports.

---

## Standard Input Contract

| Input | Purpose |
|---|---|
| `APP_OVERVIEW` | Provides application/product context |
| `RELEASE_VERSION` | Identifies the build/release |
| `TEST_ENVIRONMENT` | Identifies the execution environment |
| `FUNCTIONAL_TESTING_RESULTS` | Results from Functional Testing |
| `SMOKE_TESTING_RESULTS` | Results from Smoke Testing |
| `SANITY_TESTING_RESULTS` | Results from Sanity Testing |
| `REGRESSION_TESTING_RESULTS` | Results from Regression Testing |
| `DEFECT_SUMMARY` | Consolidated defect information |
| `BLOCKERS` | Execution blockers |
| `EVIDENCE_SUMMARY` | Available execution evidence |
| `EXECUTION_NOTES` | Additional execution context |

---

# Example

## Example Input

```text
APP_OVERVIEW:

"""
E-commerce web application used by customers to browse products,
add products to cart, place orders, and view order history.
"""

RELEASE_VERSION:

"""
Release 2.5.0
"""

TEST_ENVIRONMENT:

"""
QA Environment
Chrome 151
Windows 11
"""

FUNCTIONAL_TESTING_RESULTS:

"""
Total: 20
PASS: 18
FAIL: 1
BLOCKED: 1
NOT EXECUTED: 0

Failed:
TC-FUN-015 - Order cancellation does not update the order status correctly.

Blocked:
TC-FUN-018 - Payment refund validation could not be completed because the payment gateway was unavailable.
"""

SMOKE_TESTING_RESULTS:

"""
Total: 5
PASS: 5
FAIL: 0
BLOCKED: 0
NOT EXECUTED: 0

All critical application flows are working.
"""

SANITY_TESTING_RESULTS:

"""
Total: 6
PASS: 5
FAIL: 1
BLOCKED: 0
NOT EXECUTED: 0

Failed:
TC-SAN-004 - Updated order cancellation flow still shows the previous status after cancellation.
"""

REGRESSION_TESTING_RESULTS:

"""
Total: 30
PASS: 28
FAIL: 1
BLOCKED: 1
NOT EXECUTED: 0

Failed:
TC-REG-021 - Order history displays incorrect status after cancellation.

Blocked:
TC-REG-029 - Refund validation blocked because payment gateway is unavailable.
"""

DEFECT_SUMMARY:

"""
DEF-102 - Order cancellation status not updated correctly - High
DEF-103 - Refund validation unavailable due to payment gateway dependency - Medium
"""

BLOCKERS:

"""
Payment gateway unavailable for refund validation.
This blocked 1 functional test and 1 regression test.
"""

EVIDENCE_SUMMARY:

"""
Screenshots attached for failed order cancellation scenarios.
Execution logs available for smoke testing.
"""

EXECUTION_NOTES:

"""
Smoke testing passed completely.
Order cancellation functionality has unresolved failures.
Refund validation is incomplete due to an external dependency.
"""
```

---

## Example Output

```markdown
# Test Execution Summary

## Execution Overview

Release 2.5.0 was tested in the QA environment across Functional, Smoke, Sanity, and Regression Testing.

A total of 61 test cases were evaluated across the four testing activities.

Smoke testing completed successfully. Functional, Sanity, and Regression Testing identified issues related to the order cancellation flow. Refund validation remained partially blocked because the payment gateway was unavailable.

## Execution Status Summary

| Testing Type | Total | PASS | FAIL | BLOCKED | NOT EXECUTED |
|---|---:|---:|---:|---:|---:|
| Functional Testing | 20 | 18 | 1 | 1 | 0 |
| Smoke Testing | 5 | 5 | 0 | 0 | 0 |
| Sanity Testing | 6 | 5 | 1 | 0 | 0 |
| Regression Testing | 30 | 28 | 1 | 1 | 0 |
| **Total** | **61** | **56** | **3** | **2** | **0** |

## Overall Execution Metrics

- Total Test Cases: 61
- Passed: 56
- Failed: 3
- Blocked: 2
- Not Executed: 0
- Execution Completion: 100%
- Pass Rate: 91.8%

The execution completion is 100% because all supplied test cases have an execution status. However, this does not mean that all functionality passed.

## Defect Summary

| Defect | Description | Severity |
|---|---|---|
| DEF-102 | Order cancellation status is not updated correctly | High |
| DEF-103 | Refund validation is unavailable because of payment gateway dependency | Medium |

The order cancellation issue appears in Functional, Sanity, and Regression execution results.

## Blocker Summary

The payment gateway was unavailable during execution.

Impact:
- 1 Functional Testing case blocked.
- 1 Regression Testing case blocked.
- Refund validation could not be fully verified.

## Coverage / Completion Assessment

All 61 supplied test cases have an execution status.

However, 2 test cases remain blocked and 3 test cases have failed.

Therefore, execution is complete from a status-recording perspective, but the overall validation is not fully successful.

## Key Observations

1. Smoke Testing passed all critical flows.
2. Order cancellation has unresolved failures across Functional, Sanity, and Regression Testing.
3. Refund validation could not be completed because of the payment gateway dependency.
4. The order cancellation issue represents the primary functional concern for this release.
5. No test cases were marked NOT EXECUTED.

## Overall QA Execution Conclusion

Test execution for Release 2.5.0 is complete based on the supplied test case statuses, but the results are not fully satisfactory.

Smoke Testing passed successfully, indicating that the critical application flows are available.

However, the order cancellation functionality has unresolved failures, and refund validation remains blocked by an external payment gateway dependency.

Based on the supplied results, QA should not consider the execution fully successful until the failed functionality is fixed and the blocked refund validation is completed.

## Recommended Next Action

1. Fix DEF-102 and re-execute the affected Functional, Sanity, and Regression test cases.
2. Restore the payment gateway dependency and re-execute the blocked refund validation cases.
3. Review the updated results after re-execution before considering QA completion.
```

---

## Important Rule

The **Test Execution Summary** should consume the outputs of the four execution modules:

```text
Functional Testing Results
          +
Smoke Testing Results
          +
Sanity Testing Results
          +
Regression Testing Results
          ↓
   Test Execution Summary
          ↓
 Overall QA Execution Status
```

The summary should **never invent missing data** and should clearly distinguish between **PASS, FAIL, BLOCKED, and NOT EXECUTED**.
