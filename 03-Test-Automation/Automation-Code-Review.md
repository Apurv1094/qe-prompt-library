# Automation Code Review

## Purpose
Review existing or newly written test automation code for correctness, reliable assertions, stability, maintainability, security, and alignment with the project's established framework. Produce evidence-based, actionable code-level findings without making a pull-request merge decision.

## When to Use
Use during automation development, peer code review, framework maintenance, or technical-debt assessment. Run this review before committing changes or when investigating fragile automation. This prompt is for **code quality**, not PR-wide change impact or approval.

## Inputs Required
- `{{AUTOMATION_CODE}}` — **Required:** Files, methods, directories, or code snippets to review; use workspace paths when running in a repository-aware agent.
- `{{REVIEW_CONTEXT}}` — **Optional:** Intended behavior, particular concerns, scope, or constraints that should guide the review.
- `{{TEST_REQUIREMENTS}}` — **Optional:** User stories, acceptance criteria, or test scenarios needed to assess assertion and coverage correctness.
- `{{EXECUTION_EVIDENCE}}` — **Optional:** Existing test results, CI logs, traces, screenshots, or known failure patterns; do not require execution to perform a static review.

**Framework discovery:** When workspace access is available, inspect the project to determine language, framework, dependencies, conventions, fixtures, utilities, configuration, and relevant CI setup. Do not ask the user to re-enter discoverable framework details. If only a snippet is available, state what cannot be verified.

## Prompt

```text
Role: Act as a Senior QE Automation Architect with 10+ years of hands-on experience reviewing and maintaining UI, API, and framework automation code.

Task: Perform a focused, evidence-based technical code review. Determine whether the supplied automation is correct, stable, maintainable, reusable, secure, and consistent with the existing project. Review code; do not issue PR approval or merge-readiness decisions.

Inputs:
AUTOMATION_CODE:
{{AUTOMATION_CODE}}

REVIEW_CONTEXT:
{{REVIEW_CONTEXT}}

TEST_REQUIREMENTS:
{{TEST_REQUIREMENTS}}

EXECUTION_EVIDENCE:
{{EXECUTION_EVIDENCE}}

Workflow:
1. Inspect the requested code and relevant surrounding files. Discover the actual framework from manifests, configurations, test fixtures, helpers, and established patterns when accessible.
2. Identify the intended behavior and assertions. State any missing requirements or context.
3. Review the applicable areas below; mark non-applicable areas N/A instead of manufacturing findings.
4. For each finding, capture an exact file/line or quoted snippet, its impact, a practical fix, and evidence confidence.
5. Distinguish confirmed static code issues, potential runtime risks, and questions needing verification.
6. Summarize strengths, prioritized fixes, and specific verification steps. Do not modify files unless explicitly authorized.

Review checklist:
A. Correctness: control flow, async/await, error handling, false positives, skipped checks, and meaningful test outcomes.
B. Assertions: expected business behavior, retrying versus immediate assertions, specificity, diagnostic quality, and negative/boundary checks when in scope.
C. Stability: hardcoded sleeps, race conditions, synchronization, retries that conceal defects, dynamic data, and locator resilience.
D. Reusability and architecture: reuse existing fixtures, Page Objects or components where appropriate, API clients, request specifications, utilities, and separation of concerns; avoid needless abstractions.
E. Readability and maintainability: names, duplication, unnecessary complexity, dead code, misleading comments, and useful logging.
F. Test data and configuration: environment independence, setup/cleanup, deterministic data, hardcoded secrets versus harmless demo values, and secure configuration.
G. Isolation and parallelism: independent tests, shared state, session/context management, resource cleanup, and conflicting data.
H. UI-specific (if applicable): robust accessible/stable locators, navigation waits, page/component abstractions, and browser assumptions.
I. API-specific (if applicable): request construction, status/body/schema/header assertions, authentication, negative responses, timeouts, and cleanup after mutations.
J. Execution efficiency and CI compatibility: redundant setup, unnecessary waits, local-only paths, test grouping, artifacts, logs, and diagnosability.
K. Security: exposed real secrets, sensitive logs, unsafe test operations, and unnecessary dependencies.

Rules:
- Ground findings in supplied or accessible code. Do not invent missing helpers, defects, requirements, or runtime outcomes.
- Inspect existing conventions and reusable components before suggesting a new abstraction.
- A direct locator or hardcoded non-secret test datum is not automatically a defect.
- Cite exact file/line references when available; otherwise quote the relevant snippet and say line numbers are unavailable.
- Label each finding Confirmed, Potential Risk, or Needs Verification. Confirmed means the code pattern is observable, not that runtime failure was reproduced.
- Use Critical/High/Medium/Low severity based on practical impact; do not inflate severity for style preferences.
- Prefer minimal, framework-native corrections. Explain assumptions behind example code.
- Do not assume every negative or boundary case belongs in the reviewed file.
- Do not claim execution, reproduction, or file modifications without evidence.
- Mark missing evidence as 'Not provided'. If requirements are unavailable, assess structural quality but do not claim full business coverage.
- Never expose secrets or personal data in review output; redact sensitive snippets.
- Do not change code unless explicitly requested.

Deliverables:
1. Review summary and risk assessment.
2. Findings matrix with ID, location, category, severity, finding, impact, fix, and evidence status.
3. Code quality/framework assessment and reliability assessment.
4. Targeted before/after code examples for significant findings.
5. Positive practices, unresolved questions, verification steps, and explicit execution/modification status.
```

## Expected Output

### 1. Review Summary
State reviewed files, detected framework (or `Not provided`), intended test behavior, review scope, overall technical risk (High/Medium/Low), confirmed finding count, potential-risk count, and execution evidence status.

### 2. Code Review Findings Matrix

| Column | Meaning |
|---|---|
| Finding ID | Stable identifier, e.g., CR-01 |
| File / Line | Exact location or identifiable snippet |
| Category | Correctness, Assertions, Reliability, Architecture, Test Data, Security, etc. |
| Severity | Critical, High, Medium, or Low |
| Finding | Specific observable issue or qualified concern |
| Technical Impact | Why the issue matters |
| Recommended Fix | Minimal actionable correction |
| Evidence Status | Confirmed, Potential Risk, or Needs Verification |

### 3. Code Quality and Framework Assessment
Describe architecture fit, utility reuse, readability, duplication, and maintainability. Mark unavailable context `Not provided`.

### 4. Reliability and Execution Assessment
Assess synchronization, isolation, parallel safety, test data, assertions, CI compatibility, and available runtime evidence. Distinguish code inspection from actual execution.

### 5. Recommended Code Improvements
For significant findings, show the relevant existing snippet, a corrected snippet, and why it is better. Note assumptions (e.g., configured base URL, actual accessible labels).

### 6. Positive Engineering Practices
List only strengths supported by reviewed code.

### 7. Open Questions and Verification
List missing context, targeted checks to run, and whether code was modified or tests executed.

## Example

**Synthetic input:**

```text
AUTOMATION_CODE:
File: tests/login.spec.ts
1  import { test, expect } from '@playwright/test';
2  test('valid login', async ({ page }) => {
3    await page.goto('/login');
4    await page.locator('#username').fill('standard_user');
5    await page.locator('#password').fill('secret_sauce');
6    await page.locator('#login-button').click();
7    await page.waitForTimeout(5000);
8    expect(page.url()).toContain('/dashboard');
9  });

REVIEW_CONTEXT: Review a Playwright TypeScript smoke test for stability and assertions.
TEST_REQUIREMENTS: Successful login redirects to /dashboard.
EXECUTION_EVIDENCE: Not provided.
```

**Illustrative output (static review only; not executed):**

### 1. Review Summary

| Field | Result |
|---|---|
| Reviewed files | `tests/login.spec.ts` |
| Framework | Playwright + TypeScript (identified from import) |
| Intended behavior | Valid login redirects to dashboard |
| Review scope | Code reliability and assertion quality |
| Overall technical risk | Medium |
| Confirmed findings | 2 |
| Potential risks | 1 |
| Execution evidence | Not provided |

### 2. Code Review Findings Matrix

| Finding ID | File / Line | Category | Severity | Finding | Technical Impact | Recommended Fix | Evidence Status |
|---|---|---|---|---|---|---|---|
| CR-01 | `login.spec.ts:7` | Reliability | Medium | Fixed five-second sleep | Adds delay and does not synchronize to a meaningful state | Remove sleep and use a retrying assertion | Confirmed |
| CR-02 | `login.spec.ts:8` | Assertions | Medium | Immediate URL assertion | May evaluate before navigation completes | Use `await expect(page).toHaveURL(...)` | Confirmed |
| CR-03 | `login.spec.ts:4–5` | Test Data | Low | Inline demo credentials | May hinder environment reuse if credentials differ | Check existing fixtures/configuration before changing | Potential Risk |

### 3. Code Quality and Framework Assessment

| Area | Assessment |
|---|---|
| Framework fit | Uses Playwright Test APIs |
| Utility reuse | Not provided; surrounding repository unavailable |
| Readability | Short, focused login flow |
| Duplication | Cannot determine from one snippet |
| Maintainability | Synchronization can be simplified |

### 4. Reliability and Execution Assessment

| Area | Assessment |
|---|---|
| Synchronization | Fixed sleep found |
| Assertions | URL check present but non-retrying |
| Isolation and parallel safety | Not provided |
| Test data | Inline demonstration values; framework policy unknown |
| CI compatibility | Not provided |
| Execution evidence | Not provided |

### 5. Recommended Code Improvements

**CR-01 / CR-02 — Replace sleep and immediate URL check.**

Before:
```typescript
await page.waitForTimeout(5000);
expect(page.url()).toContain('/dashboard');
```

After:
```typescript
await expect(page).toHaveURL(/\/dashboard(?:[/?#]|$)/);
```

The Playwright assertion retries until the URL matches or times out. This assumes `/dashboard` is the expected route; confirm against the application contract.

**CR-03 — Test data:** Check whether the repository already has a fixture or configuration mechanism; do not create a new one without evidence it is needed.

### 6. Positive Engineering Practices
- Uses Playwright's built-in test runner and `expect`.
- Keeps the example focused on one login flow.
- Includes an intended post-login check, though it needs a retrying assertion.

### 7. Open Questions and Verification
- Does the repository already have login fixtures or test data helpers?
- Is `/dashboard` the exact expected destination for this environment?
- After updating the assertion, run the test locally and in CI; inspect repeatability and traces if failures occur.
- **Code modified:** No. **Tests executed:** No. **Runtime defects reproduced:** No.

*Illustrative review of synthetic code only; no actual repository or execution evidence was inspected.*

## Limitations
- A static review cannot prove that a test passes or that flakiness occurs at runtime.
- Architectural judgments may be limited when surrounding files or standards are unavailable.
- Suggested code must be checked against actual application behavior and project configuration.
- Follow shared privacy, evidence, authorization, and human-review requirements in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- **Owner:** QE Prompt Library maintainers (assign named owner before publication)
- **Version:** 1.3.0
- **Status:** Draft for team review
