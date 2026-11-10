# Requirement-to-Test Traceability

## Purpose

Analyze the provided requirements and existing test cases to establish traceability between requirements and tests.

The analysis must:

1. Map each requirement and acceptance criterion to relevant test cases.
2. Identify requirements that are fully, partially, or not covered.
3. Review traceability for completeness, correctness, and consistency.
4. Identify test cases that do not map to any requirement.
5. Highlight missing test coverage and recommend additional test scenarios where required.

---

## Required Inputs

### STORY_DESCRIPTION

```text
{{STORY_DESCRIPTION}}
```

### ACCEPTANCE_CRITERIA

```text
{{ACCEPTANCE_CRITERIA}}
```

### TEST_CASES

```text
{{TEST_CASES}}
```

---

## Prompt

Act as a Senior Quality Engineer supporting a software delivery team.

Analyze the supplied Story Description, Acceptance Criteria, and existing Test Cases to establish requirement-to-test traceability.

Determine:

1. Which requirements and acceptance criteria are covered by existing test cases.
2. Which requirements are partially covered or not covered.
3. Whether each test case correctly validates its mapped requirement.
4. Whether any test cases are unrelated to the provided requirements.
5. Whether additional test scenarios are required to improve coverage.

### Analysis Instructions

**1. Requirement Identification**

- Identify testable requirements from the Story Description and Acceptance Criteria.
- Treat Acceptance Criteria as explicit requirements.
- Assign unique requirement IDs where they are not provided.
- Avoid counting the same requirement twice when it appears in both the Story Description and Acceptance Criteria.
- Do not invent requirements.

**2. Requirement-to-Test Mapping**

For each identified requirement:

- Identify relevant existing test cases.
- Preserve existing test case IDs.
- Explain briefly how each test case validates the requirement.
- Determine whether coverage is full, partial, or missing.
- Do not assume coverage based only on similar wording.

**3. Coverage Analysis**

Use the following categories:

- **Fully Covered:** Existing test cases validate all important conditions explicitly described by the requirement.
- **Partially Covered:** Existing test cases validate only some conditions of the requirement.
- **Not Covered:** No suitable existing test case validates the requirement.

**4. Traceability Review**

Review both directions:

- **Forward Traceability:** Verify that every identified requirement maps to appropriate test cases.
- **Backward Traceability:** Verify that every test case maps to a provided requirement or a clearly identifiable testing objective.

Identify:

- Missing or insufficient coverage.
- Incorrect or weak mappings.
- Orphan test cases.
- Duplicate test cases.
- Test cases outside the stated scope.
- Ambiguous requirements affecting traceability.

**5. Additional Test Coverage**

Identify useful missing scenarios such as:

- Positive scenarios.
- Negative scenarios.
- Boundary conditions.
- Invalid input handling.
- Error handling.
- Permission or access validation.
- State transitions.

Clearly separate additional testing recommendations from actual requirement coverage gaps.

Do not classify a scenario as a mandatory requirement gap unless it is supported by the supplied Story Description or Acceptance Criteria.

---

## Expected Output

### 1. Requirement-to-Test Traceability Matrix

| Requirement ID | Requirement / Acceptance Criteria | Test Case ID(s) | Coverage | Reason / Observation |
|---|---|---|---|---|

For each requirement, identify the mapped test cases and explain the coverage status.

### 2. Coverage Summary

| Coverage Category | Count |
|---|---:|
| Fully Covered | |
| Partially Covered | |
| Not Covered | |
| Total Requirements | |

Calculate:

**Full Coverage % = (Fully Covered Requirements / Total Requirements) × 100**

Also report the number of partially covered and uncovered requirements.

Do not count partially covered requirements as fully covered.

### 3. Coverage Gaps

Identify requirements that are partially covered or not covered.

| Requirement ID | Gap | Impact | Recommended Test Coverage |
|---|---|---|---|

If no coverage gaps exist, state:

**No requirement coverage gaps identified.**

### 4. Orphan Test Cases

Identify test cases that cannot be mapped to any supplied requirement or valid testing objective.

| Test Case ID | Test Case | Observation |
|---|---|---|

If no orphan test cases exist, state:

**No orphan test cases identified.**

### 5. Recommended Additional Test Scenarios

Identify useful additional testing scenarios that are not currently covered.

| Requirement ID | Recommended Scenario | Reason |
|---|---|---|

Use `N/A` for Requirement ID when a recommendation is not tied to an explicit requirement.

Do not mix these recommendations with mandatory requirement coverage gaps.

### 6. Traceability Review Findings

Summarize significant findings related to:

- Requirement coverage.
- Incorrect or weak mappings.
- Orphan test cases.
- Missing scenarios.
- Duplicate tests.
- Ambiguous requirements.

Assign severity where appropriate:

- **High:** Important requirement has missing coverage or a critical mapping issue.
- **Medium:** Partial coverage or meaningful traceability weakness.
- **Low:** Minor duplication or improvement opportunity.

---

## Final Assessment

Provide one of the following assessments:

**Good Traceability**

Requirements have adequate test coverage, and mappings are accurate.

**Traceability Gaps Identified**

Some requirements have partial or missing coverage.

**Significant Traceability Gaps**

Important requirements are uncovered, or substantial mapping issues exist.

Provide a brief justification and identify the most important next action for the QA team.

---

## Rules

- Use only the three supplied inputs.
- Do not invent requirements, acceptance criteria, or test cases.
- Do not modify existing test cases.
- Preserve existing requirement and test case IDs.
- Assign requirement IDs only when missing.
- Do not assume coverage based on similar keywords.
- Mark requirements as fully covered only when all explicitly required conditions are validated.
- Separate actual requirement gaps from recommended additional coverage.
- Identify missing information and ambiguities.
- If test case steps or expected results are insufficient to verify coverage, state the limitation rather than assuming coverage.
- Do not claim complete coverage without sufficient evidence.
- Keep the output concise, practical, and understandable to QA engineers, developers, and Business Analysts.

---

## Primary Objective

The final output must clearly answer:

**Does every stated requirement have appropriate test coverage, and can each existing test case be traced back to a valid requirement or testing objective?**
