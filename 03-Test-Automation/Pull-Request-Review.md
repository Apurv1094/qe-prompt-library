# Automation PR Review

## Purpose
Review automation pull requests submitted by QE Automation Engineers to identify code quality issues, framework design violations, test reliability risks, missing test coverage, and CI/CD integration concerns before merging.

## When to Use
Use this prompt when reviewing a pull request containing new or modified UI automation, API automation, test utilities, framework configurations, test data, or CI/CD pipeline changes.

## Inputs Required

- `{{PR_DETAILS}}` — **Required:** PR title, description, source and target branches, and the purpose of the changes.
- `{{PR_CODE_CHANGES}}` — **Required:** PR diff, changed files, or accessible repository/PR link containing the proposed changes.
- `{{AUTOMATION_FRAMEWORK}}` — **Required:** Automation technology stack, such as Playwright with TypeScript, Selenium with Java, or Rest Assured with TestNG.
- `{{FRAMEWORK_STANDARDS}}` — **Optional:** Existing coding conventions, framework architecture, reusable utilities, and automation best practices followed by the team.
- `{{TEST_REQUIREMENTS}}` — **Optional:** User stories, acceptance criteria, or test scenarios associated with the PR.
- `{{EXECUTION_RESULTS}}` — **Optional:** CI build results, automated test execution reports, failure logs, or other validation evidence.

## Prompt

```text
Role: 
Act as a Senior QA Automation Architect with 10+ years of
industry experience designing, developing, maintaining,
and reviewing enterprise-level test automation frameworks.

Task:
Perform a comprehensive technical review of the submitted
automation pull request from the perspective of an experienced
QA Automation Architect.

Evaluate whether the proposed changes follow automation
engineering best practices, align with the existing framework,
provide reliable test coverage, and are maintainable for
long-term use.

Inputs:

PR_DETAILS:
{{PR_DETAILS}}

PR_CODE_CHANGES:
{{PR_CODE_CHANGES}}

AUTOMATION_FRAMEWORK:
{{AUTOMATION_FRAMEWORK}}

FRAMEWORK_STANDARDS:
{{FRAMEWORK_STANDARDS}}

TEST_REQUIREMENTS:
{{TEST_REQUIREMENTS}}

EXECUTION_RESULTS:
{{EXECUTION_RESULTS}}

Review Areas:

1. Code Quality and Maintainability
- Identify duplicated code and unnecessary complexity.
- Review naming conventions and code readability.
- Identify unused imports, variables, and methods.
- Evaluate method responsibilities and modularity.
- Recommend reusable methods where appropriate.

2. Framework Architecture and Reusability
- Verify alignment with existing framework architecture.
- Check whether existing utilities are reused.
- Identify unnecessary custom implementations.
- Review separation of test logic, test data, and utilities.
- Evaluate Page Object Model or equivalent design patterns
  where applicable.
- Identify unnecessary dependencies or configuration changes.

3. Test Reliability and Flakiness
- Identify hardcoded waits and unnecessary sleeps.
- Review locator stability and synchronization strategies.
- Check appropriate use of assertions and auto-waiting.
- Identify race conditions and timing dependencies.
- Verify test independence and isolation.
- Check shared state, execution order dependencies,
  and potential parallel execution issues.
- Identify retries that may conceal genuine failures.

4. Test Coverage and Assertions
- Verify that automated tests cover the intended requirements.
- Review positive, negative, and boundary scenarios
  where applicable.
- Identify missing or weak assertions.
- Check that assertions validate actual business behavior.
- Identify redundant tests and coverage gaps.
- Verify requirement-to-test traceability when available.

5. Test Data and Environment Management
- Identify hardcoded environment-specific values.
- Review test data creation, cleanup, and reuse.
- Verify environment configuration handling.
- Check handling of credentials and sensitive information.
- Identify dependencies on unstable external systems.

6. UI Automation Review (if applicable)
- Evaluate locator strategies and selector stability.
- Review Page Object or component abstraction.
- Check navigation and synchronization handling.
- Identify unnecessary direct DOM interactions.
- Review browser and viewport assumptions.

7. API Automation Review (if applicable)
- Review request and response validation.
- Check HTTP status, response body, header, and schema assertions.
- Verify authentication and authorization handling.
- Review API client and request specification reuse.
- Check negative scenarios and error handling.
- Identify hardcoded tokens and endpoint dependencies.

8. CI/CD and Execution Readiness
- Verify compatibility with existing CI/CD pipelines.
- Review execution parameters and environment selection.
- Check reporting, logging, and failure diagnostics.
- Identify parallel execution and resource risks.
- Evaluate test tagging, grouping, and execution efficiency.
- Check whether new dependencies or configuration changes
  are justified.

9. Security and Engineering Practices
- Identify exposed secrets or sensitive test data.
- Review dependency changes for potential risks.
- Check that logs do not expose confidential information.
- Identify unsafe test operations or destructive behavior.

Rules:
- Review only the provided or accessible PR changes and
  relevant framework context.
- Do not invent defects or assume missing code is incorrect.
- Inspect surrounding framework code when accessible before
  recommending architectural changes.
- Prioritize correctness, reliability, maintainability,
  and framework consistency over stylistic preferences.
- Distinguish confirmed issues from potential risks.
- Every confirmed finding must reference a file and line
  number or identifiable code snippet.
- Explain why each finding matters and how to resolve it.
- Avoid unnecessary refactoring suggestions.
- Do not recommend new utilities when equivalent reusable
  utilities already exist.
- Do not treat every missing negative or boundary test as
  a defect unless it is relevant to the PR scope.
- Use the team's documented standards when available.
- Do not claim tests were executed without execution evidence.
- Do not modify source code unless explicitly requested.
- If information is missing, mark it as "Not provided".
- Do not approve or reject a PR solely based on assumptions.
- Provide a clear review recommendation with supporting evidence.
```

## Expected Output

Generate a structured **Automation PR Review Report** containing the following sections.

### 1. PR Summary
- PR title and purpose.
- Automation framework and technology stack.
- Summary of changed files and functionality.
- Overall review recommendation.

### 2. PR Review Findings

Provide a review matrix with these columns:

| Column | Description |
|---|---|
| Finding ID | Unique review finding identifier |
| File / Location | File name and line number or code reference |
| Review Category | Reliability, Architecture, Code Quality, Coverage, Security, CI/CD, etc. |
| Severity | Critical, High, Medium, or Low |
| Finding | Description of the identified issue |
| Impact | Why the issue matters |
| Recommended Fix | Specific, actionable improvement |
| Evidence Status | Confirmed, Potential Risk, or Needs Verification |

### 3. Test Coverage Assessment
- Existing test scenarios covered by the PR.
- Missing or insufficient coverage within the PR scope.
- Assertion quality and validation gaps.
- Test data and dependency concerns.

### 4. Framework and Reliability Assessment
- Framework architecture alignment.
- Reusability and maintainability.
- Potential flakiness and synchronization risks.
- Test isolation and parallel execution readiness.

### 5. CI/CD and Execution Assessment
- Available test execution evidence.
- CI/CD compatibility and configuration concerns.
- Execution failures or unverified changes.
- Recommended validation before merging.

### 6. Recommended PR Comments

Provide actionable, developer-friendly review comments containing:
- File and line reference.
- Identified issue.
- Reason for the concern.
- Suggested correction.

### 7. Final Review Recommendation

Provide one of the following:

- **Approve:** No blocking issues identified and sufficient validation evidence is available.
- **Request Changes:** Confirmed blocking issues require correction before merging.
- **Needs Verification:** Insufficient evidence to determine merge readiness.

Summarize blocking findings, non-blocking improvements, and validation requirements.

## Example

**Synthetic input:**

```text
PR_DETAILS:
PR #142 - Add login automation tests.

PR_CODE_CHANGES:
File: tests/login.spec.ts

Line 1: test('login', async ({ page }) => {
Line 2:   await page.goto('/login');
Line 3:   await page.locator('#username').fill('standard_user');
Line 4:   await page.locator('#password').fill('secret_sauce');
Line 5:   await page.locator('#login-button').click();
Line 6:   await page.waitForTimeout(5000);
Line 7:   expect(page.url()).toContain('/dashboard');
Line 8: });

AUTOMATION_FRAMEWORK:
Playwright with TypeScript.

FRAMEWORK_STANDARDS:
Not provided.

TEST_REQUIREMENTS:
Successful login redirects to the dashboard.

EXECUTION_RESULTS:
Not provided.
```

**Illustrative output (not executed):**

### 1. PR Summary

| Parameter | Details |
|---|---|
| PR | #142 - Add login automation tests |
| Framework | Playwright + TypeScript |
| Changed File | tests/login.spec.ts |
| Review Recommendation | Request Changes |
| Execution Evidence | Not provided |

### 2. PR Review Findings

| Finding ID | File / Location | Review Category | Severity | Finding | Impact | Recommended Fix | Evidence Status |
|---|---|---|---|---|---|---|---|
| PR-01 | login.spec.ts:6 | Reliability | High | Fixed 5-second wait | Unnecessary execution delay and potential timing instability | Replace with assertion-based waiting | Confirmed |
| PR-02 | login.spec.ts:7 | Assertion Quality | Medium | Uses a non-retrying URL assertion | Navigation timing may cause intermittent failures | Use `await expect(page).toHaveURL(...)` | Confirmed |
| PR-03 | login.spec.ts:3–4 | Test Data | Medium | Credentials are hardcoded | Reduces configuration flexibility and may expose credentials if real secrets are used | Use existing test data or configuration utilities | Confirmed |
| PR-04 | login.spec.ts:3–5 | Framework Reusability | Low | Direct selectors and login steps may duplicate existing helpers | Possible maintenance duplication | Check for an existing login helper before refactoring | Needs Verification |

### 3. Test Coverage Assessment

| Coverage Area | Assessment |
|---|---|
| Successful login | Covered by test steps |
| Dashboard redirection | Assertion present but needs improvement |
| Invalid credentials | Not provided; applicability depends on PR scope |
| Empty credentials | Not provided; applicability depends on PR scope |
| Test execution | Not provided |

### 4. Framework and Reliability Assessment

- Fixed waits introduce avoidable delays and can make tests unreliable.
- Playwright's retrying URL assertion is more suitable for asynchronous navigation.
- Existing login helpers and configuration utilities should be checked before recommending new abstractions.
- Parallel execution safety cannot be determined from the supplied code.

### 5. CI/CD and Execution Assessment

| Validation Area | Status |
|---|---|
| Local Test Execution | Not provided |
| CI Pipeline Execution | Not provided |
| Test Reports | Not provided |
| Parallel Execution Validation | Not provided |

**Recommended validation:** Execute the updated login test locally and through the existing CI pipeline, then attach the results to the PR.

### 6. Recommended PR Comments

**Comment 1 — login.spec.ts:6**

The fixed 5-second wait adds unnecessary execution time and may still fail in slower environments. Please remove it and rely on Playwright's retrying assertions to wait for the expected navigation.

**Comment 2 — login.spec.ts:7**

Consider replacing the immediate URL assertion with:

```typescript
await expect(page).toHaveURL(/\/dashboard(?:[/?#]|$)/);
```

This provides automatic retrying while waiting for the expected URL.

**Comment 3 — login.spec.ts:3–4**

Please use the framework's existing test data or configuration mechanism for credentials, if available. This will improve maintainability and environment flexibility.

### 7. Final Review Recommendation

**Recommendation: Request Changes**

**Blocking findings:**
- PR-01: Replace fixed wait.
- PR-02: Improve navigation assertion.

**Non-blocking improvements:**
- Review credential configuration.
- Verify existing login helper reuse.

**Required validation:**
- Run the corrected login test.
- Provide local or CI execution results.

*This is an illustrative PR review based on synthetic code. No repository was accessed, no tests were executed, and no actual PR was reviewed.*