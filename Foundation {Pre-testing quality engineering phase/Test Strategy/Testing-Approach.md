# Testing Approach

## Purpose

Use the provided App Overview, Epic Description, Story Description, and Acceptance Criteria to determine the most appropriate overall testing approach for the requested change.

The output should tell the QA team **how the change should be tested**, not create detailed test cases.

---

## Input

### APP_OVERVIEW

```text
[Paste App Overview here]
```

### EPIC_DESCRIPTION

```text
[Paste Epic Description here]
```

### STORY_DESCRIPTION

```text
[Paste Story Description here]
```

### ACCEPTANCE_CRITERIA

```text
[Paste Acceptance Criteria here]
```

---

## Prompt

Analyze the four inputs and recommend the appropriate testing approach for the story.

Determine:

1. The primary functional testing approach.
2. Whether positive, negative, validation, boundary, and edge testing are relevant.
3. Whether regression testing is required and which areas are likely to be impacted.
4. Whether integration or end-to-end testing is relevant based on the described functionality.
5. Whether exploratory testing is useful for the change.
6. Any special testing focus caused by the business behavior described in the requirement.
7. Any areas that cannot be determined from the inputs and therefore need clarification.

Do not invent requirements or test types that are not justified by the supplied information.

---

## Expected Output

### 1. Recommended Testing Approach

| Testing Area | Recommendation | Reason |
|---|---|---|
| Functional testing | Required / Not Required / Clarification | |
| Positive testing | Required / Not Required / Clarification | |
| Negative testing | Required / Not Required / Clarification | |
| Validation testing | Required / Not Required / Clarification | |
| Boundary/edge testing | Required / Not Required / Clarification | |
| Regression testing | Required / Not Required / Clarification | |
| Integration testing | Required / Not Required / Clarification | |
| End-to-end testing | Required / Not Required / Clarification | |
| Exploratory testing | Required / Not Required / Clarification | |

### 2. Primary Testing Focus

Clearly state the main areas QA should concentrate on.

### 3. Regression Focus

Identify existing functionality that may be affected by the change.

### 4. Needs Clarification

List any requirement gaps or ambiguities that could change the testing approach.

### 5. Final Recommendation

Provide a concise summary:

- **Primary Approach:**
- **Key Testing Focus:**
- **Regression Focus:**
- **Needs Clarification:**
