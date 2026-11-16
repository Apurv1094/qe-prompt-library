# Framework Configuration Migration

## Purpose
Translate source automation settings into target framework configuration while protecting secrets and preserving intended execution behavior.

## When to use
After dependency setup and before migrating tests that depend on environment settings.

## Inputs required
- `{{SOURCE_CONFIGURATION_PATHS}}` — **Required:** Paths to existing configuration files. Example: `config.properties, testng.xml`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Target framework directory to configure. Example: `D:\QA\playwright-tests`.
- `{{APPROVED_MIGRATION_PLAN}}` — **Required:** Approved target environment and execution requirements. Example: `artifacts/framework-migration-assessment.md`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Translate source automation settings into target framework configuration while protecting secrets and preserving intended execution behavior.

Inputs:
SOURCE_CONFIGURATION_PATHS:
{{SOURCE_CONFIGURATION_PATHS}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
APPROVED_MIGRATION_PLAN:
{{APPROVED_MIGRATION_PLAN}}

Instructions:
1. Read source settings for base URLs, browsers, timeouts, retries, environments, credentials references, and execution options.
2. Create a source-to-target setting mapping and flag settings without direct equivalents.
3. Implement supported target settings using native configuration and environment-variable references; do not hardcode credentials.
4. Keep defaults explicit and distinguish source-observed values from proposed values.
5. Preserve existing target configuration unrelated to migration; do not overwrite without review.
6. Validate configuration syntax when tools are available and report any settings not verified at runtime.

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
1. Configuration mapping table with source and target keys.
2. Created or modified configuration files.
3. Secret-handling and environment-variable notes.
4. Syntax/runtime validation status and unresolved settings.

## Example
**Synthetic input:**
```text
SOURCE_CONFIGURATION_PATHS: config.properties, testng.xml
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
APPROVED_MIGRATION_PLAN: artifacts/framework-migration-assessment.md
```

**Illustrative output (synthetic; not an actual execution result):**
```text
Mapping: base.url → use.baseURL; timeout → action/navigation setting after review; browser → chromium project. Secret values not copied. Syntax check: pending.
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
