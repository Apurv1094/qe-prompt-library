# Manual vs Automation Assessment

## Purpose

Use the provided App Overview, Epic Description, Story Description, and Acceptance Criteria to determine whether the relevant test scenarios are better suited for **Manual Testing**, **Automation**, or a **Hybrid Approach**.

The goal is to make a practical automation decision based on value, repeatability, stability, and maintenance effort.

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

Analyze the four inputs and determine which parts of the requested testing are suitable for manual testing, automation, or both.

Consider:

1. How repeatable the scenarios are likely to be.
2. Whether the expected behavior is stable and deterministic from the requirement.
3. Whether the scenario requires human observation, judgment, or exploration.
4. Whether the functionality is likely to be executed repeatedly, such as during regression.
5. Whether automation would provide meaningful time or coverage benefits.
6. Whether the scenario is likely to require frequent maintenance because of changing behavior or UI.
7. Whether the functionality appears suitable for UI, API, or another automation layer, based only on the supplied information.
8. Whether a hybrid approach is more appropriate than choosing only manual or automation.

Do not recommend automation simply because a scenario is technically automatable.
Do not assume implementation details that are not provided.

---

## Expected Output

### 1. Assessment

| Test Area / Scenario | Manual | Automation | Recommendation | Reason |
|---|---|---|---|---|
| | | | | |

Use **Yes/No/Unclear** for Manual and Automation.

### 2. Automation Suitability

Identify scenarios that are good candidates for automation and explain why.

### 3. Manual Testing Suitability

Identify scenarios that should remain manual and explain why.

### 4. Hybrid Testing Suitability

Identify areas where automation and manual testing should complement each other.

### 5. Maintenance / Value Consideration

Explain any situation where automation may technically be possible but may not provide sufficient long-term value.

### 6. Needs Clarification

List information that is missing and could materially change the recommendation.

### 7. Final Recommendation

Provide:

- **Manual Testing:**
- **Automation:**
- **Hybrid:**
- **Overall Recommendation:**
- **Main Rationale:**
