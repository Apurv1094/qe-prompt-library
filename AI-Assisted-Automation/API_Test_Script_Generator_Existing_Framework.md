# API Test Script Generator — Existing Framework

## Purpose
Inspect an existing API automation framework and generate **new API automation test scripts** that follow its current architecture, conventions, and reusable utilities.

Generate tests from the supplied **user story, acceptance criteria, test cases, and endpoint API contract**. Do not create a new framework or replace existing utilities unless explicitly requested.

## Required Inputs

```text
FRAMEWORK_LOCATION: {{FRAMEWORK_LOCATION}}
STORY_DESCRIPTION: {{STORY_DESCRIPTION}}
ACCEPTANCE_CRITERIA: {{ACCEPTANCE_CRITERIA}}
TEST_CASES: {{TEST_CASES}}
API_CONTRACT: {{API_CONTRACT}}
```

`FRAMEWORK_LOCATION` can be the current workspace, a local project path, or an accessible repository. `API_CONTRACT` can be an OpenAPI/Swagger specification, endpoint documentation, or a pasted contract containing the method, path, authentication, parameters, request/response schemas, and status codes.

## Optional Inputs

```text
TARGET_MODULE: {{TARGET_MODULE}}
TARGET_ENVIRONMENT: {{TARGET_ENVIRONMENT}}
TEST_DATA: {{TEST_DATA}}
TARGET_TEST_FILE_OR_PACKAGE: {{TARGET_TEST_FILE_OR_PACKAGE}}
EXECUTION_SCOPE: {{EXECUTION_SCOPE}}  # Generate only | Generate and run
```

If optional inputs are absent, use established framework conventions. Never invent credentials, undocumented endpoint behavior, or business rules.

---

## Reusable Prompt

Act as a Senior API Automation Engineer working in an **existing** automation repository.

### Phase 1 — Inspect the Existing Framework

1. Inspect the project structure, dependency/build files, configuration, test runner, and existing API tests.
2. Identify the language, API testing tool, test runner, naming conventions, package/folder layout, and assertion style.
3. Locate reusable components such as:
   - API/HTTP client and request helpers
   - Environment/configuration manager
   - Authentication/token helpers
   - Test data builders, fixtures, and payload templates
   - Response and JSON schema validators
   - Logging, reporting, and retry mechanisms
   - Setup/teardown and CI execution configuration
4. Read at least one representative existing API test and trace how it calls those utilities.
5. Briefly summarize the conventions and reusable components that new tests must follow.

**Rule:** Reuse existing utilities and dependencies. Do not introduce a parallel API client, duplicate helpers, new test runner, or new framework structure without a clear, documented necessity.

### Phase 2 — Understand the Test Requirements

1. Read the story and acceptance criteria to understand expected business behavior.
2. Map each supplied test case to the applicable acceptance criterion and API operation.
3. Read the endpoint contract to identify:
   - HTTP method and path
   - Required authentication and headers
   - Path/query parameters and request body
   - Expected status codes, response fields, types, and schema
   - Documented validation and error behavior
4. Determine required setup, test data, cleanup, and dependencies between API calls.
5. Identify conflicts or gaps between test cases, acceptance criteria, and contract. **Do not silently resolve contradictions.**
6. Do not invent expected response codes or validations. Mark unsupported expectations as **Needs clarification**; proceed with independent, well-supported cases.

### Phase 3 — Plan the Test Scripts

Create a concise test mapping table:

| Test Case ID | AC Reference | Endpoint | Scenario | Expected Result | Planned Test File/Method | Status |
|---|---|---|---|---|---|---|

Status is **Ready**, **Needs clarification**, or **Blocked**. Cover supplied positive, negative, boundary, authentication, and schema scenarios where supported by the contract. Do not add unrelated tests.

Before writing code, confirm the planned files and which existing utilities will be reused. If a required utility is missing, prefer a minimal addition consistent with the repository; explain why it is necessary.

### Phase 4 — Generate Automation Scripts

1. Generate or update test files in the established project structure.
2. Follow the existing language, framework, test runner, naming, annotations, and coding style.
3. Use existing HTTP clients, configuration, auth helpers, fixtures, assertions, and schema validators.
4. Create independent, deterministic tests where practical. Avoid fixed sleeps and shared mutable test data.
5. Keep credentials and environment-specific values out of source code; use existing secure configuration mechanisms.
6. Use test data from supplied fixtures or contract-supported examples. Clearly label generated synthetic test data.
7. Assert meaningful contract and acceptance-criteria outcomes, not only HTTP status codes. Do not assert unspecified response details.
8. Include necessary setup/cleanup for created resources. Do not run destructive tests against an unapproved environment.
9. Add traceable test case IDs and AC references using the project's existing convention.
10. Do not modify unrelated tests, dependencies, framework utilities, or CI configuration without necessity and explanation.

### Phase 5 — Validate

1. Check imports, compilation/type checks, and framework conventions.
2. If `EXECUTION_SCOPE` is **Generate and run**, execute the relevant tests using the repository's standard command, provided the environment and access are available and execution is safe.
3. If execution is not requested or cannot be performed, do not claim tests passed. Report **Not executed** with the reason.
4. Report test failures separately from environment, authentication, missing-data, and contract issues.
5. Fix generator-introduced code errors when possible; never change expected assertions merely to make tests pass.

## Expected Output

### 1. Framework Inspection Summary
- Detected technology stack and test structure
- Existing reusable utilities selected
- Conventions to follow

### 2. Test Case Mapping
- Test case ID, AC reference, endpoint, test method/file, and coverage status
- Gaps or ambiguities requiring clarification

### 3. Generated/Updated Files
- File paths and purpose
- Summary of new test methods and utilities reused
- Any minimal framework changes and their justification

### 4. Validation Results
- Build/test command (if used)
- Passed, failed, skipped, blocked, or not executed
- Relevant errors and next actions

### 5. How to Run
- Exact commands using the existing framework
- Required environment variables, configuration, and test data (never print secrets)

---

## Example Input

```text
FRAMEWORK_LOCATION: Current VS Code workspace

STORY_DESCRIPTION:
As a customer, I want to retrieve my order details by order ID so that I can track my purchase.

ACCEPTANCE_CRITERIA:
AC1: An authenticated customer can retrieve their own order.
AC2: The response includes orderId, status, and totalAmount.
AC3: A customer cannot access another customer's order.
AC4: An unknown order ID returns the documented not-found error.

TEST_CASES:
TC-01: Retrieve an existing order with a valid customer token.
TC-02: Retrieve an order without an access token.
TC-03: Retrieve another customer's order.
TC-04: Retrieve a nonexistent order.
TC-05: Validate the successful response schema.

API_CONTRACT:
GET /api/orders/{orderId}
Authorization: Bearer <token>
200: {"orderId":"string","status":"string","totalAmount":0.0}
401: {"error":"Unauthorized"}
403: {"error":"Forbidden"}
404: {"error":"Order not found"}

EXECUTION_SCOPE: Generate only
```

**Expected behavior:** Inspect the actual repository first; generate test scripts using its existing language and utilities. Map TC-01 through TC-05 to the story, ACs, and contract. Flag any missing test data or assumptions, and report the scripts as **Not executed**.
