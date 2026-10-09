# QE Prompt Library: UI Automation Framework Development

**Owner:** QE Automation Team  
**Audience:** QE / SDET / Development Teams  
**Version:** 1.0

---

## 1. How to Use This Library

1. Fill in the **Input Parameter Sheet** in Section 2.
2. If something does not apply, enter `N/A`.
3. For a complete framework, use the **Master Prompt** in Section 3 first.
4. For smaller daily tasks, use the **Micro Prompts** in Section 4.
5. Review every AI-generated output using the **Review Checklist** in Section 6 before committing it.

### Important Rules

- Never add real credentials, customer data, or confidential URLs to prompts.
- Use dummy values such as `https://app.example.com` and `user@example.com`.
- Always review and run AI-generated code before merging it into the framework.
- Do not accept generated code without validating that it works for the project.

---

# 2. Input Parameter Sheet

Fill in the values below before using the Master Prompt.

| # | What to Provide | Placeholder | Example |
|---|---|---|---|
| 1 | Application type | `{{APP_TYPE}}` | Web, Responsive Web, Mobile Web |
| 2 | Application name | `{{APP_NAME}}` | Banking Portal, E-commerce Site |
| 3 | Framework design | `{{FRAMEWORK_TYPE}}` | POM, Page Factory, Screenplay, BDD, Hybrid |
| 4 | Automation tool | `{{TOOL}}` | Selenium, Playwright, Cypress |
| 5 | Programming language | `{{LANGUAGE}}` | Java, Python, TypeScript |
| 6 | Test runner | `{{TEST_RUNNER}}` | TestNG, JUnit, pytest, Playwright Test, Cucumber |
| 7 | Build/package tool | `{{BUILD_TOOL}}` | Maven, Gradle, npm, pip |
| 8 | Data-driven approach | `{{DATA_DRIVEN}}` | None, Excel, CSV, JSON, YAML, DataProvider |
| 9 | Test data approach | `{{TEST_DATA_STRATEGY}}` | Static files, Faker, API-seeded, DB-seeded |
| 10 | Reporting tool | `{{REPORTING}}` | Allure, Extent Reports, HTML Report |
| 11 | Logging tool | `{{LOGGING}}` | Log4j2, SLF4J, Python logging |
| 12 | Browsers | `{{BROWSERS}}` | Chrome, Firefox, Edge, Safari/WebKit |
| 13 | Execution mode | `{{EXECUTION_MODE}}` | Local, Headless, Grid, Docker, Cloud |
| 14 | Parallel execution | `{{PARALLEL}}` | Yes - 4 threads / No |
| 15 | Environments | `{{ENVIRONMENTS}}` | dev, qa, staging, prod-smoke |
| 16 | CI/CD tool | `{{CICD}}` | Jenkins, GitHub Actions, GitLab CI, Azure DevOps |
| 17 | Additional features | `{{FEATURES}}` | Screenshot on failure, retry, video, API login |
| 18 | Configuration approach | `{{CONFIG_APPROACH}}` | `.properties`, `.env`, YAML, JSON |
| 19 | Coding standards | `{{CODING_STANDARDS}}` | Google Java Style, PEP8, ESLint + Prettier |
| 20 | Sample scenarios | `{{SAMPLE_SCENARIOS}}` | Login, search, checkout |
| 21 | Constraints | `{{CONSTRAINTS}}` | No paid libraries, Java 17, corporate proxy |

---

# 3. Master Prompt: Generate a Complete UI Automation Framework

Copy the prompt below and replace the `{{PLACEHOLDERS}}` with your project details.

```text
ROLE

Act as a Senior QA Automation Engineer / Architect experienced in building
scalable, maintainable UI automation frameworks.

GOAL

Design and generate a complete UI automation framework based on the
project details provided below.

PROJECT DETAILS

- Application type: {{APP_TYPE}}
- Application name: {{APP_NAME}}
- Framework design: {{FRAMEWORK_TYPE}}
- Automation tool: {{TOOL}}
- Programming language: {{LANGUAGE}}
- Test runner: {{TEST_RUNNER}}
- Build tool: {{BUILD_TOOL}}
- Data-driven approach: {{DATA_DRIVEN}}
- Test data approach: {{TEST_DATA_STRATEGY}}
- Reporting: {{REPORTING}}
- Logging: {{LOGGING}}
- Browsers: {{BROWSERS}}
- Execution mode: {{EXECUTION_MODE}}
- Parallel execution: {{PARALLEL}}
- Environments: {{ENVIRONMENTS}}
- CI/CD: {{CICD}}
- Additional features: {{FEATURES}}
- Configuration approach: {{CONFIG_APPROACH}}
- Coding standards: {{CODING_STANDARDS}}
- Sample scenarios: {{SAMPLE_SCENARIOS}}
- Constraints: {{CONSTRAINTS}}

WHAT TO GENERATE

Generate the framework in this order.

1. ARCHITECTURE

- Explain the overall framework design in simple terms.
- Explain the main layers and what each layer does.
- Provide a simple text-based architecture diagram.

2. PROJECT STRUCTURE

- Show the complete folder/package structure.
- Give a short explanation for each important folder.

3. DEPENDENCIES

- Generate the required dependency file such as pom.xml,
  package.json, requirements.txt, etc.
- Use stable versions.
- Avoid unnecessary dependencies.

4. CORE FRAMEWORK CODE

Generate complete code for:

a. Configuration management
   - Read configuration for different environments.
   - Support overrides through CLI/system properties/environment variables.
   - Do not log secrets.

b. Browser/driver setup
   - Support the requested browsers and execution modes.
   - Support parallel execution where requested.
   - Handle setup and teardown safely.

c. Base page
   - Provide reusable UI actions.

d. Base test
   - Provide common test setup and cleanup.

e. Common utilities
   - Waits
   - Click/type/select actions
   - Screenshot capture
   - Test data reading
   - Random test data where required

f. Logging

g. Reporting

5. PAGE OBJECTS AND TESTS

- Create sample page objects.
- Create sample automated tests for:
  {{SAMPLE_SCENARIOS}}

Rules:
- Use stable locators.
- Do not use hard waits such as Thread.sleep.
- Keep assertions in the test layer.
- Keep page objects focused on page actions.
- Keep tests independent.

6. DATA-DRIVEN TESTING

Implement:
{{DATA_DRIVEN}}

Also provide:
- Data reader
- Sample data file
- Sample test using the data
- Positive, negative, and boundary data where applicable
- Handling for empty or invalid data

7. FAILURE HANDLING

Add, where applicable:
- Screenshot on failure
- Video/trace on failure if supported
- Retry mechanism if requested
- Clear error messages
- Proper test cleanup

Important:
Retries must not hide real application defects.

8. CI/CD

Generate a CI/CD pipeline for:
{{CICD}}

The pipeline should include:
- Checkout
- Dependency installation
- Build/lint if applicable
- Smoke tests
- Regression tests
- Environment/browser/tag parameters
- Report generation
- Screenshot/artifact storage
- Build failure rules

9. README

Create a beginner-friendly README covering:
- Framework overview
- Prerequisites
- Setup
- Folder structure
- How to run all tests
- How to run a specific browser
- How to run a specific environment
- How to run a tag/suite
- How to add a new page
- How to add a new test
- Reporting
- CI/CD
- Troubleshooting

FRAMEWORK RULES

- Follow SOLID and DRY principles.
- Keep tests independent.
- Separate test logic, page logic, test data, and configuration.
- Do not hardcode URLs, credentials, or secrets.
- Read secrets from environment variables or a secure vault.
- Avoid fixed waits.
- Prefer explicit waits or the automation tool's built-in auto-waiting.
- Keep locators inside page objects.
- Keep assertions inside tests.
- Make driver/browser handling thread-safe for parallel execution.
- Use clear naming conventions.
- Add short comments/docstrings for public methods.
- Do not create unnecessary framework complexity.
- Do not invent application-specific information that was not provided.

LOCATOR PRIORITY

Prefer locators in this order:

1. data-testid / other dedicated test attributes
2. id
3. Accessible role/name
4. CSS
5. XPath as a last resort

OUTPUT RULES

- Use clear headings.
- Show the file path before each code file.
- Provide complete code, not partial snippets.
- Explain important design decisions briefly.
- If information is missing, list assumptions first and then continue.
- Clearly identify anything that requires project-specific changes.
- End with:

  Next Steps / Known Limitations
```

---

# 4. Micro Prompts for Daily QE Activities

Use these prompts when you need to perform a specific automation task instead of generating the complete framework.

---

## 4.1 Project Setup and Configuration

### P-UI-01: Create Project Structure

```text
Act as a Senior QA Automation Engineer.

Create the folder/package structure for a
{{FRAMEWORK_TYPE}} UI automation framework using
{{TOOL}}, {{LANGUAGE}}, and {{TEST_RUNNER}}.

Provide:
1. Folder structure
2. One-line purpose of each important folder
3. Dependency file using {{BUILD_TOOL}}
4. .gitignore entries

Keep the structure simple and maintainable.
```

### P-UI-02: Environment Configuration

```text
Create a configuration manager in {{LANGUAGE}} using
{{CONFIG_APPROACH}}.

Requirements:
- Support these environments: {{ENVIRONMENTS}}
- Allow environment/configuration overrides through
  system properties, CLI arguments, or environment variables.
- Fail clearly when a required value is missing.
- Keep configuration thread-safe.
- Never log passwords, tokens, or other secrets.

Also provide sample configuration files.
```

### P-UI-03: Browser / Driver Factory

```text
Create a thread-safe browser/driver factory for
{{TOOL}} using {{LANGUAGE}}.

Support:
- Browsers: {{BROWSERS}}
- Execution mode: {{EXECUTION_MODE}}
- Headless mode
- Window size
- Download directory
- Browser capabilities/options
- Configuration-driven settings
- Setup and teardown for {{TEST_RUNNER}}

Ensure the driver is safely closed after the test.
```

---

# 4.2 Page Objects and Tests

### P-UI-04: Base Page

```text
Create a BasePage class in {{LANGUAGE}} for {{TOOL}}.

Include reusable methods for:
- Click
- Type
- Select
- Hover
- Scroll to element
- Get text
- Check if element is displayed
- Upload file
- Switch frame
- Switch window
- JavaScript click fallback

Requirements:
- Use configurable explicit waits or the tool's auto-waiting.
- Do not use fixed sleeps.
- Log important actions.
- Capture a screenshot when an action fails.
```

### P-UI-05: Create Page Object

```text
Create a page object for the "{{PAGE_NAME}}" page using
{{FRAMEWORK_TYPE}}, {{LANGUAGE}}, and {{TOOL}}.

Elements:
{{LIST_OF_ELEMENTS_WITH_HINTS}}

Example:
username input [id=user]
login button [text=Sign in]

Rules:
- Keep locators inside the page object.
- Prefer stable locators.
- Public methods should represent user actions.
- Do not expose unnecessary element getters.
- Do not put assertions inside the page object.
- Return the next page object when navigation occurs.
```

### P-UI-06: Convert Manual Test to Automation

```text
Convert the following manual test into an automated test using:

Tool: {{TOOL}}
Language: {{LANGUAGE}}
Test runner: {{TEST_RUNNER}}
Existing page objects: {{PAGE_OBJECT_NAMES}}

Manual test:
{{PASTE_STEPS_AND_EXPECTED_RESULTS}}

Rules:
- One clear objective per test.
- Assertions only in the test layer.
- Use a clear test name.
- Handle setup/cleanup through hooks.
- Do not depend on another test.
- Do not use fixed sleeps.
- Use the existing page objects instead of duplicating page logic.
```

### P-UI-07: BDD Feature and Step Definitions

```text
For this scenario:

{{SCENARIO_DESCRIPTION}}

Create:
1. Gherkin feature file
2. Background where useful
3. Scenario / Scenario Outline
4. Examples where useful
5. Tags
6. Matching step definitions in {{LANGUAGE}}
7. Hooks for setup, teardown, and screenshot on failure

Use Cucumber with {{TOOL}}.

Rules:
- Steps should use business-friendly language.
- Keep step definitions reusable.
- Step definitions should call page objects.
- Do not put detailed UI logic inside feature files.
```

---

# 4.3 Data-Driven Testing

### P-UI-08: Data-Driven Testing

```text
Implement data-driven testing in {{LANGUAGE}} using
{{TEST_RUNNER}} and {{DATA_DRIVEN}}.

Create:
1. Data reader utility
2. Sample data file
3. Automated test using the data
4. Positive, negative, and boundary examples
5. Test/report names that identify the data row
6. Handling for empty or malformed data
7. Environment-specific data support where required

Keep test data separate from test logic.
```

### P-UI-09: Test Data Generator

```text
Create a test data factory in {{LANGUAGE}} for:

{{ENTITY}}

Example:
User, Address, Order

Use a builder pattern and Faker or an equivalent library.

Support:
- Valid data
- Invalid data
- Boundary data
- Unique values where required
- Fixed seed for repeatable test data
```

---

# 4.4 Stability and Synchronization

### P-UI-10: Fix a Flaky Test

```text
Act as a Senior SDET.

This UI test is flaky and fails approximately
{{FAIL_RATE}}% of the time.

Test code:
{{PASTE_CODE}}

Error/log:
{{PASTE_ERROR}}

Analyze possible causes such as:
- Timing
- Locator instability
- Incorrect application state
- Test data
- Environment issues
- Animation
- Stale elements
- Parallel execution conflicts

Rank the likely causes from highest to lowest.

Then provide:
1. Root cause explanation
2. Corrected code
3. Explanation of the changes

Do not use fixed sleeps as the solution.
```

### P-UI-11: Improve Locators

```text
Review these UI locators and suggest more stable alternatives.

Preferred order:
data-testid > id > accessible role/name > CSS > XPath

Locators:
{{PASTE_LOCATORS}}

DOM/HTML:
{{PASTE_DOM}}

For each locator:
1. Explain why the current locator may be unstable.
2. Suggest a better locator.
3. Explain why the new locator is better.
4. If no stable locator exists, suggest which test-friendly
   attribute should be requested from developers.
```

### P-UI-12: Retry Mechanism

```text
Implement a retry-on-failure mechanism for
{{TEST_RUNNER}} using {{LANGUAGE}}.

Requirements:
- Retry count: {{RETRY_COUNT}}
- Retry only tests marked as retryable.
- Log every retry attempt.
- Show retried tests clearly in {{REPORTING}}.
- Do not retry every failure automatically.

Add a warning that retries must not be used to hide real defects.
```

---

# 4.5 Reporting, Logging, and Evidence

### P-UI-13: Reporting Integration

```text
Integrate {{REPORTING}} into my
{{TOOL}} + {{LANGUAGE}} + {{TEST_RUNNER}} framework.

Include:
- Required dependencies
- Listener/hook setup
- Step/action logging
- Screenshot attachment on failure
- Browser/environment information
- Report generation command
- Report opening command

Show a simple example of the final report structure.
```

### P-UI-14: Screenshot, Video, and Trace on Failure

```text
Add automatic evidence capture for test failures.

Framework:
{{TOOL}} + {{LANGUAGE}}

Capture:
- Screenshot
- Video if supported
- Trace if supported

Attach evidence to:
{{REPORTING}}

File names should contain:
- Test name
- Timestamp
- Browser

Also provide a way to clean up artifacts older than
{{DAYS}} days.
```

---

# 4.6 Execution and CI/CD

### P-UI-15: Parallel and Cross-Browser Execution

```text
Configure parallel execution for:

Tool: {{TOOL}}
Language: {{LANGUAGE}}
Test runner: {{TEST_RUNNER}}
Browsers: {{BROWSERS}}
Threads: {{THREAD_COUNT}}

Requirements:
- Thread-safe driver handling
- No shared mutable state
- Independent test data
- No test order dependency

Provide commands for:
1. Running all tests
2. Running one browser
3. Running one tag/suite
```

### P-UI-16: Grid / Docker / Cloud Execution

```text
Provide a Docker or equivalent setup for running
{{TOOL}} tests using:

Execution mode: {{EXECUTION_MODE}}
Browsers: {{BROWSERS}}

Include:
- Docker/remote configuration
- Remote URL
- Browser capabilities
- Credentials through environment variables
- Required framework changes
- Scaling approach
- Common troubleshooting steps
```

### P-UI-17: CI/CD Pipeline

```text
Create a {{CICD}} pipeline for my
{{TOOL}} / {{LANGUAGE}} UI automation framework.

Pipeline stages:
1. Checkout
2. Dependency installation/cache
3. Lint/build where applicable
4. Smoke tests
5. Regression tests
6. Environment/browser/tag parameters
7. Report generation
8. Screenshot/artifact storage
9. Notifications through {{NOTIFICATION_CHANNEL}}

Also include:
- Scheduled nightly execution
- Rules for when the pipeline should fail
```

---

# 4.7 Advanced Quality Checks

### P-UI-18: Accessibility Checks

```text
Add automated accessibility testing using axe-core
or an equivalent tool.

Framework:
{{TOOL}} + {{LANGUAGE}}

Requirements:
- Reusable accessibility helper
- WCAG level: {{WCAG_LEVEL}}
- Violation reporting in {{REPORTING}}
- Ability to exclude known issues
- Required justification for every exclusion
```

### P-UI-19: Visual Regression

```text
Implement visual regression testing for my
{{TOOL}} framework.

Include:
- Baseline screenshot creation
- Comparison
- Tolerance: {{TOLERANCE}}%
- Masking of dynamic areas
- Diff image on failure
- Process for reviewing and approving new baselines

Explain how the team should maintain visual baselines.
```

### P-UI-20: Reuse Login Session

```text
Implement a way to avoid repeating UI login for every test
using {{TOOL}} and {{LANGUAGE}}.

Preferred approach:
- Authenticate through API or stored session/cookies.
- Reuse the authenticated state.
- Refresh the state when it expires.
- Keep one dedicated test that verifies the real UI login.

Explain where the authentication state should be stored
and how it should be protected.
```

---

# 4.8 Review, Refactor, Migrate, and Document

### P-UI-21: Automation Code Review

```text
Act as a strict Senior QA Automation code reviewer.

Review this {{LANGUAGE}} / {{TOOL}} automation code for:

- Readability
- Locator quality
- Wait strategy
- Duplicate code
- SOLID violations
- Assertion quality
- Hardcoded data
- Thread safety
- Error handling
- Naming
- Maintainability

Return:

| Issue | Severity | Location | Recommended Fix |

Severity:
High / Medium / Low

Then provide the refactored code.

Code:
{{PASTE_CODE}}
```

### P-UI-22: Framework Migration

```text
Create a migration plan from:

Current tool: {{OLD_TOOL}}
Current language: {{OLD_LANGUAGE}}

To:

New tool: {{NEW_TOOL}}
New language: {{NEW_LANGUAGE}}

Include:
1. Tool/concept mapping
2. Phased migration approach
3. Coexistence strategy
4. Risks
5. Estimated effort by phase
6. Sample converted code

Sample code:
{{PASTE_SAMPLE}}
```

### P-UI-23: README and Onboarding Guide

```text
Create a beginner-friendly README for this UI automation framework.

Framework summary/structure:
{{PASTE_STRUCTURE_OR_SUMMARY}}

Include:
- Overview
- Prerequisites
- Setup
- Folder structure
- How to run all tests
- How to run specific tests
- How to select browser/environment
- How to add a new page
- How to add a new test
- How to add test data
- Reporting
- CI/CD
- Coding conventions
- FAQs
- Troubleshooting

Keep the explanation easy for a new QE/SDET team member to follow.
```

---

# 5. Filled Example

The following example shows how the Master Prompt can be filled for a typical Selenium + Java framework.

```text
ROLE

Act as a Senior QA Automation Engineer / Architect experienced in building
scalable, maintainable UI automation frameworks.

GOAL

Design and generate a complete UI automation framework.

PROJECT DETAILS

- Application type: Web
- Application name: Banking Portal
- Framework design: Page Object Model with BDD
- Automation tool: Selenium WebDriver
- Programming language: Java 17
- Test runner: TestNG + Cucumber
- Build tool: Maven
- Data-driven approach: Excel + Cucumber Examples
- Test data approach: Static Excel + Faker
- Reporting: Allure
- Logging: Log4j2
- Browsers: Chrome, Firefox, Edge
- Execution mode: Local + Selenium Grid
- Parallel execution: Yes - 4 threads
- Environments: QA, Staging
- CI/CD: Jenkins
- Additional features:
  Screenshot on failure, retry once, API login shortcut
- Configuration approach: .properties
- Coding standards: Google Java Style
- Sample scenarios:
  Login, fund transfer, statement download
- Constraints: Open-source libraries only

Generate the framework using the instructions from the Master Prompt.
```

---

# 6. Review Checklist for AI-Generated UI Framework Code

Before committing AI-generated automation code, verify the following:

### Framework

- [ ] Project builds successfully.
- [ ] Tests run using the documented commands.
- [ ] Folder structure is clear and maintainable.
- [ ] Configuration is separated from test code.
- [ ] No unnecessary dependencies are included.

### Locators and Waits

- [ ] Locators are stable.
- [ ] Locators are centralized in page objects.
- [ ] No hard sleeps such as `Thread.sleep`.
- [ ] Explicit waits or tool-supported auto-waiting are used.
- [ ] XPath is not used when a more stable locator is available.

### Tests

- [ ] Assertions are in the test layer.
- [ ] Tests are independent.
- [ ] Tests do not depend on execution order.
- [ ] Test data is separated from test logic.
- [ ] Test names clearly explain the behavior being tested.

### Parallel Execution

- [ ] Driver handling is thread-safe.
- [ ] Tests do not share mutable state.
- [ ] Test data does not cause parallel conflicts.
- [ ] Parallel execution has been tested.

### Failure Evidence

- [ ] Screenshots are captured on failure.
- [ ] Logs are available.
- [ ] Video/trace is captured if required.
- [ ] Evidence is attached to the test report.

### Security

- [ ] No credentials are hardcoded.
- [ ] No real customer data is committed.
- [ ] Secrets are stored securely.
- [ ] Secrets are not printed in logs.

### CI/CD

- [ ] CI pipeline runs successfully.
- [ ] Smoke and regression execution are supported.
- [ ] Reports are published.
- [ ] Test artifacts are archived.
- [ ] Build failure rules are defined.

### Documentation

- [ ] README is available.
- [ ] Setup instructions work on a clean machine.
- [ ] Run commands are documented.
- [ ] New team members can understand how to add a page/test.
- [ ] Troubleshooting information is included.

---

# 7. Prompting Tips

| Do | Don't |
|---|---|
| Give the AI the role, task, inputs, and expected output | Give a vague request such as "create automation framework" |
| Provide DOM/HTML when asking about locators | Ask the AI to fix a locator without giving the DOM |
| Provide the error/log when fixing a flaky test | Ask "why is this test failing?" without evidence |
| Ask the AI to list assumptions | Expect the AI to know project-specific standards |
| Build the framework step by step when the project is complex | Generate a huge framework and merge it without review |
| Specify the tool and language versions | Allow outdated APIs or dependencies without checking |
| Review and run generated code | Accept generated code without validation |

---

# 8. Recommended Usage Flow

For a new UI automation framework, use the prompts in roughly this order:

```text
1. P-UI-01
   Project Structure
        ↓
2. P-UI-02
   Configuration
        ↓
3. P-UI-03
   Browser / Driver Setup
        ↓
4. P-UI-04
   Base Page
        ↓
5. P-UI-05
   Page Objects
        ↓
6. P-UI-08
   Data-Driven Testing
        ↓
7. P-UI-13
   Reporting
        ↓
8. P-UI-14
   Failure Evidence
        ↓
9. P-UI-15
   Parallel / Cross-Browser
        ↓
10. P-UI-17
    CI/CD
        ↓
11. P-UI-21
    Code Review
        ↓
12. P-UI-23
    README / Onboarding
```

For a completely new framework, the **Master Prompt** can be used first and the Micro Prompts can then be used for individual enhancements or maintenance tasks.

---

# 9. Change Log

| Version | Date | Author | Change |
|---|---|---|---|
| 1.0 | 2026-10-08 | QE Automation | Initial release |
