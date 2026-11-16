# Migration Validation and Cleanup

## Purpose
Verify migration completeness against the source baseline and safely retire legacy framework components after approval.

## When to use
After all planned migration components are implemented and before switching the team to the target framework.

## Inputs required
- `{{SOURCE_BASELINE}}` — **Required:** Source test inventory, baseline results and acceptance criteria. Example: `artifacts/framework-migration-assessment.md and baseline-results.csv`.
- `{{TARGET_REPOSITORY_PATH}}` — **Required:** Migrated target framework to validate. Example: `D:\QA\playwright-tests`.
- `{{VALIDATION_SCOPE}}` — **Required:** Required coverage, environments, suites and exit criteria. Example: `All critical login and checkout tests; Chromium; CI green`.
- `{{CLEANUP_APPROVAL}}` — **Required:** Approval status for removing legacy files or dependencies. Example: `Pending QE lead approval`.

## Prompt
```text
Role: Act as a Senior QA Automation Architect.
Task: Verify migration completeness against the source baseline and safely retire legacy framework components after approval.

Inputs:
SOURCE_BASELINE:
{{SOURCE_BASELINE}}
TARGET_REPOSITORY_PATH:
{{TARGET_REPOSITORY_PATH}}
VALIDATION_SCOPE:
{{VALIDATION_SCOPE}}
CLEANUP_APPROVAL:
{{CLEANUP_APPROVAL}}

Instructions:
1. Compare source and target test IDs, business assertions, coverage, data scenarios, and known exclusions.
2. Validate target configuration, dependency installation, representative executions, CI results, and report artifacts using available evidence.
3. Classify gaps as migrated/verified, migrated/unverified, blocked, intentionally retired, or missing.
4. Investigate failures and distinguish migration defects from existing product defects and environmental issues.
5. Produce a go/no-go recommendation based on explicit exit criteria; never infer success from file existence alone.
6. List legacy files/dependencies eligible for retirement, but do not delete them without explicit approval and rollback readiness.

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
1. Coverage parity matrix and execution evidence.
2. Unresolved defects, gaps and accepted exclusions.
3. Exit-criteria checklist and go/no-go recommendation.
4. Cleanup candidates, approvals and rollback notes.

## Example
**Synthetic input:**
```text
SOURCE_BASELINE: artifacts/framework-migration-assessment.md and baseline-results.csv
TARGET_REPOSITORY_PATH: D:\QA\playwright-tests
VALIDATION_SCOPE: All critical login and checkout tests; Chromium; CI green
CLEANUP_APPROVAL: Pending QE lead approval
```

**Illustrative output (synthetic; not an actual execution result):**
```text
Coverage: 19/20 mapped, 18 passed, 1 blocked, 1 missing. Recommendation: NO-GO until missing test and blocker are resolved. Cleanup: not performed.
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
