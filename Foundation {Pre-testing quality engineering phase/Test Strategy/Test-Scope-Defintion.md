# Test Scope Definition

## Purpose

Use the provided **App Overview, Epic Description, Story Description, and Acceptance Criteria** to clearly determine:

* **What should be tested**
* **What should not be tested**
* **What needs clarification before testing**

The output should give the QA team a clear testing boundary before creating test cases.

---

## Input

Provide the following four inputs:

### APP_OVERVIEW

```text
[Enter the high-level overview of the application/product]
```

### EPIC_DESCRIPTION

```text
[Enter the epic description]
```

### STORY_DESCRIPTION

```text
[Enter the story description]
```

### ACCEPTANCE_CRITERIA

```text
[Enter all acceptance criteria]
```

---

## Prompt

Analyze the provided **App Overview, Epic Description, Story Description, and Acceptance Criteria** and define the test scope.

Determine what functionality and scenarios the QA team should test and what functionality should be excluded from testing.

Use the following rules:

1. Consider all functionality explicitly described in the **Story Description**.
2. Consider every **Acceptance Criterion** as part of the test scope.
3. Identify relevant positive scenarios.
4. Identify relevant negative and validation scenarios.
5. Identify boundary or edge scenarios when they are logically applicable.
6. Identify existing functionality that may be impacted by the story and therefore requires regression testing.
7. Do not include unrelated functionality merely because it exists in the application.
8. Do not invent requirements that are not supported by the provided inputs.
9. If something cannot be determined from the inputs, place it under **Needs Clarification** instead of assuming.
10. The final output must clearly separate **What to Test** and **What Not to Test**.

---

# Expected Output

## 1. Requirement Understanding

Provide a simple summary of what the story is intended to achieve.

```text
Business Objective:
[What business/user problem is being addressed]

Feature/Change:
[What is being added, changed, or removed]
```

---

## 2. What to Test

List all functionality and scenarios that should be included in testing.

| # | What to Test | Reason |
| - | ------------ | ------ |
| 1 |              |        |
| 2 |              |        |
| 3 |              |        |

Include, where applicable:

* Core functionality
* Acceptance criteria
* Positive scenarios
* Negative scenarios
* Validations
* Boundary/edge cases
* Impacted existing functionality
* Relevant integrations

---

## 3. What NOT to Test

List functionality that should be excluded from testing because it is unrelated to the requested change or outside the identified impact area.

| # | What NOT to Test | Reason |
| - | ---------------- | ------ |
| 1 |                  |        |
| 2 |                  |        |
| 3 |                  |        |

Do not mark something as out of scope simply because it is not explicitly mentioned in the story. First determine whether the changed functionality could affect it.

---

## 4. Regression Scope

Identify existing functionality that may be affected by the new or changed functionality.

| # | Existing Functionality | Why Regression Is Needed | Priority            |
| - | ---------------------- | ------------------------ | ------------------- |
| 1 |                        |                          | High / Medium / Low |
| 2 |                        |                          | High / Medium / Low |

If no regression impact is identified, state:

```text
No specific regression impact identified from the provided requirements.
```

---

## 5. Needs Clarification

List anything that prevents the testing scope from being completely defined.

| # | Clarification Needed | Why It Matters |
| - | -------------------- | -------------- |
| 1 |                      |                |
| 2 |                      |                |

Examples:

* Missing expected behavior
* Ambiguous acceptance criteria
* Undefined validation rules
* Missing business rules
* Unclear integration behavior
* Unclear error handling

Do not make assumptions to fill these gaps.

---

# Final Test Scope

At the end, provide a concise summary in exactly this format:

### WHAT TO TEST

```text
1. ...
2. ...
3. ...
```

### WHAT NOT TO TEST

```text
1. ...
2. ...
3. ...
```

### REGRESSION TO CONSIDER

```text
1. ...
2. ...
```

### NEEDS CLARIFICATION

```text
1. ...
2. ...
```

---

## Scope Decision Rules

The final scope must follow this logic:

**Story + Acceptance Criteria → Core Test Scope**

**Changed Functionality → Impacted Areas → Regression Scope**

**Unrelated Functionality → Out of Scope**

**Missing/Ambiguous Requirement → Needs Clarification**

The output must be based only on the provided inputs and must not invent functionality, business rules, or expected behavior.
