# Test Scenario Generator

## Purpose
Identify distinct, high-value testing scenarios before writing detailed cases.

## When to use
During test design when stories and acceptance criteria are available but detailed steps are not yet needed.

## Inputs required
- `{{STORY_DESCRIPTION}}` — **Required:** Feature objective, actors, and business flow.
- `{{ACCEPTANCE_CRITERIA}}` — **Required:** Numbered, observable acceptance conditions and validation rules.

## Prompt
```text
Act as a Senior Quality Analyst working with a delivery team.
Task: Identify distinct, high-value testing scenarios before writing detailed cases.

Inputs:
STORY_DESCRIPTION:
{{STORY_DESCRIPTION}}
ACCEPTANCE_CRITERIA:
{{ACCEPTANCE_CRITERIA}}

Instructions:
- Create concise, distinct scenarios with IDs, title, category, priority, AC mapping, and risk rationale.
- Include positive, negative, boundary, and workflow variations only if justified by provided criteria.
- Do not turn scenarios into step-by-step manual test cases.
- Identify uncovered criteria and assumptions; do not invent system behavior.

Output format:
1. **Scenario catalog:** Scenario ID, title, test category, priority, AC ID, brief condition/expected behavior, rationale.
2. **Coverage summary:** AC IDs covered and gaps.
3. **Open questions:** requirements needing clarification before detailed test cases.
```

## Expected output
1. **Scenario catalog:** Scenario ID, title, test category, priority, AC ID, brief condition/expected behavior, rationale.
2. **Coverage summary:** AC IDs covered and gaps.
3. **Open questions:** requirements needing clarification before detailed test cases.

## Example
**Synthetic input:**
```text
STORY_DESCRIPTION: Teachers can create assignments for a course.
ACCEPTANCE_CRITERIA:
AC-01: Due date is mandatory; saving without a due date is rejected.
```

**Illustrative output (not executed):**
| Scenario ID | Title | Category | Priority | AC | Expected behavior |
|---|---|---|---|---|---|
| SC-01 | Save assignment without due date | Negative | High | AC-01 | Save is rejected |
| SC-02 | Save assignment with a due date | Positive | Medium | AC-01 | Clarification needed: success behavior not explicitly defined |

**Coverage:** AC-01 negative validation covered. **Question:** What should happen after a valid assignment is saved?

## Limitations
- Generated artifacts are design recommendations, not proof of execution or verified application behavior.
- Do not invent requirements, business rules, observed results, or credentials. Flag gaps for human review.
- Follow `00-Library-Guide/Guardrails-Data-Privacy.md` for privacy, evidence, authorization, and review requirements.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.1.0
- Status: Draft for team review
