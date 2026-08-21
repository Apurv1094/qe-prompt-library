# Test Scenario Creation

**Module:** Manual QA

**Sub Module:** Test Design

**Purpose:** Convert a requirement into clear, high-level test scenarios that define what needs to be tested before writing detailed test cases. The focus is on covering the main user flow as well as negative, boundary, validation, permission, and alternate scenarios that could affect the feature.



## When to use this prompt

* Right after the requirement has been understood and the important gaps have been identified, before detailed test case creation starts.

* During test planning or story refinement, when the team needs to agree on the overall testing scope.

* When a feature has multiple user flows, validations, business rules, or possible failure conditions.

* When you want to make sure the obvious happy path is not the only thing being covered.

---

## What Test Scenario Creation is (and isn't)

This is a **high-level test coverage activity** — "what should we test for this requirement?"

It is **not** about writing step-by-step test cases. At this stage, we define the scenarios that need coverage. The detailed steps, test data, and expected results are handled later during Test Case Creation.

For example:

* **Test Scenario:** Verify that a user can log in with valid credentials.
* **Test Case:** Enter a registered username, enter the correct password, click Login, and verify that the user is taken to the dashboard.

The scenario defines **what needs to be tested**; the test case defines **how it will be tested**.

---

## Prompt

```text
You are a senior QA engineer creating test scenarios for a
requirement.

Your job is to identify the important things that need to be tested
for this requirement. Do not write detailed test cases or step-by-step
instructions.

Requirement:

"""
{PASTE_REQUIREMENT_OR_RESTATED_REQUIREMENT}
"""

Read the requirement carefully and first understand the expected user
flow and business behavior.

Then identify the test scenarios that should be covered.

Make sure to think about:

1. **Main Flow**
   What is the normal successful flow that the user should be able
   to complete?

2. **Alternate Flows**
   Are there other valid ways the user can use the feature or reach
   the same outcome?

3. **Negative Scenarios**
   What can go wrong? Consider invalid actions, failed operations,
   unavailable services, and unexpected conditions.

4. **Input Validation**
   What happens with missing, invalid, incorrect, duplicate, or
   unusual input?

5. **Boundary Conditions**
   What happens at minimum, maximum, zero, empty, length, size,
   quantity, date, or other defined limits?

6. **Business Rules**
   What rules, restrictions, calculations, or conditions mentioned
   in the requirement need to be verified?

7. **Permissions**
   If different users or roles are involved, what should each user
   be allowed or not allowed to do?

8. **State Changes**
   What happens when the feature is used in different states, or
   when the state changes during the flow?

9. **Data**
   What should happen when data is created, updated, deleted,
   retrieved, or used again later?

10. **Dependencies**
    If the feature depends on an API, database, notification,
    external service, or another feature, what should be tested
    around that dependency?

11. **Retry / Recovery**
    What happens when an operation fails and the user tries again,
    cancels it, or comes back to complete it later?

12. **Security**
    Are there any scenarios related to authentication,
    authorization, access control, sessions, or sensitive data?

Do not create scenarios for areas that are clearly not relevant to
the requirement.

Keep each scenario at a high level. Do not turn the scenarios into
test cases.

For each scenario:
- Give it a unique ID.
- Write it as a clear "Verify..." statement.
- Keep one main testing objective per scenario.
- Avoid duplicate scenarios.
- Do not assume behavior that is not defined in the requirement.
- If an important behavior is unclear, mention it as a clarification
  instead of inventing an expected result.

Assign priority:

- P0 — Critical: Core functionality, major business flow,
  security, or data integrity.
- P1 — High: Important functional, validation, permission,
  integration, or negative scenarios.
- P2 — Medium: Boundary, alternate, or lower-risk scenarios.
- P3 — Low: Nice-to-have or low-risk coverage.

Output in this format:

## Scenario Coverage Summary

**Feature:** [Feature name]

**Overall Coverage Risk:** [Low / Medium / High]

**Scenario Count:** [number]

## Test Scenarios

| Scenario ID | Category | Test Scenario | Priority |
|---|---|---|---|
| TS-001 | Main Flow | Verify ... | P0 |
| TS-002 | Negative | Verify ... | P1 |
| TS-003 | Validation | Verify ... | P1 |



## Example

**Requirement:** *"Users can upload a profile picture. The image is displayed on their profile page."*

**Test Scenario (excerpt):**

| Scenario ID | Category            | Test Scenario                                                                                 | Priority |
| ----------- | ------------------- | --------------------------------------------------------------------------------------------- | -------- |
| TS-001      | Main Flow           | Verify that a user can upload a valid profile picture and see it on the profile page          | P0       |
| TS-002      | Validation          | Verify that the system does not allow an unsupported image format                             | P1       |
| TS-003      | Boundary Conditions | Verify that the system handles an image at the maximum allowed file size                      | P1       |
| TS-004      | Negative            | Verify that the user receives appropriate feedback when the upload fails                      | P1       |
| TS-005      | Alternate Flow      | Verify that a user can replace an existing profile picture                                    | P1       |
| TS-006      | Data                | Verify that the uploaded picture remains available after refreshing or revisiting the profile | P1       |
| TS-007      | Permissions         | Verify that a user cannot change another user's profile picture                               | P0       |

**Clarifications Needed:**

* What image formats are supported?
* What is the maximum allowed image size?
* Can the user remove the existing picture without uploading a new one?

---

## Notes for reviewers

* Scenario creation should cover the **overall testing scope**, not just the happy path.
* Do not create detailed steps at this stage; those belong in Test Case Creation.
* A good scenario should be specific enough to test but broad enough that multiple test cases can be created from it when needed.
* If the requirement does not define an important behavior, raise it as a clarification instead of assuming the expected behavior.
* Avoid duplicate scenarios. Different input values do not always require separate scenarios if they test the same behavior.
* The final scenarios should give the QA team a clear starting point for detailed test case design.


