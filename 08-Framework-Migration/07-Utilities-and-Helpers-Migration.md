# Utilities and Helpers Migration

## Purpose
Migrate shared automation utilities to target-compatible implementations while eliminating redundant or unsafe helpers.

## When to use
After design patterns and configuration are established, before dependent test scripts are converted.

## Inputs required
- `{{SOURCE_UTILITY_PATHS}}` — **Required:** Paths to reusable source helpers and their callers. Example: `src/test/java/utils`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Target framework folder for reusable helpers. Example: `D:\QA\playwright-tests`.
- `{{APPROVED_MIGRATION_PLAN}}` — **Required:** Approved helper migration decisions and target conventions. Example: `artifacts/framework-migration-assessment.md`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Migrate shared automation utilities to target-compatible implementations while eliminating redundant or unsafe helpers.

Inputs:
SOURCE_UTILITY_PATHS:
{{SOURCE_UTILITY_PATHS}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
APPROVED_MIGRATION_PLAN:
{{APPROVED_MIGRATION_PLAN}}

Instructions:
1. Inventory helpers for waits, screenshots, API calls, dates, file operations, authentication, assertions, and reporting.
2. Inspect usage sites and classify each helper as reuse, adapt, replace with native API, or retire.
3. Prefer built-in target framework features over custom wrappers; preserve domain-specific behavior where needed.
4. Migrate utilities in dependency order with clear interfaces and error handling.
5. Avoid fixed sleeps, hardcoded credentials, hidden shared state, and swallowed exceptions.
6. Add focused checks or tests for migrated helpers where feasible; document callers requiring updates.

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
1. Utility inventory and migration decision per helper.
2. Migrated utility files or native API replacements.
3. Caller impact and interface changes.
4. Validation results and unresolved dependencies.

## Example
**Synthetic input:**
```text
SOURCE_UTILITY_PATHS: src/test/java/utils
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
APPROVED_MIGRATION_PLAN: artifacts/framework-migration-assessment.md
```

**Illustrative output (synthetic; not an actual execution result):**
```text
WaitUtil → retire in favor of auto-waiting; ScreenshotUtil → page.screenshot(); TokenHelper → adapt with env-based secret reference. Verification: static review only.
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
