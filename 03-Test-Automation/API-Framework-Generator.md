# API Framework Generator

## Purpose
Create a new reusable API automation framework.

## When to use
Use this prompt when design and, only when authorized, scaffold a reusable API test framework. Ensure the required inputs are available.

## Inputs required
- `{{TOOL}}` — **Required:** API testing library or tool, such as Rest Assured or Playwright APIRequest.
- `{{LANGUAGE}}` — **Required:** Implementation language and version, such as Java 17.
- `{{FRAMEWORK_PREFERENCES}}` — **Required:** Test runner, build tool, reporting, CI and architectural preferences.
- `{{API_CONTRACT}}` — **Required:** Sanitized OpenAPI specification or documented endpoints, schemas and authentication.

## Prompt
```text
Role: Act as a Senior API Automation Architect.

Task: Design and, only when authorized, scaffold a reusable API test framework.

Inputs:
TOOL:
{{TOOL}}
LANGUAGE:
{{LANGUAGE}}
FRAMEWORK_PREFERENCES:
{{FRAMEWORK_PREFERENCES}}
API_CONTRACT:
{{API_CONTRACT}}

Rules:
- Honor the chosen stack and contract; do not invent endpoints or status codes.
- Separate configuration, HTTP clients, authentication, fixtures, assertions and reporting.
- Keep secrets in environment variables or a secure secrets manager.
- Scaffold files only with workspace write authorization; never overwrite existing work without approval.
- Distinguish scaffolded from compiled and executed code.

Deliverables:
- Proposed project tree and responsibilities
- Build/dependency configuration and reusable HTTP components
- One contract-grounded sample test, configuration and CI commands
- File creation and verification status
```

## Expected output
- Proposed project tree and responsibilities
- Build/dependency configuration and reusable HTTP components
- One contract-grounded sample test, configuration and CI commands
- File creation and verification status
- Clearly label assumptions, missing evidence, and whether files were created or tests executed.

## Example
**Synthetic input:**
```text
TOOL: Rest Assured; LANGUAGE: Java 17; FRAMEWORK_PREFERENCES: TestNG + Maven, GitHub Actions; API_CONTRACT: GET /products/{id} returns 200 with integer id (synthetic).
```

**Illustrative output (not executed):**
> src/test/java/.../ProductApiTest.java → GET /products/1, assert 200 and id=1; pom.xml → Rest Assured/TestNG; .github/workflows/api-tests.yml → mvn test (not executed).

The example is illustrative only; use actual input evidence for real deliverables.

## Limitations
- Results depend on supplied requirements, repository access, tool availability and authorization.
- Generated code or recommendations are not verified until explicitly checked or executed.
- Shared privacy, evidence, authorization and human-review requirements: `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
