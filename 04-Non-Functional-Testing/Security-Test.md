# Security Test

## Purpose
Plan authorized defensive security validation.

## When to use
Use this prompt when assessing application security to identify potential vulnerabilities related to authentication, authorization, input validation, data protection, and other security risks within the authorized testing scope.

## Inputs required
- `{{SYSTEM_SCOPE}}` — **Required:** Provide the relevant system scope details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{AUTHORIZED_TEST_SCOPE}}` — **Required:** Explicitly permitted targets, techniques, credentials handling, and exclusions.

## Prompt
```text
Act as a Senior Application Security Test Engineer.
Task: Create safe checklist for auth, access control, input validation, secrets, logging and dependencies; prioritize findings; no unauthorized exploitation.

Inputs:
SYSTEM_SCOPE:
{{SYSTEM_SCOPE}}
AUTHORIZED_TEST_SCOPE:
{{AUTHORIZED_TEST_SCOPE}}

Rules:
- Restrict scope to authorized systems.
- prioritize secure configuration, auth, access control and input validation.
- favor safe, non-destructive checks.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected Output

Generate an **Authorized Security Test Plan** containing the following sections:

### 1. Security Testing Scope
- Application or API components included in the assessment.
- Security requirements and relevant risks.
- Approved test environment, identities, and authorization boundaries.
- Assumptions, exclusions, and missing information.

### 2. Security Test Matrix

Include the following columns:

- **Test ID:** Unique security test identifier.
- **Security Risk:** Potential security vulnerability or threat being evaluated.
- **Security Control:** Security mechanism or requirement being validated.
- **Test Scope:** Application component, endpoint, or functionality under test.
- **Safe Test Approach:** Authorized, non-destructive steps to validate the control.
- **Expected Secure Behavior:** Expected application behavior when the control is working correctly.
- **Evidence Required:** Logs, API responses, or other artifacts needed to verify the result.
- **Remediation Priority:** High, Medium, or Low, based on potential impact if the control fails.
- **Execution Status:** Not Executed, Passed, Failed, or Blocked.

### 3. Security Testing Prerequisites
- Written authorization and approved testing scope.
- Approved test accounts with different permission levels.
- Test environment and API access details.
- Test data and logging or monitoring requirements.

### 4. Findings and Recommendations
- Summarize verified security findings with supporting evidence.
- Distinguish actual vulnerabilities from potential risks.
- Recommend remediation actions and priorities.
- Mark missing evidence as `Not provided`.
- Do not report a vulnerability as confirmed without execution evidence.

## Example

**Synthetic input:**

```text
APPLICATION_SCOPE:
Staging account profile API.

SECURITY_REQUIREMENTS:
Users may access only their own profile.
```

**Illustrative output (not executed):**

### 1. Security Testing Scope

| Parameter | Details |
|---|---|
| Application | Account Profile API |
| Environment | Staging |
| Primary Security Requirement | Users can access only their own profiles |
| Testing Focus | Authentication and object-level authorization |
| Approved Test Accounts | Not provided |
| Written Testing Authorization | Not provided |
| API Endpoint Details | Not provided |
| Exclusions | Not provided |

### 2. Security Test Matrix

*The following scenarios are proposed tests. Execution requires approval and suitable test accounts.*

| Test ID | Security Risk | Security Control | Test Scope | Safe Test Approach | Expected Secure Behavior | Evidence Required | Remediation Priority | Execution Status |
|---|---|---|---|---|---|---|---|---|---|
| SEC-01 | Unauthorized profile access (BOLA/IDOR) | Object-level authorization | Profile retrieval API | Using two approved test accounts, attempt to retrieve Account B's profile with Account A's credentials | Access denied without exposing Account B's data | Sanitized API response, status code, authorization logs | High | Not Executed |
| SEC-02 | Unauthenticated profile access | Authentication enforcement | Profile retrieval API | Send a profile request without an authentication token using an approved test account ID | Request rejected without exposing profile information | HTTP response, status code, security logs | High | Not Executed |
| SEC-03 | Unauthorized profile modification | Object-level authorization | Profile update API, if supported | Attempt to update Account B's test profile using Account A's credentials | Modification denied and Account B's data remains unchanged | API response, before/after test data, audit logs | High | Not Executed |
| SEC-04 | Sensitive data exposure | Response data protection | Profile retrieval API | Inspect an authorized test account's profile response for unnecessary sensitive fields | Only permitted profile attributes are returned | Sanitized response payload, approved data contract | Medium | Not Executed |

*SEC-03 and SEC-04 are additional recommended coverage. Their applicability depends on the API contract and security requirements.*

### 3. Security Testing Prerequisites

| Prerequisite | Details / Status |
|---|---|
| Testing Authorization | Not provided |
| Approved Environment | Staging identified; approval not provided |
| Test Accounts | Two isolated test identities required |
| API Endpoint and Methods | Not provided |
| Authentication Mechanism | Not provided |
| Test Data | Synthetic profile records recommended |
| API Testing Tool | Postman or Rest Assured (suggested) |
| Logging and Monitoring | Access to relevant security logs recommended |

### 4. Findings and Recommendations

**Observed Findings:**
- No security tests have been executed.
- No vulnerabilities have been confirmed.
- Actual API responses and security logs are not provided.

**Recommendations:**
- Obtain explicit authorization before executing security tests.
- Prioritize object-level authorization testing because it directly validates the supplied security requirement.
- Confirm that unauthorized requests cannot read or modify another user's profile.
- Validate that authentication is enforced on protected profile endpoints.
- Review API responses for unnecessary sensitive information.
- Record actual evidence and assign final remediation priorities based on confirmed impact.

*This example demonstrates security test planning only. No security tests were executed, and no vulnerabilities were verified.*

## Limitations
- A checklist is not a penetration test or compliance certification.
- never attempt exploitation outside authorized scope.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
