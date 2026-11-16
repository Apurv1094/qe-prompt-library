# Dependencies and Build Setup

## Purpose
Set up target framework dependencies and reproducible build/install commands, removing legacy dependencies only when authorized.

## When to use
After target structure is agreed and before configuration or script conversion.

## Inputs required
- `{{SOURCE_REPOSITORY_PATH}}` — **Required:** Location of source build and dependency manifests. Example: `D:\QA\selenium-tests`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Location where target build files will be created or updated. Example: `D:\QA\playwright-tests`.
- `{{APPROVED_MIGRATION_PLAN}}` — **Required:** Approved target stack and dependency decisions. Example: `artifacts/framework-migration-assessment.md`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Set up target framework dependencies and reproducible build/install commands, removing legacy dependencies only when authorized.

Inputs:
SOURCE_REPOSITORY_PATH:
{{SOURCE_REPOSITORY_PATH}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
APPROVED_MIGRATION_PLAN:
{{APPROVED_MIGRATION_PLAN}}

Instructions:
1. Inspect source build files, lockfiles, runtime requirements, plugins, and dependency usage.
2. Derive target runtime and package requirements from the approved plan; check compatibility and version constraints against available project evidence.
3. Map each necessary capability (test runner, assertions, browser tooling, reporting, linting) to a target dependency; avoid adding unused packages.
4. Create or update target manifests and reproducible install/build/test scripts, preserving existing unrelated settings.
5. Do not install packages or access external registries unless authorized and tools are available; do not claim a successful installation without running it.
6. Record version selections, unresolved compatibility questions, commands, and verification results.

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
1. Source dependency inventory and target dependency mapping.
2. Updated manifest and lockfile status.
3. Setup/install/test commands with prerequisites.
4. Verification status and unresolved dependency risks.

## Example
**Synthetic input:**
```text
SOURCE_REPOSITORY_PATH: D:\QA\selenium-tests
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
APPROVED_MIGRATION_PLAN: artifacts/framework-migration-assessment.md
```

**Illustrative output (synthetic; not an actual execution result):**
```text
Target: package.json with @playwright/test and test script. Command: npm install; npx playwright install. Verification: not run (installation not authorized).
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
