# Regression Strategy

## Purpose

Use the provided App Overview, Epic Description, Story Description, and Acceptance Criteria to determine what existing functionality should be included in regression testing because of the requested change.

The goal is to identify a **focused, risk-based regression scope**, not automatically recommend execution of the entire regression suite.

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

Analyze the four inputs and determine the likely regression impact of the requested change.

Identify:

1. The functionality directly changed by the story.
2. Existing functionality that may be affected directly.
3. Existing functionality that may be affected indirectly through shared workflows, data, rules, or dependencies described in the requirement.
4. Critical user journeys that should be considered for regression.
5. The minimum targeted regression scope.
6. Areas where broader regression may be needed.
7. Any uncertainty that requires clarification before regression scope can be finalized.

Prioritize regression based on likely impact and business significance.
Do not mark unrelated functionality as regression scope without a clear reason.

---

## Expected Output

### 1. Changed Functionality

Clearly identify what functionality is being added, changed, or removed.

### 2. Regression Scope

| Existing Functionality | Potential Impact | Regression Priority | Reason |
|---|---|---|---|
| | | High / Medium / Low | |

### 3. Critical Regression Scenarios

List the most important existing workflows that should be retested.

### 4. Minimum Regression Scope

State the smallest regression set that should be executed to provide reasonable confidence for the change.

### 5. Extended Regression Scope

Identify additional areas that should be considered when time and risk justify broader regression.

### 6. What Does NOT Need Regression

Identify clearly unrelated areas that should not be included, based on the supplied information.

### 7. Needs Clarification

List missing or ambiguous information that could change the regression scope.

### 8. Final Recommendation

Provide:

- **Minimum Regression:**
- **Recommended Regression:**
- **Extended Regression:**
- **Not Required:**
- **Needs Clarification:**
