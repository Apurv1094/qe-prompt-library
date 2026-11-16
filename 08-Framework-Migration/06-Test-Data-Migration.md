# Test Data Migration

## Purpose
Adapt test data sources and data-driven execution to the target framework without changing business scenarios or exposing sensitive values.

## When to use
After target configuration and fixtures are defined, before converting data-driven tests.

## Inputs required
- `{{SOURCE_TEST_DATA_PATHS}}` — **Required:** Paths to datasets, data providers and loading helpers. Example: `src/test/resources/data, src/test/java/providers`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Destination for migrated data and loaders. Example: `D:\QA\playwright-tests`.
- `{{DATA_HANDLING_REQUIREMENTS}}` — **Required:** Required formats, environments, privacy rules and data ownership. Example: `Keep JSON datasets; mask customer details; no production data`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Adapt test data sources and data-driven execution to the target framework without changing business scenarios or exposing sensitive values.

Inputs:
SOURCE_TEST_DATA_PATHS:
{{SOURCE_TEST_DATA_PATHS}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
DATA_HANDLING_REQUIREMENTS:
{{DATA_HANDLING_REQUIREMENTS}}

Instructions:
1. Inventory source data formats, schemas, generators, DataProviders, environment dependencies, and test-to-data links.
2. Classify datasets as reusable, transformable, generated, or unsuitable; identify secrets and personal data.
3. Map source parameters and expected outcomes to target fixtures, parameterization, or data-loading utilities.
4. Migrate only authorized sanitized data; preserve boundary cases, negative cases, and unique test identifiers.
5. Validate schema, record counts, field mappings, and encoding where tooling permits.
6. Do not invent missing values or silently alter business expectations; flag gaps and data refresh needs.

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
1. Dataset inventory and source-to-target field mapping.
2. Migrated sanitized data and loader/fixture paths.
3. Record-count and schema validation results.
4. Excluded sensitive data and unresolved mapping issues.

## Example
**Synthetic input:**
```text
SOURCE_TEST_DATA_PATHS: src/test/resources/data, src/test/java/providers
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
DATA_HANDLING_REQUIREMENTS: Keep JSON datasets; mask customer details; no production data
```

**Illustrative output (synthetic; not an actual execution result):**
```text
Converted 3 synthetic rows to test-data/users.json; fields username, passwordRef, expectedStatus. Row count: 3→3; secret values excluded.
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
