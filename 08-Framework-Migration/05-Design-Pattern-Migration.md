# Design Pattern Migration

## Purpose
Migrate reusable test architecture and design patterns to target-native equivalents without carrying over unnecessary legacy abstractions.

## When to use
Once target structure and configuration exist, before bulk test conversion.

## Inputs required
- `{{SOURCE_COMPONENT_PATHS}}` — **Required:** Paths to source page objects, base classes, fixtures or patterns. Example: `src/test/java/pages, src/test/java/base`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Target framework directory for migrated abstractions. Example: `D:\QA\playwright-tests`.
- `{{APPROVED_MIGRATION_PLAN}}` — **Required:** Approved target design conventions and migration scope. Example: `artifacts/framework-migration-assessment.md`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Migrate reusable test architecture and design patterns to target-native equivalents without carrying over unnecessary legacy abstractions.

Inputs:
SOURCE_COMPONENT_PATHS:
{{SOURCE_COMPONENT_PATHS}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
APPROVED_MIGRATION_PLAN:
{{APPROVED_MIGRATION_PLAN}}

Instructions:
1. Inspect source classes and their callers to identify responsibilities, selectors, waits, setup, assertions, and shared state.
2. Map each pattern to a target-native equivalent; justify when a base class should become a fixture or be removed.
3. Migrate reusable abstractions in small units, preserving public behavior and minimizing duplicated logic.
4. Use target-native locators and synchronization; do not blindly translate Selenium waits or PageFactory annotations.
5. Keep test assertions in appropriate layers unless the approved design specifies otherwise.
6. Check imports/types and show an example usage; mark unverified selectors or behavior for validation.

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
1. Source-to-target design pattern mapping.
2. Migrated page/fixture/helper files and changed-file summary.
3. Sample integration usage and assumptions.
4. Static checks and behavior-validation checklist.

## Example
**Synthetic input:**
```text
SOURCE_COMPONENT_PATHS: src/test/java/pages, src/test/java/base
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
APPROVED_MIGRATION_PLAN: artifacts/framework-migration-assessment.md
```

**Illustrative output (synthetic; not an actual execution result):**
```text
Created pages/LoginPage.ts with locator-based login(); replaced driver setup with Playwright page fixture. Locator verification: pending against live UI.
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
