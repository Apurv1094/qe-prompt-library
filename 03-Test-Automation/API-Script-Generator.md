# API Script Generator

## Purpose
Generate or update API automation scripts from provided test cases, acceptance criteria and API contracts within an existing API automation framework.

The goal is to reuse the existing framework architecture, utilities and coding conventions rather than creating a new framework.

## When to use
Use this prompt when implement contract-backed API tests inside an existing framework. Ensure the required inputs are available.

## Inputs required
- `{{EXISTING_FRAMEWORK_PATH}}` — **Required:** Path to the existing API automation project whose conventions must be reused.
- `{{TEST_CASES}}` — **Required:** Test case IDs, requests, test data, steps and intended validations.
- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Approved business rules and expected API outcomes.
- `{{API_CONTRACT}}` — **Required:** OpenAPI/Swagger definition or verified endpoint, schema and status-code details.
- `{{OUTPUT_SCRIPT_PATH}}` — **Required:** Exact file or directory where generated API test scripts must be saved.
- `{{EXECUTION_REQUIRED}}` — **Optional:** Optional Yes/No flag authorizing execution; defaults to No.

## Prompt
```text
Role: Act as a Senior API Test Automation Engineer.

Task: Implement contract-backed API tests inside an existing framework.

Inputs:
EXISTING_FRAMEWORK_PATH:
{{EXISTING_FRAMEWORK_PATH}}
TEST_CASES:
{{TEST_CASES}}
ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}
API_CONTRACT:
{{API_CONTRACT}}
OUTPUT_SCRIPT_PATH:
{{OUTPUT_SCRIPT_PATH}}
EXECUTION_REQUIRED:
{{EXECUTION_REQUIRED}}

Rules:
- Inspect the existing project, test runner, helpers, authentication and test coverage before writing code.
- Map each requested case to an endpoint, acceptance criterion and assertions.
- Reuse existing request builders, configuration, schemas, fixtures and naming conventions; avoid duplicate utilities.
- Do not invent status codes, response fields, endpoints, credentials or undocumented behavior.
- Create files only at OUTPUT_SCRIPT_PATH; inspect before modifying and preserve unrelated tests.
- Never execute unless EXECUTION_REQUIRED=Yes, access is available and execution is safe and authorized.
- Do not weaken assertions to obtain passing tests; distinguish code, data, environment and product failures.
- Report exact paths, test mapping and actual validation evidence; never claim unrun tests passed.

Deliverables:
- Framework inspection and reuse summary
- Case-to-endpoint-to-script traceability matrix
- Exact created/updated files and assertions
- Execution command, observed result or Not executed, and blockers
```

## Expected output
- Framework inspection and reuse summary
- Case-to-endpoint-to-script traceability matrix
- Exact created/updated files and assertions
- Execution command, observed result or Not executed, and blockers
- Clearly label assumptions, missing evidence, and whether files were created or tests executed.

## Example
**Synthetic input:**
```text
EXISTING_FRAMEWORK_PATH: ./api-tests; TEST_CASES: API_TC_01 GET /products/1; ACCEPTANCE_CRITERIA: Existing product returns 200 with matching id; API_CONTRACT: GET /products/{id} 200 {id: integer}; OUTPUT_SCRIPT_PATH: src/test/java/tests/ProductTest.java; EXECUTION_REQUIRED: No.
```

**Illustrative output (not executed):**
> API_TC_01 → GET /products/{id} → ProductTest.java → assert HTTP 200 and response id=1; command: mvn -Dtest=ProductTest test; execution: Not executed.

The example is illustrative only; use actual input evidence for real deliverables.

## Limitations
- Results depend on supplied requirements, repository access, tool availability and authorization.
- Generated code or recommendations are not verified until explicitly checked or executed.
- Shared privacy, evidence, authorization and human-review requirements: `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
