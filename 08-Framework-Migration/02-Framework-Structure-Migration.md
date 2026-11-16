# Framework Structure Migration

## Purpose
Create the target framework directory and module structure based on an approved migration assessment, without migrating test logic.

## When to use
After the assessment is approved and before configuring or converting tests.

## Inputs required
- `{{SOURCE_REPOSITORY_PATH}}` — **Required:** Existing repository to inspect. Example: `D:\QA\selenium-tests`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Destination folder for the target framework. Example: `D:\QA\playwright-tests`.
- `{{APPROVED_MIGRATION_PLAN}}` — **Required:** Approved architecture and migration decisions, or path to the assessment report. Example: `artifacts/framework-migration-assessment.md`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Create the target framework directory and module structure based on an approved migration assessment, without migrating test logic.

Inputs:
SOURCE_REPOSITORY_PATH:
{{SOURCE_REPOSITORY_PATH}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
APPROVED_MIGRATION_PLAN:
{{APPROVED_MIGRATION_PLAN}}

Instructions:
1. Inspect source directories, module boundaries, shared components, and test organization.
2. Read the approved plan and identify the target language, runner, and directory conventions; request clarification if not specified.
3. Propose a source-to-target directory mapping before creating files.
4. Create only the agreed folders and minimal structural placeholders required by the target architecture; do not copy obsolete base classes or invent test implementations.
5. Preserve the source repository; do not overwrite existing target files without approval.
6. Report created paths, skipped paths, mappings, and any deviations from the plan.

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
1. Source-to-target folder mapping with rationale.
2. Created target directory tree and placeholder file list.
3. Skipped or blocked changes and decisions requiring approval.
4. Structure verification evidence and next-step handoff.

## Example
**Synthetic input:**
```text
SOURCE_REPOSITORY_PATH: D:\QA\selenium-tests
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
APPROVED_MIGRATION_PLAN: artifacts/framework-migration-assessment.md
```

**Illustrative output (synthetic; not an actual execution result):**
```text
Mapping: pages → pages/; tests → tests/; utils → utils/. Created: pages/, tests/, fixtures/, utils/. No test scripts converted. Verification: folders exist.
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
