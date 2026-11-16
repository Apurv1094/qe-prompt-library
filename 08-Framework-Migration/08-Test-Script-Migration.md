# Test Script Migration

## Purpose
Convert selected source automation tests to the target runner while preserving test intent, assertions, and traceability.

## When to use
After reusable components, test data, and target configuration are ready.

## Inputs required
- `{{SOURCE_TEST_PATHS}}` — **Required:** Source test files or suites to migrate. Example: `src/test/java/tests/LoginTest.java`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Destination target framework directory. Example: `D:\QA\playwright-tests`.
- `{{APPROVED_MIGRATION_PLAN}}` — **Required:** Approved coverage priorities, design rules and migration mapping. Example: `artifacts/framework-migration-assessment.md`.
- `{{TEST_SCOPE}}` — **Required:** Specific scenarios to migrate in this run. Example: `Login positive, invalid password, empty credentials`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Convert selected source automation tests to the target runner while preserving test intent, assertions, and traceability.

Inputs:
SOURCE_TEST_PATHS:
{{SOURCE_TEST_PATHS}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
APPROVED_MIGRATION_PLAN:
{{APPROVED_MIGRATION_PLAN}}
TEST_SCOPE:
{{TEST_SCOPE}}

Instructions:
1. Inspect each selected source test, related page objects, data, setup, assertions, and test identifiers.
2. Build a source-to-target test mapping and identify unsupported steps or ambiguous business expectations.
3. Generate idiomatic target tests using existing approved pages/fixtures; preserve meaningful assertions and negative cases.
4. Use verified locators when accessible; otherwise mark locators as unverified rather than inventing them.
5. Keep tests isolated and deterministic; avoid hardcoded sleeps, order dependencies, and embedded secrets.
6. Run targeted tests only if execution is authorized; report pass/fail/skipped and do not claim parity without evidence.

Rules:
- Inspect the actual source and target files before proposing or applying changes.
- Follow the approved migration scope and record evidence with relevant file paths.
- Do not invent framework behavior, test outcomes, missing files, or tool results.
- Ask for missing mandatory inputs and flag uncertain decisions explicitly.
- Do not overwrite unrelated code or remove source assets without approval.
- Protect credentials, tokens, personal data and proprietary information; apply the central QE Prompt Library privacy guardrails.
- Separate completed changes, proposed changes, and validation not performed.
- Require human review of material architecture or behavior changes.
```

## Expected output
1. Source-to-target test case mapping with IDs.
2. Generated target test files and changed-file list.
3. Coverage parity and assertion comparison.
4. Execution evidence, blocked cases and follow-up actions.

## Example
**Synthetic input:**
```text
SOURCE_TEST_PATHS: src/test/java/tests/LoginTest.java
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
APPROVED_MIGRATION_PLAN: artifacts/framework-migration-assessment.md
TEST_SCOPE: Login positive, invalid password, empty credentials
```

**Illustrative output (synthetic; not an actual execution result):**
```text
Created tests/login.spec.ts with LOGIN_01 and LOGIN_02; 2/2 source cases mapped. Execution: not run. Unverified locator: error message.
```

## Limitations
- Accurate migration requires access to relevant source and target repository files; missing access must be reported.
- Static inspection cannot establish runtime compatibility or test parity; report verification status explicitly.
- Dependency installation, test execution, CI changes and file deletion require the necessary tool access and authorization.
- Never expose real secrets or sensitive test data in generated files, logs or examples.
- Final migration decisions and production/CI cutover require QE or engineering approval.

## Owner / Version
- Owner: QE Automation Team
- Version: 1.0.0
