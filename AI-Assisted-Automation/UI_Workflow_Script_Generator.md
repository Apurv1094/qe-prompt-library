# UI Workflow Script Generator

## Purpose

Inspect an existing UI automation framework and generate maintainable, executable workflow automation scripts from the workflows produced by `Workflow_Generator.md`.

A workflow may combine multiple test cases into a single logical execution. Reuse shared setup and navigation while preserving every original test case's expected result and traceability.

**This prompt generates automation code. It does not generate or redesign the framework.**

---

## Mandatory Input

### GENERATED_WORKFLOWS

Paste the output from `Workflow_Generator.md`, including workflow IDs, related test case IDs, execution steps, expected results, prerequisites, and test data where available.

```text
GENERATED_WORKFLOWS:
"""
[Paste generated workflows here]
"""
```

**Framework access:** Run this prompt in the existing UI automation repository/workspace. The agent should inspect the project directly. If the repository is inaccessible, request access or the relevant configuration and source files before generating implementation-specific code. Do not invent a framework structure.

---

## Reusable Prompt

Act as a Senior UI Automation Engineer working inside the existing project.

Your task is to inspect the current UI automation framework and implement the supplied workflows as executable automated tests, following the project's established conventions.

### Phase 1 — Inspect the Existing Framework

1. Identify the automation tool and language (for example, Playwright with TypeScript, Selenium with Java, or Cypress with JavaScript).
2. Inspect project configuration, test runner, dependencies, test discovery rules, directory structure, and naming conventions.
3. Identify the current design pattern and reusable components: page objects, screen objects, fixtures, base classes, actions, helpers, selectors, assertions, authentication/session handling, test data, environment configuration, reports, and CI integration.
4. Review representative existing tests and determine how new workflow tests should be structured.
5. Summarize the actual files and components that will be reused. Do not assume a particular framework or design pattern.

### Phase 2 — Analyze and Map Workflows

1. Read every supplied workflow ID, test case ID, prerequisite, step, expected result, and available test data.
2. Map workflow actions to existing reusable framework methods and identify missing actions or assertions.
3. Determine which steps can safely share setup, login, navigation, and test data.
4. Preserve the logical order and expected result of each test case. Add explicit assertions for each test case's verifiable outcome.
5. Keep independent negative scenarios, destructive scenarios, conflicting data states, and tests requiring isolated sessions separate when combining them would make results unreliable.
6. If a workflow lacks necessary test data, expected outcomes, or application behavior, clearly flag the gap rather than inventing values.
7. Present a concise workflow-to-script mapping before implementation.

### Phase 3 — Generate Workflow Scripts

1. Generate executable scripts using the **existing** tool, language, test runner, design pattern, naming conventions, and folder structure.
2. Prefer existing page objects, fixtures, utilities, selectors, and data providers. Extend reusable components only where necessary.
3. Avoid duplicate logins and repeated navigation when state can safely be shared within a workflow.
4. Create one cohesive workflow test where appropriate, with clearly labeled assertion checkpoints for each mapped test case.
5. Ensure every original test case ID appears in code comments, named steps, metadata, or reporting hooks, as supported by the framework.
6. Do not hide failures with blanket exception handling, unconditional retries, arbitrary sleeps, or weak assertions.
7. Use stable locators, proper waits, test isolation, safe data cleanup, and secrets from existing configuration mechanisms.
8. Respect project linting, formatting, package conventions, and existing test naming standards.
9. Do not replace the current framework, change its technology, or introduce dependencies without a clear need and approval.

### Phase 4 — Validate

1. Check that generated files compile or pass type checking and are discoverable by the existing test runner.
2. Run targeted workflow tests if the environment, credentials, and application are available and execution is authorized.
3. Review results and fix script defects caused by the generated code, then rerun relevant checks when possible.
4. Distinguish actual test passes from tests not executed. Never claim a pass based only on generated code.
5. Report test case coverage, execution results, blocked checks, and remaining gaps.

---

## Required Output

### 1. Framework Inspection Summary

| Item | Finding |
|---|---|
| Automation tool and language | Detected from repository |
| Test runner | Detected from repository |
| Design pattern | Detected from repository |
| Reusable components | Existing files/classes/functions |
| Test location and naming convention | Detected from repository |
| Execution command | Actual project command |

### 2. Workflow-to-Script Mapping

| Workflow ID | Test Case IDs | Target Script | Reused Components | New Components Needed |
|---|---|---|---|---|
| WF-01 | TC-01, TC-02, TC-03 | [Actual path] | [Existing methods] | [Only if needed] |

### 3. Generated or Modified Files

For each file, provide its path, purpose, and whether it was created or modified. Implement the changes in the repository when write access is available. Otherwise provide complete code and placement instructions.

### 4. Execution and Validation Results

- Commands run and their outcomes
- Workflow IDs executed
- Test case checkpoints covered
- Passed, failed, blocked, and not-run results (only when evidenced)
- Issues and recommended fixes

### 5. Coverage Traceability

| Workflow ID | Test Case ID | Assertion or Checkpoint | Implementation Location | Validation Status |
|---|---|---|---|---|

All input test case IDs must appear in the coverage mapping. Mark omitted or blocked cases explicitly.

---

## Rules

- **Mandatory input:** `GENERATED_WORKFLOWS` only. Do not request separate application pages as input.
- Treat the workflow generator's output as the source of workflow definitions, not as evidence that the application currently behaves as described.
- Inspect the actual repository before generating framework-specific code.
- Reuse existing framework conventions; do not generate a new framework.
- Consolidate repeated actions only when doing so does not compromise isolation or correctness.
- Keep test case checkpoints individually identifiable even when one workflow has a single pass/fail outcome. If the runner stops after a failure, explain that later checkpoints were not executed; do not report them as passed.
- Avoid brittle selectors, fixed delays, hard-coded credentials, and unnecessary dependencies.
- Do not fabricate files, methods, test data, execution results, or coverage.
- If repository access is missing, explain what is needed to proceed.

---

## Example Input

```text
GENERATED_WORKFLOWS:
"""
Workflow ID: WF-01
Workflow Name: Login and Dashboard Verification
Prerequisite: Valid test account and accessible application
Test Cases:
  TC-01: Login with valid credentials; expected: login succeeds.
  TC-02: Verify dashboard heading; expected: heading is displayed.
  TC-03: Verify application logo; expected: logo is visible.
  TC-04: Verify navigation options; expected: expected menu items are visible.
Execution Steps:
  1. Open the application.
  2. Enter valid account credentials and sign in.
  3. Verify login success.
  4. Verify dashboard heading.
  5. Verify application logo.
  6. Verify navigation options.
"""
```

**Expected behavior:** Inspect the existing framework, reuse its login and dashboard components, generate one workflow script with distinct TC-01 through TC-04 checkpoints, and provide actual validation evidence or explicitly mark tests as not run.
