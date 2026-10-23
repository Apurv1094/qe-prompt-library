# CI/CD Pipeline Configuration Generator

## Purpose

Generate a CI/CD pipeline configuration that matches the user's existing or planned test automation framework. Select the correct pipeline syntax, runtime, dependency manager, test commands, browser setup, reporting, and artifact handling based on the chosen CI/CD tool, automation tool, programming language, and project configuration.

The output must be specific to the user's choices. Do not assume every automation framework uses Maven, npm, or the same test command.

## User Inputs

Collect the following inputs. If an essential input is missing, ask a concise follow-up question. Allow the user to leave optional inputs blank and make clearly stated, conservative assumptions where possible.

- **CI/CD Tool:** `{{CI_CD_TOOL}}`
  - Examples: Jenkins, GitHub Actions, GitLab CI, Azure DevOps, CircleCI, Bitbucket Pipelines
- **Automation Tool:** `{{AUTOMATION_TOOL}}`
  - Examples: Selenium, Playwright, Cypress, Appium, REST Assured
- **Programming Language:** `{{PROGRAMMING_LANGUAGE}}`
  - Examples: Java, TypeScript, JavaScript, Python, C#
- **Test Runner / Framework:** `{{TEST_RUNNER}}`
  - Examples: TestNG, JUnit, Cucumber, Playwright Test, pytest, NUnit
- **Dependency / Build Tool:** `{{BUILD_TOOL}}`
  - Examples: Maven, Gradle, npm, pnpm, yarn, pip, Poetry, NuGet; use `Auto-detect` if unsure
- **Repository and Branch:** `{{REPOSITORY_AND_BRANCH}}`
- **Execution Environment:** `{{EXECUTION_ENVIRONMENT}}`
  - Examples: Windows, Linux, macOS, Docker, hosted agent
- **Browser / Platform:** `{{BROWSER_OR_PLATFORM}}`
  - Examples: Chrome, Firefox, Edge, WebKit, Android emulator; include headless or headed preference if relevant
- **Configuration Source:** `{{CONFIGURATION_SOURCE}}`
  - Examples: properties file, JSON, environment variables, command-line parameters, CI/CD variables
- **Test Selection / Parameters:** `{{TEST_SELECTION_AND_PARAMETERS}}`
  - Examples: suite XML, tags, test folder, environment, browser, smoke/regression
- **Reports and Artifacts:** `{{REPORTS_AND_ARTIFACTS}}`
  - Examples: TestNG XML, JUnit XML, Playwright HTML report, Playwright Allure Report, screenshots, videos, logs
- **Secrets / Credentials:** `{{SECRETS_REQUIREMENTS}}`
  - Describe required secret names only. Never request or hard-code actual secret values.
- **Additional Requirements:** `{{ADDITIONAL_REQUIREMENTS}}`
  - Examples: parallel execution, scheduled runs, manual parameters, notifications, Docker, deployment gates

## Core Instructions

1. Confirm the requested CI/CD tool and generate its native pipeline format:
   - Jenkins → `Jenkinsfile` using Declarative Pipeline Groovy by default.
   - GitHub Actions → workflow YAML under `.github/workflows/`.
   - GitLab CI → `.gitlab-ci.yml`.
   - Azure DevOps → `azure-pipelines.yml`.
   - CircleCI → `.circleci/config.yml`.
   - Bitbucket Pipelines → `bitbucket-pipelines.yml`.
   - If a tool is not listed, use its supported native configuration format rather than forcing Groovy.
2. Determine the correct runtime, dependency manager, installation steps, and test command from the automation tool, language, test runner, and build configuration.
3. Prefer inspecting the existing repository files when available, including build files, package manifests, test-runner configuration, framework configuration, and existing pipeline files. Do not invent project-specific scripts, paths, report locations, or task names.
4. If repository inspection is not available, state assumptions and use conventional defaults only where appropriate. Clearly mark values the user must replace.
5. Separate CI/CD pipeline syntax from test framework logic. The pipeline should invoke the framework's existing configuration and driver/browser initialization; it should not assume the CI/CD system automatically discovers or implements browser selection.
6. Use secure secret handling. Reference the CI/CD tool's secret store or credential mechanism; never place passwords, tokens, or private keys directly in the generated file.
7. Make the pipeline practical and maintainable. Include checkout, environment/runtime setup, dependency installation, test execution, report publishing or artifact upload where supported, and a clear final status.
8. Use valid syntax for the chosen CI/CD platform and the selected shell/agent OS. For Jenkins, use `bat` for Windows command steps and `sh` for Linux/macOS steps as appropriate.
9. Do not include incompatible commands from multiple ecosystems in one pipeline. For example, do not run Maven commands for a typical Playwright TypeScript project unless the repository specifically requires Maven.
10. Do not claim the generated configuration has been executed or validated unless it actually has. Provide validation steps and identify anything that needs local or CI verification.

## Framework Selection Guidance

Use these as starting points, then verify the actual repository configuration.

| Automation tool and language | Common build/dependency tool | Common test command examples |
|---|---|---|
| Selenium + Java + TestNG | Maven or Gradle | `mvn test` or the configured Gradle test task |
| Selenium + Java + JUnit | Maven or Gradle | `mvn test` or the configured Gradle test task |
| Selenium + Python | pip / Poetry / other project-defined tool | `pytest` or the configured test command |
| Playwright + TypeScript | npm / pnpm / yarn | `npx playwright test` or the package script |
| Playwright + JavaScript | npm / pnpm / yarn | `npx playwright test` or the package script |
| Playwright + Java | Maven or Gradle, depending on project | Use the repository's configured test command |
| Cypress + JavaScript/TypeScript | npm / pnpm / yarn | `npx cypress run` or the package script |
| Appium + Java | Maven or Gradle | Use the configured TestNG/JUnit/Cucumber command |
| REST Assured + Java | Maven or Gradle | Use the configured test task |

Do not infer the test runner solely from the automation tool. For example, a Selenium project may use TestNG, JUnit, or Cucumber. Prefer the repository's `pom.xml`, `build.gradle`, `package.json`, lockfile, or equivalent source of truth.

## Pipeline Design Requirements

Build the pipeline using only stages and features relevant to the selected platform and project. Consider these stages as applicable:

1. **Checkout** — fetch the intended repository and branch using the platform's supported mechanism.
2. **Runtime Setup** — select/install the required JDK, Node.js, Python, .NET SDK, or other runtime.
3. **Dependency Installation** — use the project's actual dependency manager and lockfile where present.
4. **Browser / Driver Setup** — install or provision required browsers and drivers when the environment does not already provide them. Prefer supported automation-tool installation mechanisms.
5. **Test Execution** — run the project's actual test command, forwarding configured parameters safely.
6. **Report Publication** — publish supported test results, using the correct report paths and formats for the selected test runner and CI/CD tool.
7. **Artifact Collection** — retain useful reports, screenshots, videos, logs, and other debugging artifacts when configured and available.
8. **Notifications / Follow-up Actions** — add only if requested and if the platform and required integration are known.
9. **Post-run Handling** — ensure report/artifact collection runs when tests fail where supported, without incorrectly hiding the test failure.

Avoid adding unnecessary stages just to make the pipeline look comprehensive.

## Browser and Configuration Parameter Handling

If the user requests browser selection or other runtime parameters:

- Determine how the framework currently reads them: environment variable, command-line/system property, config file, test-runner parameter, or package script.
- Pass values using that established mechanism.
- If the framework does not support the requested parameter, explain the required framework-side change separately. Do not imply that adding a pipeline parameter alone changes the browser used by the tests.
- Validate parameter values where practical and avoid unsafe shell interpolation.
- Keep secrets separate from ordinary parameters.

Examples of common patterns (verify the project's implementation before using them):

- Java/Maven may read a system property such as `System.getProperty("Browser", "chrome")`, passed with a Maven option such as `-DBrowser=chrome`.
- Playwright Test may read an environment variable or use its `playwright.config.ts` projects and command-line options.
- A properties-file-driven framework may need the pipeline to update a property, supply a supported override, or select a config file. Do not assume system properties override custom config readers unless the code confirms it.

## Required Output

Return the following sections in order:

### 1. Detected Configuration
Summarize the user's choices and list any assumptions or unresolved details.

### 2. Generated Pipeline File
Provide the complete configuration in one code block using the correct file name and syntax for the selected CI/CD tool. Do not mix in explanatory prose inside the code block.

### 3. Project-specific Integration Notes
Explain which existing project files, scripts, configuration keys, test-runner settings, browser setup, and report paths the pipeline relies on. Mark all placeholders that must be replaced.

### 4. Setup Required in the CI/CD Tool
Explain any required agent/runner, runtime/tool installation, credentials, secret variables, permissions, browser dependencies, and report-publishing configuration.

### 5. How to Run It
Explain how to trigger the pipeline, set supported parameters, and inspect the test results.

### 6. Validation Checklist
Provide a concise checklist to verify syntax, dependency installation, test discovery, browser startup, parameter forwarding, report generation, artifact retention, and failure handling.

## Quality Gate

Before returning the generated file, verify against the available project details:

- The pipeline format matches the selected CI/CD tool.
- The runtime and dependency manager match the language and repository.
- The test command matches the actual test runner and project scripts.
- The shell commands match the selected agent operating system.
- Browser installation and browser selection are handled correctly for the environment.
- Report paths and formats match the actual test configuration.
- Secrets are referenced securely and no real secret values are included.
- Failure handling preserves a failed build when tests fail.
- Every assumption and replacement value is clearly identified.
- No execution or validation is claimed unless performed.

## Start Here

Use the inputs above to generate a complete, project-appropriate CI/CD pipeline configuration. If an essential detail is missing, ask only for the missing information needed to avoid producing an incorrect pipeline. Otherwise, proceed and clearly document assumptions.
