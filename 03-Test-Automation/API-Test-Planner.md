# API Test Planner

## Purpose
Discover API operations and plan test coverage without coding.

## When to use
Use this prompt when inventory documented API operations and prioritize coverage without generating test code. Ensure the required inputs are available.

## Inputs required
- `{{API_CONTRACT}}` — **Required:** OpenAPI/Swagger specification or equivalent documented endpoints, schemas and authentication.
- `{{TEST_SCOPE}}` — **Required:** In-scope operations, test categories, environments and exclusions.

## Prompt
```text
Role: Act as a Senior API Test Architect.

Task: Inventory documented API operations and prioritize coverage without generating test code.

Inputs:
API_CONTRACT:
{{API_CONTRACT}}
TEST_SCOPE:
{{TEST_SCOPE}}

Rules:
- Inventory documented methods, paths, parameters, responses, schemas and auth.
- Label each observation Documentation only or Runtime verified; never imply runtime verification from a contract.
- Map functional, negative, boundary, auth and schema cases to documented behavior.
- Prioritize by business impact, change risk and dependencies; flag missing contract details.
- Do not generate scripts or call APIs unless separately authorized.

Deliverables:
- Endpoint inventory with method, path, auth and verification status
- Prioritized scenario matrix: ID, endpoint, category, expected result, priority and evidence
- Test-data dependencies, contract gaps and execution prerequisites
```

## Expected output
- Endpoint inventory with method, path, auth and verification status
- Prioritized scenario matrix: ID, endpoint, category, expected result, priority and evidence
- Test-data dependencies, contract gaps and execution prerequisites
- Clearly label assumptions, missing evidence, and whether files were created or tests executed.

## Example
**Synthetic input:**
```text
API_CONTRACT: GET /courses returns 200 array; POST /courses requires bearer auth and returns 201 (synthetic). TEST_SCOPE: Functional, authentication and schema; no runtime access.
```

**Illustrative output (not executed):**
> API-01 | GET /courses | Functional | 200 and array | P1 | Documentation only; API-02 | POST /courses without token | Auth | expected status Not specified | P1 | Contract gap; no runtime claims.

The example is illustrative only; use actual input evidence for real deliverables.

## Limitations
- Results depend on supplied requirements, repository access, tool availability and authorization.
- Generated code or recommendations are not verified until explicitly checked or executed.
- Shared privacy, evidence, authorization and human-review requirements: `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
