

# Requirement-to-Test Traceability

## Purpose

Analyze the provided requirements and existing test cases to establish traceability between requirements and tests.

The analysis must:
1. Map each requirement and acceptance criterion to relevant test cases.
2. Identify requirements that are fully, partially, or not covered.
3. Review the traceability for completeness, correctness, and consistency.
4. Identify test cases that do not map to any requirement.
5. Highlight missing test coverage and recommend additional test scenarios where required.

---

## Standard Input Contract

| Input | Required | Purpose |
|---|---|---|
| `APP_OVERVIEW` | No | Provides high-level context about the application/product. |
| `EPIC_DESCRIPTION` | No | Provides broader business and feature context. |
| `STORY_DESCRIPTION` | Yes | Defines the functionality or business requirement being delivered. |
| `ACCEPTANCE_CRITERIA` | Yes | Defines specific conditions that must be satisfied. |
| `TEST_CASES` | Yes | Provides the existing test cases to be mapped against requirements. |
| `BUSINESS_RULES` | No | Provides additional business rules that may require test coverage. |
| `KNOWN_REQUIREMENTS_OR_CONSTRAINTS` | No | Provides additional requirements, limitations, or constraints relevant to testing. |

### Input Guidelines

- Do not assume requirements that are not provided.
- Treat the Acceptance Criteria as explicit requirements.
- Use Business Rules as additional requirements when provided.
- Use the existing test cases as the source for determining current test coverage.
- Do not consider a requirement covered merely because a test case appears related by wording.
- A test case must validate the actual behavior or condition described by the requirement to be considered valid coverage.
- Clearly distinguish between full, partial, and missing coverage.

---

## Analysis Instructions

### 1. Requirement Identification

Identify all testable requirements from:

- Story Description
- Acceptance Criteria
- Business Rules
- Explicit requirements or constraints provided in the input

Assign a unique identifier where one is not already available.

Do not create requirements that are not supported by the provided inputs.

---

### 2. Requirement-to-Test Mapping

For each identified requirement:

- Identify all relevant test cases.
- Explain briefly why each test case covers the requirement.
- Determine whether the requirement is fully or partially covered.
- Mark the requirement as not covered if no suitable test case exists.

Use the following coverage categories:

- **Fully Covered** – One or more test cases adequately validate the complete requirement.
- **Partially Covered** – Test cases validate only some aspects of the requirement.
- **Not Covered** – No suitable test case validates the requirement.

---

### 3. Requirement Coverage Analysis

Analyze the overall coverage and identify:

- Fully covered requirements.
- Partially covered requirements.
- Requirements with no test coverage.
- Acceptance Criteria without corresponding test cases.
- Business rules without corresponding test coverage.
- Important positive, negative, boundary, or exception scenarios that appear to be missing.

Do not classify a scenario as missing solely because it is not explicitly mentioned in the Acceptance Criteria. Clearly label such scenarios as **recommended additional coverage** rather than requirement gaps.

---

### 4. Traceability Review

Review the mapping for:

#### Forward Traceability

Verify that every requirement has one or more appropriate test cases.

Identify:

- Uncovered requirements.
- Partially covered requirements.
- Requirements with insufficient test coverage.

#### Backward Traceability

Verify that every test case maps to at least one requirement or valid testing objective.

Identify:

- Orphan test cases.
- Test cases that do not appear to validate any provided requirement.
- Test cases that may be testing functionality outside the stated scope.

#### Mapping Quality

Check whether:

- The test case actually validates the mapped requirement.
- The mapping is logically correct.
- Multiple requirements are incorrectly treated as covered by an unrelated test.
- Important conditions within a requirement are not tested.
- Test cases are duplicated unnecessarily.

---

## Coverage Rules

Use the following rules when determining coverage:

### Fully Covered

Mark as **Fully Covered** only when the available test cases validate all important conditions of the requirement.

### Partially Covered

Mark as **Partially Covered** when:

- Only some conditions are tested.
- Only the positive scenario is tested when the requirement contains additional conditions.
- Boundary or exception behavior required by the requirement is not tested.

### Not Covered

Mark as **Not Covered** when no existing test case validates the requirement.

### Recommended Additional Coverage

If a useful test scenario is not explicitly required but would improve test quality, identify it separately.

Examples:

- Negative scenarios.
- Boundary conditions.
- Invalid input.
- Error handling.
- Permission/access scenarios.
- Data validation.
- State transitions.

Do not represent these recommendations as mandatory requirement gaps unless supported by the provided requirements.

---

## Expected Output

### 1. Requirement-to-Test Traceability Matrix

| Requirement ID | Requirement / Acceptance Criteria | Test Case ID(s) | Coverage | Reason / Observation |
|---|---|---|---|---|

---

### 2. Coverage Summary

Provide:

| Coverage Category | Count |
|---|---:|
| Fully Covered | |
| Partially Covered | |
| Not Covered | |
| Total Requirements | |

Calculate coverage based on the identified requirements and clearly explain the calculation used.

---

### 3. Coverage Gaps

List all requirements or acceptance criteria that are:

- Partially covered.
- Not covered.

For each gap, provide:

| Requirement ID | Gap | Impact | Recommended Test Coverage |
|---|---|---|---|

---

### 4. Orphan Test Cases

Identify test cases that cannot be mapped to any provided requirement.

| Test Case ID | Test Case | Observation |
|---|---|---|

If there are no orphan test cases, explicitly state:

> No orphan test cases identified.

---

### 5. Recommended Additional Test Scenarios

Identify useful scenarios that are not currently covered.

Separate these from actual requirement coverage gaps.

| Requirement ID | Recommended Scenario | Reason |
|---|---|---|

---

### 6. Traceability Review Findings

Summarize the overall traceability quality.

Include:

- Requirement coverage issues.
- Incorrect or weak mappings.
- Orphan test cases.
- Missing test scenarios.
- Ambiguous requirements affecting traceability.
- Any other significant observations.

Use severity where appropriate:

- **High**
- **Medium**
- **Low**

---

## Final Assessment

Provide an overall assessment using one of the following:

### Good Traceability

Use when requirements have adequate test coverage and mappings are accurate.

### Traceability Gaps Identified

Use when some requirements have partial or missing coverage.

### Significant Traceability Gaps

Use when important requirements are not covered or the existing test suite has substantial mapping issues.

Provide a concise explanation for the assessment.

---

## Important Constraints

- Do not invent requirements, acceptance criteria, or test cases.
- Do not modify the supplied test cases.
- Do not assume a test case provides coverage based only on similar keywords.
- Do not treat recommended test scenarios as requirement gaps unless the requirement explicitly requires them.
- Preserve existing requirement and test case IDs whenever available.
- If an input is missing, explicitly state that the analysis is limited by the missing information.
- Do not claim complete coverage when the available information is insufficient to establish it.
- If the requirements are ambiguous, flag the ambiguity rather than making assumptions.
- Keep the analysis understandable to QA, developers, Business Analysts, and stakeholders.

## Primary Objective

The final output should clearly answer:

> **Does every stated requirement have appropriate test coverage, and can each test case be traced back to a valid requirement or testing objective?**