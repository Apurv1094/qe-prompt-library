# Smoke Testing Prompt

## Purpose

Use this prompt to perform a focused smoke test execution after a new build, deployment, release, or environment change.

The goal is to determine whether the build is stable enough for further testing.

The QA provides application context, build information, critical smoke test cases, environment details, execution observations, and evidence.

The output must focus on critical build health and must not expand into full functional or regression testing.

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

BUILD_VERSION:

"""
{BUILD_VERSION}
"""

DEPLOYMENT_DETAILS:

"""
{DEPLOYMENT_DETAILS}
"""

SMOKE_TEST_CASES:

"""
{SMOKE_TEST_CASES}
"""

TEST_ENVIRONMENT:

"""
{TEST_ENVIRONMENT}
"""

TEST_DATA:

"""
{TEST_DATA}
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

You are a senior QA engineer responsible for smoke test execution.

Using the information provided below, evaluate the critical smoke test cases for the specified build and environment.

The purpose of smoke testing is to determine whether the build is sufficiently stable to proceed with further testing.

Execute/evaluate only the provided smoke test cases.

Do not create additional smoke tests, functional tests, or regression tests.

Do not invent execution results, defects, evidence, or system behavior.

For each smoke test case, determine:

- PASS: Critical functionality works as expected.
- FAIL: A critical expected behavior does not work.
- BLOCKED: Execution cannot proceed because of a blocking dependency, environment, access, or data issue.
- NOT EXECUTED: No execution information is available.

Analyze the information and provide:

1. Build & Environment Overview
   - Identify the build/version and environment used.
   - Summarize the deployment context.

2. Critical Smoke Coverage
   - List the supplied smoke test cases and the critical functionality they validate.

3. Smoke Execution Results
   - Report each test case with ID, description, expected result, actual result/observation, and status.

4. Critical Failures / Blockers
   - Identify failures or blockers that could prevent further testing.
   - Explain their impact based only on the supplied information.

5. Defect Summary
   - Summarize provided defects associated with smoke execution.
   - Do not invent defect IDs or severity.

6. Build Stability Assessment
   - Determine whether the build appears stable enough for further testing based on the supplied smoke results.
   - If critical tests are failed or blocked, clearly state the impact.

7. Execution Conclusion
   - Provide a concise smoke testing conclusion.

Output using exactly this structure:

# Smoke Testing Execution

## Build & Environment Overview

## Critical Smoke Coverage

## Smoke Execution Results

## Critical Failures / Blockers

## Defect Summary

## Build Stability Assessment

## Execution Conclusion
```

---

## Expected Output

The output should answer:

- Which build was tested?
- Which critical smoke tests were executed?
- Did the critical functionality work?
- Are there failures or blockers that prevent further testing?
- Are the supplied results sufficient to consider the build stable for the next QA phase?

---

## Scope Boundaries

### This prompt SHOULD:

- Focus on critical build validation.
- Evaluate supplied smoke test cases.
- Identify build-blocking failures.
- Record execution status.
- Summarize defects and blockers.
- Provide a build stability conclusion.

### This prompt SHOULD NOT:

- Perform full functional testing.
- Perform complete regression testing.
- Create new test cases.
- Create test data.
- Perform detailed requirement gap analysis.
- Define test strategy.
- Recommend automation.
- Invent results or defects.
- Treat smoke testing as a replacement for functional or regression testing.

---

## Standard Input Contract

| Input | Purpose |
|---|---|
| `APP_OVERVIEW` | Provides application/product context |
| `EPIC_DESCRIPTION` | Provides feature context |
| `STORY_DESCRIPTION` | Provides story context |
| `BUILD_VERSION` | Identifies the build/release being validated |
| `DEPLOYMENT_DETAILS` | Provides deployment/release information |
| `SMOKE_TEST_CASES` | Provides critical smoke tests |
| `TEST_ENVIRONMENT` | Identifies the execution environment |
| `TEST_DATA` | Provides required execution data |
| `EXECUTION_OBSERVATIONS` | Provides actual smoke execution results |
| `EVIDENCE` | Provides execution evidence |
| `DEFECTS_FOUND` | Provides identified defects |

### Important

Smoke testing is a build-health check. Keep the evaluation focused on critical functionality and readiness for further testing.
