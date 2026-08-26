# Functional Testing Prompt

## Purpose

Use this prompt to execute and evaluate functional test cases against the implemented feature.

The QA provides the requirement context, acceptance criteria, test cases, test data, environment details, and execution results or observations.

The output should determine whether the implemented functionality behaves as expected for the defined functional test cases. It must not create new test cases or perform unrelated requirement analysis.

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

ACCEPTANCE_CRITERIA:

"""
{ACCEPTANCE_CRITERIA}
"""

TEST_CASES:

"""
{TEST_CASES}
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


Using the requirement context, acceptance criteria, existing test cases, test data, environment details, execution observations, evidence, and defects provided below, evaluate the functional behavior of the feature.

Execute/evaluate only the provided functional test cases.

Do not create new test cases or test scenarios.

Do not invent execution results, evidence, defects, or expected behavior that is not supported by the provided inputs.

For each test case, determine the execution status based on the available information:

- PASS: Actual behavior satisfies the expected result.
- FAIL: Actual behavior does not satisfy the expected result.
- BLOCKED: Execution cannot be completed because of an environment, dependency, data, access, or other blocking issue.
- NOT EXECUTED: No execution information is available.

When a test fails, identify the observed behavior and the requirement or expected result that it violates.

When a test is blocked, identify the blocking reason if provided.

Analyze the information together and provide:

1. Execution Overview
   - Summarize the functional execution performed.
   - Mention the feature/area covered.

2. Test Case Execution Results
   - Evaluate every provided test case.
   - Include Test Case ID, Test Case Description, Expected Result, Actual Result/Observation, Status, and Defect Reference where available.

3. Requirement / Acceptance Criteria Validation
   - Map observed functional behavior to the relevant acceptance criteria.
   - Identify any acceptance criterion that is not satisfied.

4. Defect Summary
   - Summarize defects identified during execution.
   - Use only defects explicitly provided or directly evidenced by the execution information.
   - Do not invent defect IDs.

5. Blockers
   - List execution blockers and their impact.
   - If none are provided, state that no blockers were identified from the supplied execution information.

6. Evidence Summary
   - Reference the supplied evidence where available.
   - Do not invent evidence links or attachments.

7. Execution Conclusion
   - State whether the functional execution can be considered successful based on the supplied results.
   - Clearly mention any failed, blocked, or not-executed test cases.

Output using exactly this structure:

# Functional Testing Execution

## Execution Overview

## Test Case Execution Results

## Requirement / Acceptance Criteria Validation

## Defect Summary

## Blockers

## Evidence Summary

## Execution Conclusion


## Expected Output

The output should provide a clear record of functional test execution and answer:

- Which functional test cases were executed?
- Which test cases passed, failed, were blocked, or were not executed?
- Does the observed behavior satisfy the acceptance criteria?
- What defects were identified?
- What execution blockers exist?
- What evidence supports the execution result?
- What is the overall functional execution conclusion?



## Scope Boundaries

### This prompt SHOULD:

- Evaluate provided functional test cases.
- Compare actual behavior with expected results.
- Validate implemented behavior against acceptance criteria.
- Record execution status.
- Summarize defects, blockers, and evidence.
- Provide an execution conclusion.

### This prompt SHOULD NOT:

- Create new test cases.
- Create new test scenarios.
- Generate test data.
- Perform detailed requirement gap analysis.
- Perform risk assessment.
- Define test strategy.
- Recommend automation.
- Create regression suites.
- Invent defects or execution results.
- Modify the expected behavior defined by the requirement.


## Standard Input Contract

| Input | Purpose |
|---|---|
| `APP_OVERVIEW` | Provides high-level application/product context |
| `EPIC_DESCRIPTION` | Provides broader business and feature context |
| `STORY_DESCRIPTION` | Defines the specific functionality under test |
| `ACCEPTANCE_CRITERIA` | Defines conditions that must be satisfied |
| `TEST_CASES` | Provides the functional test cases to execute |
| `TEST_DATA` | Provides data required for execution |
| `TEST_ENVIRONMENT` | Defines the environment/build/configuration used |
| `EXECUTION_OBSERVATIONS` | Provides actual execution observations/results |
| `EVIDENCE` | Provides screenshots, logs, videos, or other execution evidence |
| `DEFECTS_FOUND` | Provides defects identified during execution |

### Important

The prompt evaluates the supplied test cases and execution information. It must never fabricate execution results when actual execution information is missing.
