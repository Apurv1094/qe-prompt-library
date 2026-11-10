# API Automation Framework Generator

## Purpose
Generate a reusable, maintainable API test automation framework based on the QA engineer's selected language, API testing tool, test runner, and supporting tools. Include working example tests, shared utilities, configuration, reporting, and setup instructions.

## Required Inputs

```text
PROJECT_NAME: {{PROJECT_NAME}}
PROGRAMMING_LANGUAGE: {{PROGRAMMING_LANGUAGE}}
API_AUTOMATION_TOOL: {{API_AUTOMATION_TOOL}}
TEST_RUNNER: {{TEST_RUNNER}}
BUILD_OR_PACKAGE_MANAGER: {{BUILD_OR_PACKAGE_MANAGER}}
API_BASE_URL: {{API_BASE_URL}}
```

Examples: Java + Rest Assured + TestNG + Maven; TypeScript + Playwright API + Playwright Test + npm; Python + requests + pytest + pip.

## Optional Inputs

```text
API_DOCUMENTATION_OR_OPENAPI: {{API_DOCUMENTATION_OR_OPENAPI}}
AUTHENTICATION_TYPE: {{AUTHENTICATION_TYPE}}
FRAMEWORK_ARCHITECTURE: {{FRAMEWORK_ARCHITECTURE}}
ENVIRONMENTS: {{ENVIRONMENTS}}
REPORTING_TOOL: {{REPORTING_TOOL}}
CI_CD_TOOL: {{CI_CD_TOOL}}
SCHEMA_VALIDATION_LIBRARY: {{SCHEMA_VALIDATION_LIBRARY}}
TEST_DATA_SOURCE: {{TEST_DATA_SOURCE}}
LOGGING_TOOL: {{LOGGING_TOOL}}
ADDITIONAL_DEPENDENCIES: {{ADDITIONAL_DEPENDENCIES}}
EXISTING_REPOSITORY_PATH: {{EXISTING_REPOSITORY_PATH}}
```

If an optional field is empty, choose a conventional compatible default and document the choice. Never invent endpoints, credentials, or API contracts.

---

## Reusable Prompt

Act as a **Senior API Automation Architect and Framework Developer**.

Build an API automation framework using the inputs above. The framework must be **generic and reusable**, not hard-coded for a single API. Prioritize simple architecture, readable code, and practical utilities over unnecessary abstractions.

### Phase 1 — Validate the stack and plan

1. Check that the selected language, API tool, runner, build manager, and libraries are compatible.
2. If a choice is incompatible, explain the issue and propose the smallest change needed; ask only if the decision is blocking.
3. Identify the framework architecture and proposed directory structure.
4. Explain the responsibility of each core folder and reusable utility.
5. Use the provided API documentation to identify a safe example endpoint, if available. Otherwise create clearly labeled illustrative fixtures and examples that do not claim to work against the live API.
6. Do not overwrite an existing project without approval; inspect and preserve existing files when a repository is supplied.

### Phase 2 — Generate the framework

Create actual source files, not just a directory tree or pseudocode, when file-writing tools are available.

Include the following components where relevant to the selected stack:

| Component | Expected responsibility |
|---|---|
| Configuration manager | Read base URL, environment, timeouts, and non-secret settings |
| HTTP/API client | Centralize GET, POST, PUT, PATCH, DELETE, headers, and request options |
| Request builder/helper | Construct requests, query/path parameters, and payloads |
| Authentication helper | Support configured auth flows and token reuse/refresh where applicable |
| Response validation | Reusable status, header, body, and response-time assertions |
| Schema validation | Validate response structure against supplied schemas/contracts |
| Test data utility | Load JSON/CSV/fixtures and generate unique test data where needed |
| Serialization utility | Parse and serialize JSON safely |
| Logging utility | Log useful request/response diagnostics with sensitive values redacted |
| Environment manager | Select local, QA, staging, or other configured environments |
| Test setup/teardown | Shared fixtures, lifecycle hooks, and cleanup |
| Reporting | Produce human-readable test results and machine-readable CI output |
| Error handling | Clear exceptions and actionable failure messages |

Keep utilities focused: combine components when separate classes/modules would add complexity without benefit. Use the native capabilities of the selected tool rather than reimplementing them.

### Phase 3 — Create representative tests

Provide executable examples for these categories, where supported by the documented API:

1. Positive functional request
2. Negative request (for example, invalid input)
3. Boundary-value check
4. Authentication/authorization check
5. Response schema validation

Use real documented endpoints only. When the API contract is unavailable, use local mocks or explicitly illustrative tests and explain what needs replacing. Do not assume a particular API returns a specific status or error message without evidence.

Tests must call reusable utilities rather than duplicate HTTP setup, configuration, and assertions. Show a short execution-flow example: **test → client/helper → endpoint → validator → report**.

### Phase 4 — Configuration, security, and CI

1. Provide dependency configuration and reproducible install/build commands.
2. Separate environment-specific configuration from test logic.
3. Load credentials/tokens from environment variables or a secret manager; never commit secrets.
4. Provide `.gitignore` and a `.env.example` (or stack equivalent) with placeholder values only.
5. Configure sensible timeouts, failure diagnostics, and controlled retries only where justified. Never use retries to hide test failures.
6. Enable parallel execution only when test data and shared state are safe.
7. If a CI/CD tool is selected, create a minimal pipeline that installs dependencies, runs tests, publishes reports, and returns a failing exit status when tests fail.

### Phase 5 — Validate the framework

1. Install dependencies and compile/type-check if the runtime is available.
2. Execute the representative tests or local mock tests.
3. Report actual commands, passed/failed/skipped counts, and errors.
4. Fix issues within the generated framework and rerun checks when possible.
5. If execution is unavailable, explicitly state **Not executed** and give exact commands for the user to run. Never claim tests passed without execution evidence.

---

## Expected Output

Return results in this order:

1. **Selected Technology Stack** — choices and any defaults applied.
2. **Framework Architecture** — directory tree and brief explanation of key files.
3. **Generated Framework Files** — complete working code and configuration, saved in the project if tools permit.
4. **Reusable Utilities** — utility name, purpose, and an example of how a test uses it.
5. **Sample API Tests** — representative tests for the supported categories.
6. **Execution Instructions** — prerequisites, setup, environment variables, and run commands.
7. **CI/CD and Reporting** — configuration and output locations, if requested.
8. **Validation Results** — checks actually performed and their outcomes.
9. **Extension Guide** — steps for adding a new endpoint, test, environment, and reusable helper.
10. **Limitations / Next Steps** — missing API documentation, unverified behavior, or remaining work.

## Rules

- Respect the user's chosen technology stack. Do not silently substitute another language, tool, or runner.
- Build a reusable **framework**, not a single hard-coded test script.
- Prefer straightforward modules, consistent naming, and minimal dependencies.
- Do not generate dozens of placeholder files or unused abstraction layers.
- Keep test assertions in tests or validators; keep HTTP communication in the client layer.
- Use parameterization/data-driven tests where it adds value.
- Keep test cases independent and avoid order-dependent execution.
- Avoid destructive requests against real environments unless explicitly authorized.
- Do not fabricate API specifications, responses, execution results, or working integrations.
- Include a concise README explaining how another QA engineer can use the framework.

## Example Input

```text
PROJECT_NAME: Reusable API Automation Framework
PROGRAMMING_LANGUAGE: Java 17
API_AUTOMATION_TOOL: Rest Assured
TEST_RUNNER: TestNG
BUILD_OR_PACKAGE_MANAGER: Maven
API_BASE_URL: https://dummyjson.com

API_DOCUMENTATION_OR_OPENAPI: https://dummyjson.com/docs
AUTHENTICATION_TYPE: Bearer token where required
FRAMEWORK_ARCHITECTURE: Layered (tests, clients, utilities, config)
ENVIRONMENTS: local, qa, staging
REPORTING_TOOL: Surefire reports
CI_CD_TOOL: Jenkins
SCHEMA_VALIDATION_LIBRARY: Rest Assured JSON Schema Validator
TEST_DATA_SOURCE: JSON fixtures
LOGGING_TOOL: SLF4J
ADDITIONAL_DEPENDENCIES: None
EXISTING_REPOSITORY_PATH: New project
```

**Usage:** Fill the required inputs, optionally fill the remaining fields, then paste this Markdown file into your coding agent or AI-assisted development workflow. Ask it to execute Phases 1–5 and generate the files in your project workspace.
