# UI Automation Framework Generator

## Purpose

Generate a reusable, maintainable UI test automation framework based on the user's selected tools, programming language, supporting dependencies, and design pattern.

The framework should be ready to run, easy for QA engineers to extend, and suitable for local execution and optional CI/CD integration.

---

## Inputs

Fill in the fields below. Use `AUTO_RECOMMEND` where you want the assistant to choose a compatible option. Use `NONE` for optional features you do not need.

| Input | Required | Examples / Guidance |
|---|---|---|
| `APPLICATION_URL` | Yes | `https://www.saucedemo.com/` |
| `AUTOMATION_TOOL` | Yes | `Playwright`, `Selenium`, `Cypress`, `WebdriverIO` |
| `PROGRAMMING_LANGUAGE` | Yes | `TypeScript`, `JavaScript`, `Java`, `Python`, `C#` |
| `TEST_RUNNER` | Yes | `Playwright Test`, `TestNG`, `JUnit 5`, `pytest`, `Mocha`, `AUTO_RECOMMEND` |
| `DESIGN_PATTERN` | Yes | `Page Object Model (POM)`, `Screenplay`, `Page Factory`, `NONE` |
| `BUILD_OR_PACKAGE_MANAGER` | Yes | `npm`, `Maven`, `Gradle`, `pip`, `Poetry`, `AUTO_RECOMMEND` |
| `DEPENDENCIES_AND_UTILITIES` | No | `Allure`, `Faker`, `dotenv`, `Log4j2`, `Jackson`, `AUTO_RECOMMEND`, `NONE` |
| `BROWSERS` | No | `Chromium`, `Firefox`, `WebKit`, `Chrome`, `Edge`, `AUTO_RECOMMEND` |
| `REPORTING_TOOL` | No | `Allure`, `HTML`, `ExtentReports`, `Built-in`, `AUTO_RECOMMEND` |
| `TEST_DATA_FORMAT` | No | `JSON`, `CSV`, `Excel`, `AUTO_RECOMMEND` |
| `CONFIGURATION` | No | `local`, `qa`, `staging`, `.env`, `AUTO_RECOMMEND` |
| `CI_CD_TOOL` | No | `GitHub Actions`, `Jenkins`, `GitLab CI`, `NONE` |
| `SAMPLE_TEST_SCOPE` | No | `Login and home page checks`, `AUTO_RECOMMEND` |

### User-provided configuration

```text
APPLICATION_URL: {{APPLICATION_URL}}
AUTOMATION_TOOL: {{AUTOMATION_TOOL}}
PROGRAMMING_LANGUAGE: {{PROGRAMMING_LANGUAGE}}
TEST_RUNNER: {{TEST_RUNNER}}
DESIGN_PATTERN: {{DESIGN_PATTERN}}
BUILD_OR_PACKAGE_MANAGER: {{BUILD_OR_PACKAGE_MANAGER}}
DEPENDENCIES_AND_UTILITIES: {{DEPENDENCIES_AND_UTILITIES}}
BROWSERS: {{BROWSERS}}
REPORTING_TOOL: {{REPORTING_TOOL}}
TEST_DATA_FORMAT: {{TEST_DATA_FORMAT}}
CONFIGURATION: {{CONFIGURATION}}
CI_CD_TOOL: {{CI_CD_TOOL}}
SAMPLE_TEST_SCOPE: {{SAMPLE_TEST_SCOPE}}
```

---

## Reusable Prompt

Act as a Senior UI Test Automation Architect and Framework Developer.

Create a **working UI automation framework** using the configuration supplied above.

### Step 1 — Validate selections

1. Check whether the selected automation tool, language, runner, design pattern, build manager, and reporting tools work together.
2. If a combination is unsupported, explain the conflict and propose the closest supported alternative. Do not silently change a user selection.
3. For fields set to `AUTO_RECOMMEND` or left blank, choose simple, widely supported defaults and state them.
4. Use compatible, stable dependency versions; verify exact versions when reliable package information is available. Otherwise mark versions for verification rather than inventing them.
5. Do not introduce unnecessary libraries or complicated abstractions.

### Step 2 — Design the framework

Create a clear project structure suited to the selected stack and design pattern.

Include, as appropriate:

- Test specifications / test classes
- Page objects or other selected pattern components
- Browser setup, teardown, and reusable fixtures
- Environment configuration and base URL management
- Test data files and data-reading utilities
- Reusable waits, assertions, and helper functions
- Logging, screenshots, and failure diagnostics
- Test execution reports
- Dependency and package configuration
- `.gitignore` and `README.md`
- CI/CD configuration **only if selected**

Keep test assertions in tests unless the chosen pattern or a specific reusable component justifies otherwise. Avoid hard-coded credentials and unnecessary fixed waits.

### Step 3 — Generate implementation

1. Create the actual project files, not just an architecture description.
2. Implement the chosen design pattern consistently.
3. Include at least one meaningful end-to-end UI test flow based on `SAMPLE_TEST_SCOPE` and the application URL.
4. Demonstrate navigation, element interaction, assertions, and data/configuration usage.
5. Prefer stable locators (roles, labels, test IDs, or other appropriate strategies).
6. Use environment variables or secret stores for credentials. Provide a safe example configuration without real secrets.
7. Include dependency installation, browser/driver setup, and test execution commands.
8. Make parallel execution, retries, screenshots, and tracing configurable where supported. Avoid hiding real failures behind excessive retries.
9. Do not invent application elements, credentials, or expected outcomes. If the application cannot be inspected, clearly label sample tests as templates requiring locator/behavior verification.

### Step 4 — Validate

When execution tools and application access are available:

1. Install dependencies and perform required setup.
2. Run a compile/type-check or equivalent validation.
3. Execute the sample test(s).
4. Check reports and diagnostic artifacts.
5. Fix framework-related errors and rerun, where feasible.

If execution is not available, state **Not executed** and provide exact commands for local validation. Never claim tests passed without execution evidence.

---

## Expected Output

Provide the results in this order:

1. **Selected Technology Stack** — tool, language, runner, build manager, design pattern, reporting, utilities, and any compatibility decisions.
2. **Framework Folder Structure** — readable directory tree with short descriptions of important files.
3. **Generated Framework Files** — working implementation with correct filenames and contents (or actual files in the workspace, if file creation is available).
4. **Sample Automated Test** — one representative flow showing how the framework is used.
5. **Setup and Execution Commands** — install, configure, run, filter tests, and view reports.
6. **Validation Results** — what was actually checked, passed, failed, or not executed.
7. **How to Add a New Test** — simple steps for a QA engineer to add a page/component and test.
8. **Limitations / Next Steps** — only practical, relevant items.

---

## Rules

- Follow the user's explicit technology choices whenever compatible.
- Generate a framework, not only isolated test scripts.
- Apply the selected design pattern rather than forcing POM for every project.
- Prefer simple, readable, reusable code over over-engineering.
- Keep test data, configuration, reusable UI actions, and test logic appropriately separated.
- Do not add optional dependencies or CI tools unless requested or justified.
- Never fabricate successful test execution or verified UI locators.
- Explain missing inputs and assumptions briefly, and ask a question only when a critical decision blocks implementation.

---

## Example Input — Playwright + TypeScript + POM

```text
APPLICATION_URL: https://www.saucedemo.com/
AUTOMATION_TOOL: Playwright
PROGRAMMING_LANGUAGE: TypeScript
TEST_RUNNER: Playwright Test
DESIGN_PATTERN: Page Object Model (POM)
BUILD_OR_PACKAGE_MANAGER: npm
DEPENDENCIES_AND_UTILITIES: dotenv, Faker
BROWSERS: Chromium, Firefox
REPORTING_TOOL: HTML
TEST_DATA_FORMAT: JSON
CONFIGURATION: local, qa
CI_CD_TOOL: GitHub Actions
SAMPLE_TEST_SCOPE: Valid login, inventory page title, product list visibility
```

## Example Input — Selenium + Java + POM

```text
APPLICATION_URL: https://www.saucedemo.com/
AUTOMATION_TOOL: Selenium
PROGRAMMING_LANGUAGE: Java
TEST_RUNNER: TestNG
DESIGN_PATTERN: Page Object Model (POM)
BUILD_OR_PACKAGE_MANAGER: Maven
DEPENDENCIES_AND_UTILITIES: Jackson, Log4j2
BROWSERS: Chrome, Firefox
REPORTING_TOOL: Allure
TEST_DATA_FORMAT: JSON
CONFIGURATION: local, qa
CI_CD_TOOL: Jenkins
SAMPLE_TEST_SCOPE: Valid login, invalid login, inventory page validation
```
