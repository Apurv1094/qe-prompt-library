# Test Plan and Estimation

## Purpose

Create a practical, risk-based test plan with testing scope, strategy, effort estimation, resource allocation, timelines, and potential risks for a software release.

## When to use

Use this prompt during sprint planning, release planning, or when estimating QA effort for new features, enhancements, or regression testing.

## Inputs required

- `{{RELEASE_SCOPE}}` — **Required:** Provide the features, user stories, enhancements, integrations, and exclusions planned for testing.
  - **Example:** Login enhancement, shopping cart discount functionality, order reporting changes, and payment gateway integration.

- `{{TEAM_CAPACITY}}` — **Required:** Provide the number of QA engineers, their availability, allocation, and relevant testing skills.
  - **Example:** 2 QAs available for 8 hours/day; QA1 handles manual/API testing and QA2 handles automation/regression testing.

- `{{TIMELINE}}` — **Required:** Provide the testing duration, target release date, and important testing milestones.
  - **Example:** 2-week release cycle, functional testing in Week 1, regression testing in Week 2, and release at the end of Week 2.

## Prompt

```text
Role:
Act as a Senior QA Test Manager and QE Automation Architect.

Task:
Analyze the provided release scope, team capacity, and
timeline to prepare a realistic Test Plan and Estimation
Report for the software release.

Inputs:

RELEASE_SCOPE:
{{RELEASE_SCOPE}}

TEAM_CAPACITY:
{{TEAM_CAPACITY}}

TIMELINE:
{{TIMELINE}}

Instructions:

1. Analyze Release Scope
   - Identify features, integrations, and impacted areas.
   - Define in-scope and out-of-scope testing.
   - Highlight missing or unclear requirements.

2. Define Testing Approach
   - Recommend applicable testing types such as smoke,
     functional, API, integration, regression, and
     non-functional testing.
   - Identify manual and automation testing opportunities.
   - Prioritize critical business workflows.

3. Estimate Testing Effort
   - Break down effort for test design, test data preparation,
     execution, automation, defect retesting, and reporting.
   - Provide estimated effort in hours or person-days.
   - Include assumptions and reasonable contingency.

4. Evaluate QA Capacity
   - Calculate available QA effort using team size,
     allocation, working days, and known commitments.
   - Compare estimated effort with available capacity.
   - Highlight resource shortages or scheduling conflicts.

5. Prepare Testing Schedule
   - Define testing activities, milestones, and dependencies.
   - Include functional testing, regression, defect retesting,
     and release readiness activities.

6. Define Entry and Exit Criteria
   - Specify conditions required to begin testing.
   - Define measurable conditions for testing completion,
     including coverage, execution status, and defect severity.

7. Identify Risks and Dependencies
   - Highlight risks related to requirements, environment,
     resources, integrations, and timelines.
   - Recommend practical mitigation actions.

8. Assess Feasibility
   - Determine whether the planned testing activities
     can fit within the available timeline and capacity.
   - Recommend adjustments if the plan is not feasible.

Rules:
- Base recommendations on provided inputs and available evidence.
- Do not invent requirements, dates, or team availability.
- Clearly label assumptions and estimated values.
- Use realistic effort calculations and avoid double-counting.
- Include only testing activities relevant to the release.
- Mark missing information as "Not provided".
- Present the final report using clear headings and tables.
```

## Expected output

Generate a structured **Test Plan and Estimation Report** containing:

1. **Release Overview:** Summary of the release, key features, and testing objectives.
   - *Example:* Release R2.5 covers login enhancements and order reporting changes.

2. **Testing Scope:** Features and functionalities included and excluded from testing.
   - *Example:* In Scope — Login, Reporting; Out of Scope — Mobile Application.

3. **Testing Strategy:** Applicable testing types, priorities, and manual/automation approach.
   - *Example:* Functional and API testing for new changes; automated regression for existing workflows.

4. **Effort Estimation:** Activity-wise estimated testing effort with assumptions and contingency.
   - *Example:* Test Design — 8 hours; Functional Testing — 20 hours; Regression — 12 hours.

5. **Resource Allocation:** Available QA capacity and recommended distribution of testing responsibilities.
   - *Example:* QA1 — Functional/API Testing; QA2 — Automation/Regression Testing.

6. **Testing Schedule:** Planned activities, milestones, dependencies, and expected completion windows.
   - *Example:* Week 1 — Functional Testing; Week 2 — Regression, Retesting, and Closure.

7. **Entry and Exit Criteria:** Conditions for starting and completing the agreed testing scope.
   - *Example:* Entry — QA build deployed; Exit — Critical scenarios executed and no unresolved release-blocking defects unless formally accepted.

8. **Risks and Dependencies:** Potential testing blockers, their impact, and mitigation recommendations.
   - *Example:* Risk — Delayed QA environment; Mitigation — Confirm environment readiness before execution.

9. **Feasibility Assessment:** Comparison of estimated effort, available capacity, and release timeline.
   - *Example:* Estimated Effort — 80 hours; Available Capacity — 120 hours; Status — Provisionally Feasible, subject to dependencies.

## Example

**Synthetic input:**

```text
RELEASE_SCOPE:
Login enhancements and order reporting changes.

TEAM_CAPACITY:
2 QA engineers, 8 hours/day, 100% allocation.

TIMELINE:
2 weeks (10 working days).
```

**Illustrative response (synthetic, not executed):**

### Testing Scope and Approach

| Feature | Testing Type | Priority |
|---|---|---|
| Login Enhancement | Functional, Negative, Regression | P1 |
| Order Reporting | Functional, API, Regression | P2 |

### Effort Estimation

| Activity | Estimated Effort |
|---|---:|
| Requirement Analysis | 8 hours |
| Test Case Design | 12 hours |
| Functional/API Testing | 24 hours |
| Regression Testing | 16 hours |
| Defect Retesting | 12 hours |
| Reporting and Closure | 4 hours |
| **Total** | **76 hours** |

*All estimates are illustrative assumptions.*

### Resource Capacity

```text
Gross QA Capacity:
2 QAs × 10 days × 8 hours = 160 hours

Assumed Meetings/Admin Overhead:
20% = 32 hours

Net Available Capacity:
160 - 32 = 128 hours

Estimated Testing Effort:
76 hours

Capacity Surplus:
128 - 76 = 52 hours
```

### Testing Schedule

| Activity | Timeline |
|---|---|
| Requirement Analysis and Test Design | Days 1–3 |
| Functional/API Testing | Days 4–7 |
| Regression Testing | Days 8–9 |
| Defect Retesting and Closure | Day 10 |

### Feasibility Assessment

**Status: Provisionally Feasible**

Estimated testing effort fits within the assumed available QA capacity. Final feasibility depends on build readiness, environment availability, and actual test complexity.

## Limitations

- Effort estimates are planning assumptions, not delivery guarantees.
- Accuracy depends on requirement clarity, team availability, and historical testing data.
- Environment readiness, automation coverage, and external dependencies require confirmation.
- Final estimates and release commitments require review by the QA Lead or relevant stakeholders.

Shared privacy, evidence, authorization, and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version

- **Owner:** QE Prompt Library maintainers (assign named owner before publication)
- **Version:** 1.2.0
- **Status:** Draft for team review
