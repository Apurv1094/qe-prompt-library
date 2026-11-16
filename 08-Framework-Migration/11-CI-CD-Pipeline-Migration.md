# CI/CD Pipeline Migration

## Purpose
Update CI/CD automation to install, execute and publish results for the target framework without disrupting existing delivery controls.

## When to use
After local target execution and reporting have been validated.

## Inputs required
- `{{SOURCE_PIPELINE_PATH}}` — **Required:** Current CI pipeline definition. Example: `Jenkinsfile`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Target framework and pipeline directory. Example: `D:\QA\playwright-tests`.
- `{{CI_REQUIREMENTS}}` — **Required:** CI platform, triggers, credentials, environments and reporting requirements. Example: `Jenkins Windows agent; PR builds; smoke suite; JUnit reports`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Update CI/CD automation to install, execute and publish results for the target framework without disrupting existing delivery controls.

Inputs:
SOURCE_PIPELINE_PATH:
{{SOURCE_PIPELINE_PATH}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
CI_REQUIREMENTS:
{{CI_REQUIREMENTS}}

Instructions:
1. Inspect source pipeline stages, triggers, agents, tool versions, secrets, parameters, artifacts, and quality gates.
2. Map source stages to target install, browser provisioning, test execution, and report publication steps.
3. Update pipeline using supported target commands and least-privilege secret injection; preserve unrelated release gates.
4. Add explicit failure handling, artifact archiving, and report publication; avoid masking test failures.
5. Check agent OS/runtime compatibility, caching, and browser dependencies; note unverified infrastructure assumptions.
6. Validate syntax and run CI only when authorized; provide rollback and cutover considerations.

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
1. Old-to-new pipeline stage mapping.
2. Updated pipeline file and environment prerequisites.
3. Artifact/report publication and secret handling summary.
4. CI verification evidence, rollback plan and open blockers.

## Example
**Synthetic input:**
```text
SOURCE_PIPELINE_PATH: Jenkinsfile
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
CI_REQUIREMENTS: Jenkins Windows agent; PR builds; smoke suite; JUnit reports
```

**Illustrative output (synthetic; not an actual execution result):**
```text
Updated Test stage to npm ci, npx playwright install, npx playwright test --grep @smoke; JUnit XML archived. Jenkins build: not executed.
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
