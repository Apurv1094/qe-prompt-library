# Accessibility Test

## Purpose
Design accessibility checks for web or mobile UI.

## When to use
Use this prompt when evaluating a web application's accessibility to identify issues related to WCAG compliance, keyboard navigation, screen reader compatibility, color contrast, and accessible UI components.

## Inputs required
- `{{UI_SCOPE}}` — **Required:** Pages, screens, components, and user journeys to assess, including relevant platform or browser.
- `{{ACCESSIBILITY_STANDARD}}` — **Required:** Target WCAG version and conformance level or another applicable accessibility standard.
- `{{APP_URL}}` — **Required:** Accessible application URL and environment, if authorized for live inspection.

## Prompt
```text
Act as a Senior Accessibility Test Engineer.
Task: Generate keyboard, focus, semantic, screen-reader, contrast and form-error checks with manual and automated evidence; identify tool limitations.

Inputs:
UI_SCOPE:
{{UI_SCOPE}}
ACCESSIBILITY_STANDARD:
{{ACCESSIBILITY_STANDARD}}

APP_URL:
{{APP_URL}}

Rules:
- Evaluate supplied UI against applicable WCAG criteria.
- cover keyboard navigation, focus, semantics, labels and contrast.
- separate automated from manual checks.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected Output

Provide an Accessibility Checks Matrix containing the following columns:

- **ID:** Unique accessibility check identifier.
- **UI Element or Journey:** Component or user journey being evaluated.
- **WCAG Criterion:** Applicable WCAG success criterion.
- **Testing Method:** Manual, Automated, or Both.
- **Test Steps:** Actions required to validate accessibility.
- **Expected Accessible Behavior:** Expected behavior according to the applicable WCAG criterion.
- **Evidence Status:** Verified, Failed, Pending, or Not provided.
- **Priority:** High, Medium, or Low.

Clearly separate verified observations from recommendations. Mark missing evidence as `Not provided` and do not claim that checks were executed unless execution evidence is available.

### Example

**Synthetic input:**

```text
UI_SCOPE: Registration form with email, password, and Submit button.
ACCESSIBILITY_STANDARD: WCAG 2.2 AA.
```

**Illustrative output (not executed):**

| ID | UI Element or Journey | WCAG Criterion | Testing Method | Test Steps | Expected Accessible Behavior | Evidence Status | Priority |
|---|---|---|---|---|---|---|---|
| A11Y-01 | Registration form | 2.1.1 Keyboard | Manual | Navigate through all fields and Submit using Tab, Shift+Tab, and Enter | All interactive controls must be keyboard operable | Not provided | High |
| A11Y-02 | Email field | 3.3.2 Labels or Instructions | Both | Inspect accessible name and verify visible label association | Email input must have an appropriate label | Not provided | High |
| A11Y-03 | Submit button | 4.1.2 Name, Role, Value | Automated + Manual | Inspect button's accessible name and role | Submit button must expose an appropriate accessible name and role | Not provided | High |

**Observed Findings:** None. No accessibility testing was executed.

**Recommendations:** Execute the identified checks and record actual findings with supporting evidence.

*The example demonstrates the expected output structure, not verified application behavior or executed accessibility tests.*

## Limitations
- Automated scanners cannot establish full accessibility compliance.
- assistive-technology and human checks remain necessary.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
