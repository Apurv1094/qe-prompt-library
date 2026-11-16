# Test Execution and Parallelization

## Purpose
Recreate intended test selection, isolation, retries and parallel execution behavior in the target framework.

## When to use
After a representative migrated test suite exists and before full CI rollout.

## Inputs required
- `{{SOURCE_EXECUTION_CONFIG}}` — **Required:** Existing runner configuration and commands. Example: `testng.xml and mvn test -Dgroups=smoke`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Target framework location. Example: `D:\QA\playwright-tests`.
- `{{EXECUTION_REQUIREMENTS}}` — **Required:** Required browsers, groups, worker limits, retries and environment rules. Example: `Chromium; smoke/regression; 2 CI workers; retry failures once`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Recreate intended test selection, isolation, retries and parallel execution behavior in the target framework.

Inputs:
SOURCE_EXECUTION_CONFIG:
{{SOURCE_EXECUTION_CONFIG}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
EXECUTION_REQUIREMENTS:
{{EXECUTION_REQUIREMENTS}}

Instructions:
1. Inspect source suite definitions, groups, setup/teardown, parallel settings, retries, and environment selection.
2. Map source behavior to target runner projects, tags, fixtures, workers, and retry configuration.
3. Identify shared data, global state, order dependence, and collision risks before enabling parallel runs.
4. Implement target execution configuration and documented commands for smoke, regression, and selected tests.
5. Use retries for diagnostics rather than hiding unstable tests; avoid inventing equivalent runner semantics.
6. Execute a representative serial and parallel comparison only when authorized; report actual results and limitations.

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
1. Execution setting mapping and updated configuration.
2. Commands for local, CI, smoke and regression execution.
3. Isolation/parallel safety findings.
4. Serial-vs-parallel validation evidence and open risks.

## Example
**Synthetic input:**
```text
SOURCE_EXECUTION_CONFIG: testng.xml and mvn test -Dgroups=smoke
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
EXECUTION_REQUIREMENTS: Chromium; smoke/regression; 2 CI workers; retry failures once
```

**Illustrative output (synthetic; not an actual execution result):**
```text
Mapped groups to @smoke/@regression tags; workers=2 in CI; documented npx playwright test --grep @smoke. Parallel run: pending.
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
