# Testing Approach

## Purpose

Recommend a practical, risk-based testing approach for a user story or feature by identifying applicable testing types, coverage areas, priorities, dependencies, and potential risks.

## When to use

Use this prompt during requirement analysis, sprint planning, or before test case design to determine how a new feature, enhancement, or change should be tested.

## Inputs required

- `{{STORY_DESCRIPTION}}` — **Required:** Provide the user story describing the functionality, business objective, and expected user behavior.
  - **Example:** As a customer, I want to search the course catalog so that I can find courses relevant to my interests.

- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Provide the numbered acceptance criteria defining the expected functionality, validations, and business rules.
  - **Example:** AC-01: Users can search courses by keyword. AC-02: Users can filter courses by subject and grade. AC-03: Matching courses are displayed.

## Prompt

```text
Role:
Act as a Senior QE Analyst with expertise in
functional, API, integration, regression, automation,
and risk-based testing.

Task:
Analyze the provided user story and acceptance criteria
to recommend a practical testing approach.

Inputs:

STORY_DESCRIPTION:
{{STORY_DESCRIPTION}}

ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}

Instructions:

1. Understand Requirements
   - Identify the feature objective and expected behavior.
   - Identify key business rules and validations.
   - Highlight unclear or missing requirements.

2. Identify Applicable Testing Types
   - Recommend relevant testing types such as:
     Functional, Negative, Boundary, API, Integration,
     Regression, UI, Accessibility, Security, and Performance.
   - Explain why each testing type is required.
   - Exclude testing types that are not applicable.

3. Define Testing Coverage
   - Identify major workflows and validations to cover.
   - Include positive, negative, and edge-case coverage
     where applicable.
   - Map coverage areas to acceptance criteria.
   - Do not generate detailed test cases or test steps.

4. Prioritize Testing
   - Assign P1 (Critical), P2 (High), or P3 (Medium/Low)
     based on business impact, complexity, and risk.
   - Identify critical workflows requiring early validation.

5. Recommend Execution Approach
   - Recommend manual, automated, or hybrid testing.
   - Identify suitable automation opportunities.
   - Consider existing test coverage if available.

6. Identify Risks and Dependencies
   - Highlight requirement gaps, integration dependencies,
     environment needs, and potential testing risks.
   - Recommend actions to address identified risks.

7. Define Entry Conditions
   - Identify prerequisites such as clear requirements,
     available builds, environments, test data, and access.

Rules:
- Base recommendations on the supplied requirements.
- Do not invent functionality or business rules.
- Recommend only relevant testing types.
- Explain testing priorities and significant exclusions.
- Clearly label assumptions and missing information.
- Mark unavailable information as "Not provided".
- Do not generate detailed test cases or automation scripts.
- Present the output using clear headings and tables.
```

## Expected output

Generate a structured **Testing Approach Report** containing:

1. **Feature Overview:** Brief summary of the functionality and business objective.
   - *Example:* Enable customers to search and filter courses by keyword, subject, and grade.

2. **Recommended Testing Types:** Applicable testing types with justification for their selection.
   - *Example:* Functional Testing — Validate search and filters; Negative Testing — Validate searches with no matching results.

3. **Testing Coverage:** High-level workflows, validations, and edge cases mapped to acceptance criteria.
   - *Example:* Verify keyword search (AC-01), subject/grade filters (AC-02), and matching results (AC-03).

4. **Risk-Based Priorities:** Prioritized testing areas based on business impact and likelihood of failure.
   - *Example:* P1 — Search accuracy; P2 — Combined filter behavior; P3 — Optional UI presentation checks.

5. **Execution Approach:** Recommended manual, automated, or hybrid testing with automation opportunities.
   - *Example:* Automate stable search/filter regression checks; manually explore unusual search combinations.

6. **Risks and Dependencies:** Potential testing blockers, requirement gaps, and mitigation recommendations.
   - *Example:* Risk — Unclear behavior for empty search results; Action — Confirm expected behavior with the Product Owner.

7. **Entry Conditions:** Prerequisites required before testing can begin.
   - *Example:* Search feature deployed, test catalog data available, and acceptance criteria clarified.

## Example

**Synthetic input:**

```text
STORY_DESCRIPTION:
As a student, I want to search and filter the course
catalog so that I can find relevant courses.

ACCEPTANCE_CRITERIA:
AC-01: Users can search courses by keyword.
AC-02: Users can filter courses by subject and grade.
AC-03: Matching courses are displayed.
```

**Illustrative response (synthetic, not executed):**

### 1. Recommended Testing Types

| Testing Type | Coverage | Reason |
|---|---|---|
| Functional | Search and filter functionality | Validate expected behavior |
| Negative | No matching courses | Check handling of unsuccessful searches |
| Boundary | Empty and unusually long keywords | Explore input limits; expected limits need clarification |
| Integration | Search results from catalog service, if applicable | Validate data retrieval |
| Regression | Existing catalog browsing | Detect unintended changes |
| Accessibility | Keyboard access and filter labels | Check usability with assistive technologies |

### 2. Testing Coverage and Priorities

| Coverage Area | AC Mapping | Priority |
|---|---|---|
| Keyword search | AC-01 | P1 |
| Subject and grade filters | AC-02 | P1 |
| Matching course results | AC-03 | P1 |
| No matching results | Requirement clarification | P2 |
| Empty/long keyword handling | Requirement clarification | P2 |

*Priorities are illustrative and should be confirmed against business impact.*

### 3. Execution Approach

| Testing Area | Recommended Approach |
|---|---|
| Search and filters | Automated regression |
| Negative and edge cases | Manual initially; automate stable cases |
| Exploratory testing | Manual |
| Accessibility checks | Automated scan + manual verification |

### 4. Risks and Dependencies

| Risk / Dependency | Recommended Action |
|---|---|
| Empty search behavior undefined | Clarify expected results |
| Catalog test data unavailable | Prepare representative course data |
| Search service integration unknown | Confirm architecture and integration scope |

### 5. Entry Conditions

- Acceptance criteria reviewed and clarified.
- Testable application build available.
- QA environment and relevant test data ready.
- Required user access and integrations available.

## Limitations

- The recommended approach depends on the completeness of the user story and acceptance criteria.
- Unknown integrations, business rules, or technical dependencies may change the testing scope.
- Automation recommendations require confirmation of existing framework capabilities and test stability.
- This prompt defines the testing approach only; it does not generate detailed test cases, execute tests, or confirm actual coverage.
- Final priorities and testing recommendations require QA and stakeholder review.

Shared privacy, evidence, authorization, and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version

- **Owner:** QE Prompt Library maintainers (assign named owner before publication)
- **Version:** 1.2.0
- **Status:** Draft for team review
