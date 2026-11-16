# Reporting and Logging Migration

## Purpose
Preserve essential test results, failure diagnostics and report consumption during framework migration.

## When to use
Once migrated tests run and before CI reporting is finalized.

## Inputs required
- `{{SOURCE_REPORTING_SETUP}}` — **Required:** Existing reporters, logging libraries and sample report paths. Example: `ExtentReports config and target/surefire-reports`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Target framework directory. Example: `D:\QA\playwright-tests`.
- `{{REPORTING_REQUIREMENTS}}` — **Required:** Required formats, artifacts, retention and consumers. Example: `HTML + JUnit XML; screenshots on failure; Jenkins ingestion`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Preserve essential test results, failure diagnostics and report consumption during framework migration.

Inputs:
SOURCE_REPORTING_SETUP:
{{SOURCE_REPORTING_SETUP}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
REPORTING_REQUIREMENTS:
{{REPORTING_REQUIREMENTS}}

Instructions:
1. Inventory source report fields, pass/fail/skip semantics, logs, attachments, and CI consumers.
2. Map required report outputs to supported target reporters and artifact collection.
3. Configure reporting, logging, screenshots, traces or videos according to requirements, with privacy-safe defaults.
4. Avoid duplicate logging and ensure sensitive request payloads, tokens, and personal data are redacted.
5. Verify report generation with an authorized sample run when possible; distinguish configured from observed artifacts.
6. Document report locations, retention considerations, integration points, and gaps in historical comparability.

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
1. Reporting capability and artifact mapping.
2. Reporter configuration and output paths.
3. Privacy and retention considerations.
4. Sample-run validation status and known gaps.

## Example
**Synthetic input:**
```text
SOURCE_REPORTING_SETUP: ExtentReports config and target/surefire-reports
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
REPORTING_REQUIREMENTS: HTML + JUnit XML; screenshots on failure; Jenkins ingestion
```

**Illustrative output (synthetic; not an actual execution result):**
```text
Configured HTML and JUnit reporters; output: playwright-report/ and test-results/results.xml. Sample report generation: pending execution.
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
