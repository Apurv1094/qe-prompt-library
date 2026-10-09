# API Automation Script Development

## Objective

Generate maintainable API automation scripts from an **API contract** and **approved API test cases**, using the specified automation framework, language, and existing framework structure.

Focus only on **test script development**. Do not redesign requirements or create/modify test cases unless explicitly requested.

---

## Inputs

### Required

**API_CONTRACT**

* Preferred: OpenAPI/Swagger JSON or YAML.
* Source of truth for endpoint, method, parameters, headers, authentication, request/response schemas, status codes, constraints, and error responses.

**TEST_CASES**

* Approved API test cases containing, where applicable:

    * ID/scenario
    * Preconditions
    * Test data
    * Request/steps
    * Expected result/status

**AUTOMATION_FRAMEWORK**

* e.g. Rest Assured, Playwright API, Karate, Postman/Newman.

**LANGUAGE**

* e.g. Java, JavaScript, TypeScript, Python.

### Optional

**EXISTING_FRAMEWORK_STRUCTURE**

* Base classes, API clients, utilities, configuration, reporting, assertions, test runner, package/folder structure, coding standards.

**TEST_DATA**

* Request data, parameters, expected values, positive/negative/boundary data.

**ENVIRONMENT_DETAILS**

* Base URL, environment/configuration structure, API version, environment variables.

Never provide or generate real secrets.

---

## Processing

1. Parse the API contract and identify the APIs relevant to the supplied test cases.
2. Map each test case to its API endpoint and contract definition.
3. Identify request, authentication, test-data and response requirements.
4. Follow the specified framework, language and existing framework architecture.
5. Reuse existing framework components instead of duplicating them.
6. Generate the required API automation code.
7. Implement, where applicable:

    * Request construction
    * Path/query parameters
    * Headers/authentication
    * Request body
    * API execution
    * Status-code validation
    * Response/header/body assertions
    * Schema validation
    * Error validation
    * Data extraction/dependency handling
8. Externalize test data and environment configuration where appropriate.
9. Validate generated implementation against the API contract.
10. Report missing information or contract/test-case conflicts instead of inventing values.

---

## Locator/Automation Design Rules

For API automation:

* Use reusable API clients/builders/utilities where appropriate.
* Keep assertions explicit.
* Avoid duplicate request/response handling.
* Follow existing project conventions when supplied.
* Do not hardcode credentials, tokens, API keys or secrets.
* Do not fabricate endpoints, payloads, response fields, status codes or expected results.
* Do not silently change a test case or API contract when they conflict.

---

## Output

### 1. Automation Coverage

| Test Case | Status    | Class/Component | Method         |
| --------- | --------- | --------------- | -------------- |
| TC-001    | Automated | CourseApiTest   | createCourse() |

Status: `Automated`, `Partially Automated`, or `Not Automated`.

Explain why a test cannot be automated.

### 2. Automation Code

Provide the required framework-ready code, including applicable:

* Test classes
* API clients
* Request builders
* Authentication utilities
* Response/assertion utilities
* Test-data components
* Supporting configuration

### 3. Traceability

Map:

`Test Case → HTTP Method → Endpoint → Automation Class → Method`

### 4. Validations

Identify important assertions implemented for each test case:

* Status code
* Response headers
* Response fields/values
* Schema
* Error response
* Other test-case-defined validations

### 5. Framework Integration

Identify:

* Files/classes created or modified
* Package/folder location
* Dependencies
* Configuration changes
* Reused framework components

### 6. Missing Information / Conflicts

Clearly report:

* Missing contract information
* Missing test data
* Missing authentication details
* Missing expected results
* Contract/test-case conflicts
* Other blockers

Do not fabricate missing information.

---

## Input Template

```text
API_CONTRACT:

TEST_CASES:

AUTOMATION_FRAMEWORK:

LANGUAGE:

EXISTING_FRAMEWORK_STRUCTURE:

TEST_DATA:

ENVIRONMENT_DETAILS:
```

---

## Execution Flow

```text
API CONTRACT
     +
APPROVED TEST CASES
     +
FRAMEWORK + LANGUAGE
     +
EXISTING FRAMEWORK
          ↓
    MAP TEST CASES
          ↓
    DESIGN SCRIPT
          ↓
   GENERATE AUTOMATION
          ↓
 VALIDATE AGAINST CONTRACT
          ↓
 CODE + TRACEABILITY
 + COVERAGE + GAPS/CONFLICTS
```
