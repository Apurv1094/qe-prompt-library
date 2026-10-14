# UI Automation Prompt Guide
**QE Prompt Library | Owner:** QE Automation Team | **Version:** 3.0 | **Updated:** 14 October 2026

## What this guide helps you do

Use these ready-to-copy prompts with an AI assistant to **create, improve, troubleshoot, and maintain UI automation**. You do not need to write prompts from scratch.

This guide is for QA Engineers, SDETs, and developers working with tools such as Selenium, Playwright, or Cypress.

## Start here: choose what you want to do

| If you want to… | Use this |
|---|---|
| Create a new automation framework | [Framework Master Prompt](#1-build-a-new-framework) |
| Add a page or automate a manual test | [P-04 Page Object](#p-04-create-a-page-object), [P-05 Manual Test to Automation](#p-05-convert-a-manual-test-to-automation) |
| Fix an unreliable test | [P-07 Fix a Flaky Test](#p-07-fix-a-flaky-test) |
| Improve a locator | [P-08 Improve Locators](#p-08-improve-locators) |
| Add reporting or failure screenshots | [P-09 Reporting and Failure Evidence](#p-09-add-reporting-and-failure-evidence) |
| Set up CI/CD | [P-12 CI/CD Pipeline](#p-12-create-a-cicd-pipeline) |
| Review code before merging | [P-14 Code Review](#p-14-review-and-refactor-code) |
| Write onboarding documentation | [P-15 README](#p-15-create-a-beginner-friendly-readme) |

## Quick start: use any prompt in 4 steps

1. **Choose a task** from the table above.
2. **Fill in the placeholders** such as `{{TOOL}}` and `{{LANGUAGE}}`. Replace every placeholder that applies to your task.
3. **Add the Standard Rules** from the next section to the end of your prompt.
4. **Run, review, and test** the AI-generated code before using or merging it.

If a field does not apply, enter `N/A`. If you do not know an optional setting, ask the AI to recommend a sensible default and clearly state its assumption.

### Important safety rules

- Never paste real passwords, access tokens, customer information, or confidential internal URLs. Use dummy examples instead.
- Do not assume generated code is correct. Build it, run it, inspect the results, and review it before merging.
- Never commit credentials, authentication state, or other secrets to source control.

---

## 1. Set up your project details

Fill this in once, then reuse the values across prompts. Most tasks only need the details relevant to that task.

| Placeholder | What it means | Example |
|---|---|---|
| `{{APP}}` | Application type/name | Web application, Banking Portal |
| `{{TOOL}}` | Automation tool | Selenium, Playwright, Cypress |
| `{{LANGUAGE}}` | Programming language/version | Java 17, TypeScript, Python 3.12 |
| `{{RUNNER}}` | Test runner or BDD tool | TestNG, pytest, Playwright Test, Cucumber |
| `{{BUILD}}` | Build/package tool | Maven, npm, pip |
| `{{DESIGN}}` | Framework design | Page Object Model (POM), POM + BDD |
| `{{BROWSERS}}` | Browsers to support | Chrome, Firefox, Edge |
| `{{EXECUTION}}` | Where tests will run | Local machine, Docker, Grid, Cloud |
| `{{REPORTING}}` | Reporting tool | Allure, Extent, HTML |
| `{{CICD}}` | Pipeline tool | Jenkins, GitHub Actions |
| `{{SCENARIOS}}` | Two or three example scenarios | Login, search, checkout |
| `{{CONSTRAINTS}}` | Mandatory restrictions | Open-source libraries only |
| `{{OPTIONAL_EXTRAS}}` | Any extra project requirements | Excel data, parallel threads, environments, logging |

Optional details might include the data source (Excel/CSV/JSON), number of parallel threads, environments (QA/Staging), configuration format, logging library, coding standards, retries, or API-based login. Include only the details that matter to your project.

## 2. Standard Rules — add these to every prompt

Copy this block and paste it at the end of the prompt you choose.

```text
STANDARD RULES
- Keep tests independent; do not rely on execution order.
- Store locators in page objects; keep assertions in tests.
- Prefer locators in this order: data-testid > id > role/accessible name > CSS > XPath (last resort).
- Do not use fixed sleeps. Use explicit waits or the tool's auto-waiting.
- Read URLs and secrets from configuration/environment variables or a vault. Never hardcode or log secrets.
- Make driver/browser handling safe for parallel execution.
- Keep the solution simple; avoid unnecessary dependencies and abstractions.
- Do not invent application-specific details. List important assumptions first (maximum 5 lines), then continue.
- Show the file path before each code file and provide complete, runnable code.
- Mark project-specific changes with TODO.
```

---

## 3. Build a new framework

### Framework Master Prompt

Use this when starting a new UI automation framework. The AI will deliver one phase at a time, so you can review and run each phase before asking it to continue.

Copy the prompt below, replace the placeholders, and add the Standard Rules.

```text
ROLE
Act as a Senior QA Automation Architect.

GOAL
Build a UI automation framework in phases. Complete only ONE phase at a time.
After each phase, stop and wait until I reply "continue".

PROJECT DETAILS
- Application: {{APP}}
- Automation tool / language: {{TOOL}} / {{LANGUAGE}}
- Test runner / build tool: {{RUNNER}} / {{BUILD}}
- Framework design: {{DESIGN}}
- Browsers / execution: {{BROWSERS}} / {{EXECUTION}}
- Reporting: {{REPORTING}}
- CI/CD: {{CICD}}
- Sample scenarios: {{SCENARIOS}}
- Constraints: {{CONSTRAINTS}}
- Optional extras: {{OPTIONAL_EXTRAS}}

PHASES
1. Foundation
   Explain the architecture briefly with a simple text diagram. Provide the
   folder structure, dependencies, configuration (including CLI/environment
   overrides), driver/browser factory, BasePage, and BaseTest.

2. Pages and Tests
   Create sample page objects and tests for the listed scenarios. Add a data
   reader and sample data file if a data source was requested.

3. Quality and Evidence
   Add logging, reporting, and screenshots on failure (plus video/trace if
   supported). Add retries only if requested; retries must be opt-in per test
   and must not hide real defects.

4. Pipeline and Documentation
   Create the CI/CD pipeline for smoke and regression tests, including
   environment/browser/tag parameters, report and artifact publishing, and
   clear failure rules. Write a short README covering setup, run commands,
   adding pages/tests, and troubleshooting.

At the end of each phase, include "Next step / Known limitations" in no more
than 5 lines.

[Paste STANDARD RULES here]
```

---

## 4. Prompts for Everyday Tasks

Use these prompts to add, improve, troubleshoot, and maintain UI automation in an **existing automation framework**.

For each task, describe the outcome you want. The AI should inspect the existing project, discover relevant implementation details, and reuse available components instead of asking you to supply information it can find itself.

### Standard Rules — Apply to Every Prompt

Add these rules at the end of each prompt.

```text
STANDARD RULES
- Inspect the existing framework, relevant files, dependencies, and coding
  conventions before making changes.
- Discover technical details from the project and available tools instead
  of asking the user to provide information that can be found.
- Reuse existing components and patterns. Do not rebuild the framework,
  duplicate utilities, or introduce unnecessary dependencies.
- Make focused changes and preserve unrelated functionality.
- Do not invent application details or claim an inspection, change, or test
  was completed if it was not.
- If required information cannot be discovered, ask only for the minimum
  information needed to proceed.
- Provide the complete code for created or modified files and show their paths.
- Run relevant validation checks when possible. Clearly report passed,
  failed, and unexecuted checks.
- Protect credentials, authentication state, and sensitive test data.
- Summarize the changes, validation results, assumptions, and remaining
  actions required from the user.
```

---

### Setup

#### P-01: Create or Update Configuration

```text
Review the existing configuration management in this automation framework.

Task:
{{CONFIGURATION_NEED}}

Inspect how the project currently handles environments, configuration files,
overrides, and required settings.

Implement the requested configuration change by extending the existing
approach. Support CLI arguments, system properties, or environment variables
where appropriate for the current framework.

Handle missing required values clearly, preserve thread safety where needed,
and protect sensitive configuration values.

Provide the complete code for modified or new files, explain how the
configuration works, and show how to run or validate it.
```

#### P-02: Create or Update Driver / Browser Factory

```text
Review the existing browser/driver factory and test lifecycle.

Task:
{{DRIVER_OR_BROWSER_NEED}}

Inspect the current framework to identify supported browsers, execution modes,
driver setup, configuration, and test runner integration.

Implement the requested change by extending the existing factory and
lifecycle management. Preserve current capabilities, support headless or
remote execution where required, and ensure browser resources are released
safely even when a test fails.

Avoid creating a duplicate factory or changing unrelated tests.

Provide the complete code, required configuration changes, run instructions,
and validation results.
```

#### P-03: Create or Update Reusable Base Page

```text
Review the existing BasePage or equivalent reusable interaction layer.

Task:
{{REUSABLE_ACTION_NEED}}

Inspect the current framework to identify existing actions, wait strategies,
logging, error handling, screenshot capture, and frame/window management.

Implement the requested functionality using the existing patterns. Check
whether a reusable action already exists before adding another one.

Use appropriate waits and error handling. Introduce a JavaScript interaction
fallback only when justified, not as a default workaround.

Provide the complete code, explain how page objects should use it, and report
the validation results.
```

---

### Create Tests

#### P-04: Create or Update a Page Object

```text
Create or update the Page Object for the "{{PAGE_NAME}}" page in the
existing automation framework.

Page details:
- URL: {{PAGE_URL_OR_NA}}
- Task / expected user behavior: {{TASK_OR_EXPECTED_BEHAVIOR}}

Instructions:
1. Inspect the existing framework and follow its page-object conventions.
2. Use available browser automation tools to inspect the page and identify
   relevant interactive elements, labels, inputs, buttons, and page structure.
3. Identify stable locators from the actual page. Prefer stable test attributes,
   IDs, accessible roles/names, CSS, and XPath as a last resort.
4. Create reusable methods representing user actions. Keep locators in the
   Page Object and assertions in tests, following project conventions.
5. Reuse existing utilities and avoid unnecessary getters, abstractions,
   dependencies, or duplicate methods.
6. If an action navigates to another page, return the next Page Object only
   after confirming navigation has completed, where appropriate.
7. Validate locator uniqueness and behavior where possible. Do not invent
   elements or claim validation was performed if it was not.
8. If browser inspection is unavailable, use available DOM/HTML or request
   the minimum information needed to identify the elements accurately.

Provide the complete code, expected file path, assumptions, and validation
results.
```

#### P-05: Convert a Manual Test to Automation

```text
Convert the following manual test into an automated test using the existing
automation framework.

Manual test / scenario:
{{MANUAL_TEST_OR_SCENARIO}}

Expected result, if not already specified:
{{EXPECTED_RESULT_OR_NA}}

Relevant URLs(if not covered in the test case):
{{URLS}}

Instructions:
1. Inspect the existing test structure, page objects, setup/cleanup hooks,
   test-data handling, and naming conventions.
2. Reuse existing components and identify any missing page actions.
3. Create a clearly named automated test with one primary objective.
4. Follow existing assertion, test-data, and reporting conventions.
5. If the framework uses BDD, follow its existing feature-file and
   step-definition patterns. Use Scenario Outline and tags where appropriate.
6. Identify missing requirements or expected results instead of inventing
   business rules.

Provide the complete code, changed file paths, and instructions to run the test.
```

#### P-06: Create or Update Data-Driven Tests

```text
Review the existing framework's test-data management and data-driven testing
approach.

Test or scenario:
{{TEST_OR_SCENARIO}}

Task:
{{DATA_COVERAGE_NEED}}

Inspect the existing data sources, readers, test runner, and reporting
conventions.

Extend the current approach to cover relevant positive, negative, and boundary
cases. Create or update data files and readers only where needed.

Handle missing or malformed data clearly. Make test results traceable to the
corresponding data case. If generated test data is required, use a repeatable
approach consistent with the existing framework.

Provide the complete code, sample data, changed file paths, and run instructions.
```

---

### Fix Test Stability and Locators

#### P-07: Fix a Flaky Test

Use this prompt when a test passes sometimes and fails at other times.

```text
Investigate and fix an intermittently failing test in the existing framework.

Test name or location:
{{TEST_NAME_OR_PATH}}

Observed failure, error, or logs, if available:
{{ERROR_OR_LOGS_OR_NA}}

Inspect the test, related page objects, waits, application state, test data,
browser/environment, animations, stale elements, and parallel execution
where relevant.

Reproduce the failure if the environment permits. Identify and rank likely
causes, distinguishing confirmed evidence from hypotheses.

Fix the root cause where possible. Do not use fixed sleeps, broad exception
handling, or retries to hide the failure.

Provide the corrected code, explain what changed, and report whether the
failure was reproduced and which validation checks were completed.
If the cause cannot be confirmed, explain the evidence needed next.
```

#### P-08: Improve Locators

```text
Review locator stability in the existing automation framework.

Page, test, or area to review:
{{PAGE_OR_TEST_OR_NA}}

Inspect the existing page objects and use available browser tools to examine
the current DOM and relevant elements.

Identify fragile locators and replace them with stable alternatives grounded
in the actual page structure. Follow project conventions and prefer stable
test attributes, IDs, accessible roles/names, CSS, and XPath as a last resort.

Validate locator uniqueness where possible. Explain why each changed locator
is more reliable.

If no reliable locator can be identified, recommend the specific DOM or
test-attribute change needed from the development team.

Provide the complete changed code and validation results. Do not invent
elements or claim a locator was validated if it was not.
```

---

### Reporting, Execution, and CI/CD

#### P-09: Add or Update Reporting and Failure Evidence

```text
Review the existing reporting and failure-evidence implementation.

Task:
{{REPORTING_NEED}}

Inspect the current reporting tool, test listeners/hooks, logging, screenshot
capture, and supported video/trace capabilities.

Extend the existing setup to meet the requirement. Attach failure evidence
to reports where supported, follow existing naming conventions, and implement
retention or cleanup only when needed.

Avoid introducing a second reporting system unless there is a clear reason.

Provide the complete code, configuration changes, instructions to generate
and view reports, and validation results.
```

#### P-10: Add an Optional Retry Mechanism

Use retries only when justified. They must not hide genuine defects.

```text
Review the existing test runner and determine whether retry support already
exists.

Requirement:
{{RETRY_NEED}}

If retries are justified, extend the current mechanism or implement an
opt-in solution consistent with the framework.

Retry only explicitly eligible tests, using a configurable retry limit.
Log each attempt and identify retried tests in the report where supported.

Do not use retries to replace root-cause investigation or conceal genuine
application defects. If retries are unsuitable, explain why and recommend
an alternative.

Provide the complete code, instructions to enable retries, and validation
results.
```

#### P-11: Set Up Parallel and Cross-Browser Execution

```text
Review the existing test execution configuration and parallel-safety.

Task:
{{EXECUTION_REQUIREMENT}}

Inspect the current test runner, supported browsers, driver lifecycle,
shared state, test data, and any existing Grid, Docker, or cloud setup.

Extend the current configuration to support the requested execution modes.
Avoid shared mutable state, resource conflicts, and dependencies between tests.

Check whether the existing tests are safe for parallel execution before
enabling it broadly. Do not assume that increasing thread count is sufficient.

Provide the complete code and configuration changes, commands for the
required execution modes, troubleshooting guidance, and validation results.
```

#### P-12: Create or Update a CI/CD Pipeline

```text
Review the existing CI/CD pipeline and automation framework's run commands.

Task:
{{PIPELINE_REQUIREMENT}}

Identify the current pipeline platform, build process, test commands,
environment configuration, reporting, and artifact handling.

Extend the existing pipeline to meet the requirement. Include relevant steps
such as dependency caching, build/lint, smoke and regression execution,
browser/environment/tag parameters, report publishing, failure evidence,
scheduling, and notifications where needed.

Use the project's existing secret-management approach. Define clear failure
conditions and preserve unrelated pipeline behavior.

Provide the complete pipeline changes, explain how to trigger the workflow,
and report validation results. Do not claim the pipeline executed unless
it actually ran.
```

#### P-13: Reuse a Login Session

```text
Review the existing authentication and session-management approach in this
automation framework.

Task:
{{SESSION_REUSE_REQUIREMENT}}

Determine whether repeated UI login can be reduced safely using a supported
API login or the automation tool's session-state capabilities.

Reuse existing authentication utilities where possible. Preserve a dedicated
test for the actual UI login flow. Handle session expiry and refresh where
required by the application.

Protect authentication state and credentials. Never commit secrets or
session files to source control.

If the application or environment does not support a safe approach, explain
the limitation before implementing an assumption.

Provide the complete code, configuration changes, instructions, and
validation results.
```

---

### Review and Document Your Framework

#### P-14: Review and Refactor Code

```text
Act as a Senior QA Automation Engineer and review the following code or change
in the context of the existing framework.

File, class, test, or change:
{{CODE_LOCATION_OR_CHANGE}}

Inspect the relevant implementation and project conventions before
recommending changes.

Review applicable areas such as locator stability, waits, assertions,
duplication, hardcoded data, configuration, thread safety, error handling,
naming, maintainability, and security.

First provide a table with:
Issue | Severity (High/Medium/Low) | File/Location | Recommended Fix

Then provide a focused refactor where appropriate. Preserve existing
behavior unless a change is necessary, and explain any behavior changes.

Do not refactor unrelated files or introduce unnecessary abstractions.
Provide the complete changed code and validation results.
```

#### P-15: Create or Update a Beginner-Friendly README

```text
Review the existing README, project structure, configuration, and test
execution commands.

Documentation task:
{{DOCUMENTATION_REQUIREMENT}}

Update the existing documentation rather than creating a duplicate guide.

Document the topics relevant to the project, such as prerequisites, setup,
folder structure, commands to run tests by browser/environment/tag, adding
page objects and tests, managing test data, reporting, CI/CD, coding
conventions, and troubleshooting.

Verify instructions against the actual project wherever possible. Clearly
identify anything that could not be verified instead of inventing commands
or configuration details.

Provide the complete updated README, its file path, and a summary of changes.
```

---

### Optional Prompts — Use Only When Needed

#### P-16: Add Accessibility Checks

```text
Review the existing automation framework and determine how accessibility
checks can be added consistently.

Pages or flows:
{{PAGES_OR_FLOWS}}

Task:
{{ACCESSIBILITY_REQUIREMENT}}

Inspect the existing tool, language, test runner, reporting, and dependencies.
Reuse the current setup and integrate axe-core or a compatible alternative
where appropriate.

Report accessibility violations clearly and support documented exclusions
only when each exclusion has a written justification. Do not silently
suppress violations.

Provide the complete code, required configuration, instructions to run the
checks, and validation results.
```

#### P-17: Add Visual Regression Testing

```text
Review the existing framework for visual comparison or screenshot-testing
capabilities.

Pages or flows:
{{PAGES_OR_FLOWS}}

Task:
{{VISUAL_REGRESSION_REQUIREMENT}}

Extend the existing setup or recommend a compatible approach if the required
capability is missing.

Where relevant, implement baseline creation, comparison thresholds, masking
of dynamic content, failure diff images, and a controlled process for
reviewing and approving baseline updates.

Do not automatically approve changed baselines. Explain setup requirements,
the files changed, how to run the checks, and the validation results.
```

#### P-18: Plan or Execute a Framework Migration

```text
Review the existing automation framework and assess the migration request.

Migration goal:
{{MIGRATION_GOAL}}

Inspect the current tool, language, framework architecture, dependencies,
test coverage, page objects, test-data handling, reporting, and CI/CD.

If the target tool or language has already been decided, use that target.
Otherwise, recommend suitable options with their trade-offs and ask for a
decision only if it is necessary to proceed.

Provide a phased migration plan covering reusable components, required
changes, compatibility, risks, coexistence of old and new implementations,
and estimated effort.

If implementation is requested, migrate one representative example first,
validate it, and then recommend the next step.

Do not assume that every component must be rewritten. Identify what can
be reused and explain any limitations.
```

---

### Recommended Usage

1. Select the prompt that matches your task.
2. Describe the outcome you want. Provide only details that the AI cannot discover.
3. Allow the AI to inspect the existing code and application using available tools.
4. Review the changes and validation results before merging.
5. Ask for clarification only when necessary information is genuinely unavailable.

## 5. Example: project details already filled in

Use this as a reference for how to fill in the project details.

```text
ROLE
Act as a Senior QA Automation Architect.

GOAL
Build a UI automation framework in phases. Complete one phase at a time and
wait for me to reply "continue" before moving on.

PROJECT DETAILS
- Application: Web, Banking Portal
- Automation tool / language: Selenium WebDriver / Java 17
- Test runner / build tool: TestNG + Cucumber / Maven
- Framework design: POM + BDD
- Browsers / execution: Chrome, Firefox, Edge / Local + Selenium Grid
- Reporting: Allure
- CI/CD: Jenkins
- Sample scenarios: Login, fund transfer, statement download
- Constraints: Open-source libraries only
- Optional extras: Excel data, 4 parallel threads, QA + Staging,
  .properties configuration, Log4j2, Google Java Style, retry once, API login

PHASES
Use the four phases in the Framework Master Prompt above.

[Paste STANDARD RULES here]
```

---

## 6. Before using AI-generated code: review checklist

Do not merge generated code until the relevant checks are complete.

### Does it work?
- [ ] The project builds and tests run using the documented commands.
- [ ] Parallel execution was actually tested, if required.

### Is the code maintainable?
- [ ] Locators are stable and stored in page objects.
- [ ] No fixed sleeps; appropriate explicit waits or auto-waiting are used.
- [ ] Assertions are in tests, and tests are independent.
- [ ] Test data and configuration are separate from test logic.
- [ ] There are no unnecessary dependencies.

### Is it safe and is the evidence available?
- [ ] Screenshots/logs are attached to the report on failure.
- [ ] Credentials are neither hardcoded nor logged.
- [ ] Real customer data and authentication state are not committed.

### Are pipeline and documentation ready?
- [ ] CI runs and publishes reports/artifacts with clear failure rules.
- [ ] The README works on a clean machine.

---

## 7. Tips for getting better results

| Do this | Avoid this |
|---|---|
| State the role, task, inputs, and expected output. | Asking only “create an automation framework.” |
| Include the DOM for locator issues and logs for failures. | Asking “why is this failing?” without evidence. |
| Work in small steps and run each step before continuing. | Generating everything at once and merging without review. |
| Specify tool and language versions. | Accepting outdated APIs without checking. |
| Ask the AI to list assumptions. | Assuming the AI knows your project standards. |

## 8. Suggested workflow for a new framework

1. Start with the **Framework Master Prompt** and complete Phases 1–4 one at a time.
2. Use **P-04** and **P-05** when adding pages and tests.
3. Use **P-06** if your tests need multiple data sets.
4. Use **P-07** or **P-08** when tests become unstable or locators break.
5. Use **P-14** for a code review before merging.
6. Add optional prompts **P-16 to P-18** only when the project needs them.

## Change log

| Version | Date | Updates |
|---|---|---|
| 1.0 | 8 October 2026 | Initial release |
| 2.0 | 14 October 2026 | Reduced core parameters, consolidated shared rules, introduced phased framework creation, and reduced the number of task prompts |
| 3.0 | 14 October 2026 | Reorganized for task-based navigation, simplified instructions, explained placeholders, and clarified when and how to use each prompt |
