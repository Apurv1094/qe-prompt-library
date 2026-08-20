# Test Data

**Module:** Manual QA

**Sub Module:** Test Design

**Purpose:** Identify the data required to execute test cases, including valid, invalid, boundary, duplicate, and role-specific data where applicable.


## When to use this prompt

* After test cases are created and before test execution begins.
* When a feature requires specific users, records, files, values, or other inputs.
* When positive, negative, or boundary testing needs different data.


## What Test Data is (and isn't)

Test Data is the **actual input or existing data used while executing a test case**.

It is **not** the test case itself. The test case defines what to do; test data provides the values needed to perform it.

For example:

* **Test Case:** Verify login with valid credentials.
* **Test Data:** Registered email + valid password.


## Prompt

Preparing test data for a feature.

Requirement:

"""
{PASTE_REQUIREMENT}
"""

Test Cases:

"""
{PASTE_TEST_CASES}
"""

Identify the test data required to execute the test cases.

Consider the following where applicable:

1. **Valid Data**
   Data required for successful scenarios.

2. **Invalid Data**
   Incorrect, malformed, or rejected values.

3. **Boundary Data**
   Minimum, maximum, zero, empty, length, size, or other limits.

4. **Duplicate Data**
   Existing values or records used to verify duplicate handling.

5. **Role / State Data**
   Users or records with different roles or states.

For each data item:
- Give it a unique Data ID.
- Clearly mention the data and its purpose.
- Do not use real sensitive or production data.
- Do not invent undefined business values; mark them as
  "To be defined".

Output in this format:

## Test Data Summary

**Feature:** [Feature name]

**Total Data Sets:** [number]

## Test Data

| Data ID | Category | Test Data | Purpose |
|---|---|---|---|
| TD-001 | Valid | ... | ... |
| TD-002 | Invalid | ... | ... |
| TD-003 | Boundary | ... | ... |

## Data Preparation Notes

- ...
- ...

## Clarifications Needed

- ...

If there are no open points, write "None."
```

---

## Example

**Requirement:** *"Users can register using their name, email, and password. The email must be unique."*

| Data ID | Category  | Test Data                                  | Purpose                 |
| ------- | --------- | ------------------------------------------ | ----------------------- |
| TD-001  | Valid     | Valid name + unique email + valid password | Successful registration |
| TD-002  | Invalid   | Invalid email format                       | Email validation        |
| TD-003  | Duplicate | Already registered email                   | Duplicate validation    |
| TD-004  | Boundary  | Password at minimum allowed length         | Boundary validation     |


## Notes for reviewers

* Test data should be prepared before execution.
* Keep valid, invalid, and boundary data separate where required.
* Never use real sensitive customer or production data.
* If a required value is not defined, raise it for clarification instead of assuming it.
