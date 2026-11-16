# Framework Assessment and Migration Plan

## Purpose
Assess an existing test automation framework and prepare a structured migration plan for transitioning to a target framework while preserving test coverage and reusable components.

## When to use
Use before starting an automation framework migration to understand the existing implementation, identify migration gaps and risks, and determine the required migration activities.

## Inputs required
- `{{EXISTING_FRAMEWORK_PATH}}` — **Required:** Path to the existing automation framework repository. Example: `D:\Automation\selenium-framework`.
- `{{TARGET_FRAMEWORK}}` — **Required:** Framework and programming language to migrate to. Example: `Playwright with TypeScript`.
- `{{MIGRATION_SCOPE}}` — **Required:** Components or functionality included in the migration. Example: `Complete migration of framework structure, POM, utilities, test data, test scripts, reporting and CI/CD`.

## Prompt

```text
Role: Act as a Senior QA Automation Architect.

Task: Assess the existing test automation framework and prepare a practical, evidence-based migration plan for the target framework.

Inputs:
EXISTING_FRAMEWORK_PATH:
{{EXISTING_FRAMEWORK_PATH}}

TARGET_FRAMEWORK:
{{TARGET_FRAMEWORK}}

MIGRATION_SCOPE:
{{MIGRATION_SCOPE}}

Instructions:

1. Existing Framework Assessment
   - Inspect the existing repository and its folder structure.
   - Identify the automation tool, programming language, test runner, build tool and relevant dependencies.
   - Review existing configuration files and execution setup.
   - Identify the framework architecture and design patterns.

2. Framework Component Inventory
   - Identify existing test scripts and test suites.
   - Identify Page Object Model classes, base classes, fixtures and reusable components.
   - Identify test data files, utilities, configuration, reporting and logging mechanisms.
   - Identify CI/CD pipeline files and execution commands.
   - Record the relevant file paths for each identified component.

3. Target Framework Assessment
   - Identify the target framework's capabilities and architectural requirements.
   - Determine the recommended target project structure.
   - Identify differences in language, test execution, configuration, assertions and dependency management.
   - Highlight any target framework decisions requiring confirmation.

4. Migration Gap Analysis
   - Compare existing components against the target framework.
   - Classify each component as Reuse, Convert, Redesign, Replace or Retire.
   - Explain the reason for each migration decision.
   - Identify unsupported dependencies, compatibility concerns and missing capabilities.

5. Test Coverage Assessment
   - Inventory existing automated tests and their functional areas.
   - Identify critical workflows, test groups and execution dependencies.
   - Highlight test coverage that must be preserved during migration.
   - Identify coverage information that cannot be verified from available evidence.

6. Migration Risk Assessment
   - Identify technical and functional migration risks.
   - Assess risks related to dependencies, utilities, execution behavior, test data and coverage preservation.
   - Assign High, Medium or Low risk levels with justification.
   - Recommend mitigation actions.

7. Migration Effort and Prioritization
   - Classify migration activities by relative complexity: High, Medium or Low.
   - Identify prerequisites and dependencies between activities.
   - Prioritize components based on technical dependencies, business criticality and migration risk.
   - Avoid unsupported time or resource estimates.

8. Migration Roadmap
   - Prepare a phased migration plan covering:
     a. Framework structure
     b. Dependencies and build setup
     c. Framework configuration
     d. Design patterns
     e. Test data
     f. Utilities and helpers
     g. Test scripts
     h. Execution and parallelization
     i. Reporting and logging
     j. CI/CD integration
     k. Migration validation and cleanup
   - Define the expected deliverable and validation checkpoint for each phase.
   - Identify activities that require approval or additional information.

Rules:
- Inspect existing project files before making recommendations.
- Use the actual repository implementation as the primary source of evidence.
- Do not assume the source framework's technology stack or architecture.
- Do not invent missing files, test coverage, dependencies or execution results.
- Clearly distinguish verified findings, recommendations and assumptions.
- Preserve existing business validations and automated test coverage.
- Recommend reuse where practical instead of unnecessary redesign.
- Do not generate, modify, delete or migrate code during this assessment.
- Do not execute tests or install dependencies without authorization.
- Request missing mandatory information when it cannot be determined.
- Protect credentials, tokens and sensitive test data.
- Follow the central QE Prompt Library data-privacy guardrails.
```

## Expected output

Generate a **Framework Migration Assessment Report** containing:

1. **Existing Framework Summary** — Identified technology stack, architecture, dependencies and configuration, with supporting file references.
2. **Framework Component Inventory** — Existing test scripts, page objects, utilities, test data, reports and CI/CD components with their locations.
3. **Target Framework Overview** — Proposed target architecture, tooling and key implementation differences.
4. **Migration Gap Analysis** — Component-wise migration decisions (Reuse, Convert, Redesign, Replace or Retire) with reasons.
5. **Test Coverage Assessment** — Existing test inventory, critical workflows and coverage-preservation requirements.
6. **Migration Risk Register** — Identified risks, severity, impact and mitigation recommendations.
7. **Migration Complexity and Priorities** — Relative effort, dependencies and recommended implementation priorities.
8. **Migration Roadmap** — Ordered migration activities, expected deliverables and validation checkpoints.
9. **Open Questions and Assumptions** — Missing information, unverified findings and decisions requiring confirmation.

## Example

**Synthetic input:**

```text
EXISTING_FRAMEWORK_PATH:
D:\Automation\selenium-framework

TARGET_FRAMEWORK:
Playwright with TypeScript

MIGRATION_SCOPE:
Complete migration including framework structure, POM,
test scripts, test data, utilities, reporting and CI/CD.
```

**Illustrative output:**

*Assume the repository inspection identified the following components.*

**1. Existing Framework Summary**

| Component | Existing implementation |
|---|---|
| Automation Tool | Selenium WebDriver |
| Programming Language | Java |
| Test Runner | TestNG |
| Build Tool | Maven |
| Design Pattern | Page Object Model |
| Configuration | `config.properties`, `testng.xml` |
| CI/CD | Jenkins |

**2. Migration Gap Analysis**

| Component | Migration Decision | Recommended Approach |
|---|---|---|
| Framework Structure | Redesign | Adopt Playwright TypeScript project structure |
| Page Objects | Convert | Convert Java page classes to TypeScript |
| Test Scripts | Convert | Migrate TestNG tests to Playwright test specifications |
| Test Data | Reuse/Adapt | Preserve JSON datasets and adapt data-loading logic |
| Configuration | Convert | Use `playwright.config.ts` and environment configuration |
| Utilities | Review/Convert | Replace Selenium-specific helpers with Playwright-compatible utilities |
| Reporting | Replace/Integrate | Configure Playwright reporting and retain required integrations |
| CI/CD | Modify | Update Jenkins setup and execution commands |

**3. Migration Risk Assessment**

| Risk | Priority | Mitigation |
|---|---|---|
| Selenium-specific utility dependencies | High | Review and replace incompatible implementations |
| Loss of existing test coverage | High | Map source tests to migrated tests |
| Test data compatibility | Medium | Validate existing datasets against target tests |
| Execution configuration differences | Medium | Validate browser, retry and parallel execution settings |

**4. Migration Roadmap (Excerpt)**

| Phase | Activity | Deliverable |
|---|---|---|
| 01 | Framework Assessment | Migration assessment report |
| 02 | Framework Structure Migration | Target project structure |
| 03 | Dependencies and Build Setup | Target dependency and build configuration |
| 04 | Framework Configuration Migration | Target framework configuration |
| 05 | Design Pattern Migration | Migrated Page Object Model |
| 06 | Test Data Migration | Compatible test data and fixtures |

**5. Assessment Conclusion**

The example framework requires migration of its Selenium-specific components to Playwright-compatible implementations. Existing business scenarios and reusable test data should be preserved wherever feasible.

The next recommended activity is **02-Framework-Structure-Migration**, following approval of the migration assessment.

## Limitations
- Repository access is required to inspect the existing framework accurately.
- Static code inspection cannot confirm runtime behavior, test stability or execution compatibility.
- Migration recommendations depend on the completeness of available source code, configurations and documentation.
- Complexity assessments are indicative and should not be treated as committed delivery estimates.
- Sensitive configuration values, credentials and test data must not be exposed in assessment reports.
- Final architecture, migration scope and priorities require review and approval from the responsible QE or engineering team.

## Owner / Version
- Owner: QE Automation Team
- Version: 1.0.0