# Test Case Creation

**Module:** Manual QA

**Sub Module:** Test Design

**Purpose:** Convert approved test scenarios into detailed, executable test cases with clear preconditions, test data, steps, and expected results. The goal is to make each test case easy to execute, understand, and reuse during functional and regression testing.


## When to use this prompt

* After Test Scenario Creation is completed and the scenarios are reviewed.
* When a requirement or feature is ready for detailed functional testing.
* Before test execution, when the QA team needs clear and repeatable test steps.
* When existing test scenarios need to be converted into executable test coverage.


## What Test Case Creation is (and isn't)

This is a **detailed test design activity** — "how exactly will we verify this scenario?"

It is **not** about discovering new requirements or changing the expected business behavior. The test case should be based on the requirement, acceptance criteria, approved scenarios, and any clarified business rules.

A good test case should be:

* Clear enough for another QA engineer to execute without additional explanation.
* Focused on one testing objective.
* Independent where practical.
* Traceable back to a requirement or test scenario.
* Specific about the expected result.

For example:

* **Test Scenario:** Verify that a user can log in with valid credentials.
* **Test Case:** Enter a registered username, enter the correct password, click Login, and verify that the user is redirected to the dashboard.


## Prompt

```text
You are a senior QA engineer creating detailed test cases from
approved test scenarios and requirements.

Your job is to convert each scenario into clear, executable test
cases. Do not change the requirement or invent unsupported behavior.

Requirement:

"""
{PASTE_REQUIREMENT_OR_RESTATED_REQUIREMENT}
"""

Test Scenarios:

"""
{PASTE_APPROVED_TEST_SCENARIOS}
"""

Additional Business Rules / Acceptance Criteria, if available:

"""
{PASTE_ACCEPTANCE_CRITERIA_OR_BUSINESS_RULES}
"""

For each applicable test scenario, create detailed test cases.

Make sure the test cases cover:

1. **Positive Flow**
   Verify that the expected successful behavior works correctly.

2. **Negative Flow**
   Verify how the system behaves when invalid actions, data, or
   failure conditions are introduced.

3. **Validation**
   Cover required fields, invalid formats, incorrect values,
   duplicate values, and other validations defined by the requirement.

4. **Boundary Conditions**
   Cover relevant minimum, maximum, empty, zero, length, size,
   quantity, date, or other defined limits.

5. **Business Rules**
   Verify each important rule, condition, calculation, or restriction.

6. **Permissions**
   Where applicable, verify allowed and restricted actions for
   different users or roles.

7. **State and Data**
   Verify important state changes, saved data, updates, deletion,
   persistence, and consistency.

8. **Error Handling**
   Verify that failures are handled correctly and that the user
   receives the expected feedback where defined.

9. **Integration / Dependency**
   Where applicable, verify behavior when interacting with APIs,
   databases, notifications, external services, or dependent features.

10. **Regression Impact**
    Include important cases that should be retained for future
    regression testing.

For every test case:

- Give it a unique Test Case ID.
- Map it to the relevant Scenario ID.
- Write a clear test case title.
- Include preconditions when required.
- Include required test data.
- Write numbered, easy-to-follow test steps.
- Provide an expected result for each step or for the complete action,
  whichever is clearer.
- Keep the test case focused on one main objective.
- Avoid unnecessary repetition.
- Do not combine unrelated validations into one test case.
- Do not invent expected behavior that is not supported by the
  requirement or approved clarification.

Assign priority:

- **P0 — Critical:** Core business flow, critical functionality,
  security, or data integrity.
- **P1 — High:** Important functional, validation, permission,
  integration, or negative coverage.
- **P2 — Medium:** Boundary, alternate, or lower-risk coverage.
- **P3 — Low:** Nice-to-have or low-risk coverage.

Output in this format:

## Test Case Summary

**Feature:** [Feature name]

**Total Test Cases:** [number]

**P0:** [number]
**P1:** [number]
**P2:** [number]
**P3:** [number]

## Test Cases

### TC-001 — [Test Case Title]

**Scenario ID:** TS-001

**Priority:** P0

**Type:** Functional / Negative / Validation / Boundary / Security / etc.

**Preconditions:**
- ...

**Test Data:**
- ...

**Steps:**

1. ...
2. ...
3. ...

**Expected Result:**
- ...
- ...

Repeat the same structure for each test case.

## Scenario Coverage

| Scenario ID | Test Cases | Coverage |
|---|---|---|
| TS-001 | TC-001, TC-002 | Covered |
| TS-002 | TC-003 | Covered |
| TS-003 | TC-004, TC-005 | Covered |

## Test Data Notes

- ...
- ...

## Clarifications / Assumptions

- ...
- ...

If there are no open points, write "None."

Make the test cases practical and execution-ready. They should be
detailed enough for another QA engineer to execute without needing
additional explanation.
```


## Example

**Requirement:** *"Users can upload a profile picture. The image is displayed on their profile page."*

**Test Case:**

### TC-001 — Upload a valid profile picture

**Scenario ID:** TS-001

**Priority:** P0

**Type:** Functional

**Preconditions:**

* User is logged in.
* User is on the profile page.
* A valid supported image is available.

**Test Data:**

* Valid image within the allowed file size.

**Steps:**

1. Open the profile page.
2. Select the option to upload a profile picture.
3. Select the valid image.
4. Complete the upload.

**Expected Result:**

* The image is uploaded successfully.
* The uploaded image is displayed as the user's profile picture.
* No upload error is shown.


### TC-002 — Upload an unsupported image format

**Scenario ID:** TS-002

**Priority:** P1

**Type:** Validation

**Preconditions:**

* User is logged in and on the profile page.

**Test Data:**

* Image in an unsupported format.

**Steps:**

1. Select the option to upload a profile picture.
2. Select the unsupported image.
3. Attempt to complete the upload.

**Expected Result:**

* The system rejects the unsupported file.
* An appropriate validation message is displayed.
* The existing profile picture, if any, remains unchanged.


## Notes for reviewers

* Test cases should be created from **approved scenarios**, not directly from assumptions.
* Keep positive, negative, validation, and boundary coverage separate when they have different objectives.
* Steps should be simple and executable; avoid unnecessary wording.
* Expected results should describe the behavior that is actually required.
* Do not add assumptions silently. Raise unclear behavior under **Clarifications / Assumptions**.
* Each important test scenario should have at least one corresponding test case.
* Keep critical and high-priority cases suitable for future regression testing.
* The final test cases should be ready to move directly into test execution or a test management tool.

