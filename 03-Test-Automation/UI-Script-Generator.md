# UI Script Generator

## Purpose
Generate or update UI automation scripts from provided test cases and acceptance criteria using an existing UI automation framework.

## When to use
Use this prompt when generate or update UI tests in an existing framework using supplied cases and acceptance criteria. Ensure the required inputs are available.

## Inputs required
- `{{EXISTING_FRAMEWORK_PATH}}` — **Required:** Existing UI automation project path to inspect and reuse.
- `{{TEST_CASES}}` — **Required:** Test case IDs, steps, preconditions, data and expected outcomes.
- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Approved user-facing behavior and assertions for each case.
- `{{OUTPUT_DIRECTORY}}` — **Optional:** Optional target directory; if omitted, use paths in test plan, then framework conventions.
- `{{EXECUTION_REQUIRED}}` — **Optional:** Optional Yes/No execution permission; defaults to No.

## Prompt
```text
Role: Act as a Senior UI Test Automation Engineer.

Task: Generate or update UI tests in an existing framework using supplied cases and acceptance criteria.

Inputs:
EXISTING_FRAMEWORK_PATH:
{{EXISTING_FRAMEWORK_PATH}}
TEST_CASES:
{{TEST_CASES}}
ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}
OUTPUT_DIRECTORY:
{{OUTPUT_DIRECTORY}}
EXECUTION_REQUIRED:
{{EXECUTION_REQUIRED}}

Rules:
- Inspect project conventions, existing scripts, fixtures, page objects and coverage before editing.
- Generate only requested cases; reuse abstractions and maintain case ID traceability.
- Use verified locators; if UI access is unavailable, flag selectors as unverified rather than claiming runnable validation.
- Prefer condition-based assertions and waits; avoid fixed sleeps, shared state and hardcoded secrets.
- If output path conflicts with test plan paths, ask for clarification; report exact file paths.
- Preserve unrelated tests and files; do not create a new framework or agent.
- Run only when explicitly authorized and environment is available; report actual results, never imagined passes.

Deliverables:
- Framework inspection and reuse notes
- Case ID to script path and assertion mapping
- Exact generated/modified files and execution command
- Execution results if run, otherwise Not executed; selector or requirement gaps
```

## Expected output
- Framework inspection and reuse notes
- Case ID to script path and assertion mapping
- Exact generated/modified files and execution command
- Execution results if run, otherwise Not executed; selector or requirement gaps
- Clearly label assumptions, missing evidence, and whether files were created or tests executed.

## Example
**Synthetic input:**
```text
EXISTING_FRAMEWORK_PATH: ./ui-tests; TEST_CASES: LOGIN_TC_01 valid login; ACCEPTANCE_CRITERIA: Successful login shows Products heading; OUTPUT_DIRECTORY: tests/login; EXECUTION_REQUIRED: No.
```

**Illustrative output (not executed):**
> LOGIN_TC_01 → tests/login/login.spec.ts → assert Products heading visible; locator requires live verification; command: npx playwright test tests/login/login.spec.ts; Not executed.

The example is illustrative only; use actual input evidence for real deliverables.

## Limitations
- Results depend on supplied requirements, repository access, tool availability and authorization.
- Generated code or recommendations are not verified until explicitly checked or executed.
- Shared privacy, evidence, authorization and human-review requirements: `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
