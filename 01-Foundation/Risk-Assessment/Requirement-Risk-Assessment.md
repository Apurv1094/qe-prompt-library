# Requirement Risk Assessment

## Purpose
Identify and prioritize risks in a user story so QA can focus testing on the most important behaviors and dependencies.

## When to use
Use during requirement review or sprint planning, before test design, when a new or changed story needs risk-based testing priorities.

## Inputs required
- `{{STORY_DESCRIPTION}}` — **Required:** Describe the user goal and feature being introduced or changed. **Example:** Staff can update a student's grade.
- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Provide numbered, testable rules for the story. **Example:** AC-01: Authorized staff can update grades; AC-02: Every update is audited.
- {{CHANGE_IMPACT}} — Optional: List the features or areas affected by the change. Example: Grade entry page, student reports.

- {{DEPENDENCIES}} — Optional: List other systems or services required for the feature to work. Example: Authentication service, database.
- `{{KNOWN_DEFECTS}}` — **Optional:** Provide related defect IDs and symptoms. **Example:** BUG-104: Audit entry missing after edit; use `None known` only if confirmed, otherwise `Not provided`.

## Prompt
```text
Role: Act as a Senior Quality Assurance Engineer specializing in requirement analysis and risk-based testing.

Task: Review the story and acceptance criteria, identify realistic product and delivery risks, and recommend where QA should focus testing. Do not generate detailed test cases.

Inputs:
STORY_DESCRIPTION:
{{STORY_DESCRIPTION}}
ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}
CHANGE_IMPACT:
{{CHANGE_IMPACT}}
DEPENDENCIES:
{{DEPENDENCIES}}
KNOWN_DEFECTS:
{{KNOWN_DEFECTS}}

Instructions:
1. Summarize the feature, its business-critical workflows, and any unclear or untestable requirements.
2. Identify risks involving functional correctness, authorization, data integrity, integrations, regression, and relevant non-functional concerns.
3. Map each risk to an AC ID or label it as an inferred risk needing confirmation.
4. Score Impact and Likelihood from 1 (Low) to 3 (High); calculate Risk Score = Impact × Likelihood. Explain each score using available evidence; where likelihood is unknown, state the assumption.
5. Assign testing priority: P1 for scores 7–9, P2 for 4–6, P3 for 1–3. Flag any security or regulatory criticality that merits escalation irrespective of score.
6. Recommend high-level testing focus, risk mitigation, and the relevant owner or role where known.
7. Identify missing information and decisions needed before test design.

Rules:
- Do not invent requirements, dependencies, defects, or historical failure rates.
- Distinguish confirmed facts, assumptions, and questions.
- Do not claim a risk has been eliminated without evidence.
- Keep the output concise, actionable, and traceable to the story.
```

## Expected output
1. **Feature Summary:** What is changing and why. **Example:** Staff can edit grades with an audit trail.
2. **Risk Register:** Risks with AC mapping, impact, likelihood, score, priority, and rationale. **Example:** Unauthorized grade edits — AC-01 — 3 × 2 = 6 — P2.
3. **Recommended Testing Focus:** High-level checks for each major risk. **Example:** Validate authorized and unauthorized grade updates.
4. **Mitigations and Dependencies:** Actions or prerequisites that reduce testing or product risk. **Example:** Confirm audit storage availability.
5. **Clarifications Needed:** Unspecified behavior requiring stakeholder input. **Example:** Who may edit grades after final approval?

## Example
**Synthetic input:**
```text
STORY_DESCRIPTION: Authorized staff can update student grades.
ACCEPTANCE_CRITERIA: AC-01: Authorized staff can update grades. AC-02: Each change is audited.
CHANGE_IMPACT: Grade-entry UI and grade API.
DEPENDENCIES: Role-based access service; audit database.
KNOWN_DEFECTS: Not provided.
```

**Illustrative output (not executed):**

| Risk / AC | Impact | Likelihood | Score / Priority | Testing focus |
|---|---:|---:|---|---|
| Unauthorized grade edit / AC-01 | 3 | 2* | 6 / P2 | Verify role restrictions across UI and API |
| Missing audit record / AC-02 | 3 | 2* | 6 / P2 | Verify audit record after successful changes |

*Likelihood is assumed for illustration, not derived from defect history. Confirm risk ranking with the team. Clarify whether an audit failure must prevent a grade update.*

## Limitations
- Risk scoring is a prioritization aid, not a measured probability of failure.
- Missing technical details and defect history can change the assessment.
- QA and relevant stakeholders must validate risk priorities and mitigations.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
