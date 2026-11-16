# Exploratory Test Charter

## Purpose
Plan a focused, time-boxed exploratory session based on feature risks.

## When to use
Before exploratory sessions, especially where scripted cases may miss interaction or usability issues.

## Inputs required
- `{{FEATURE_SCOPE}}` — **Required:** Feature, user journeys, environment, and boundaries to explore.
- `{{KNOWN_RISKS}}` — **Optional:** Suspected failure areas, recent changes, defects, and dependencies to prioritize.

## Prompt
```text
Act as a Senior Quality Analyst working with a delivery team.
Task: Plan a focused, time-boxed exploratory session based on feature risks.

Inputs:
FEATURE_SCOPE:
{{FEATURE_SCOPE}}
KNOWN_RISKS:
{{KNOWN_RISKS}}

Instructions:
- State a focused mission, in-scope and out-of-scope areas, and a suggested timebox.
- Give concrete test ideas, user perspectives, heuristics, and observable checkpoints.
- Provide a session notes template distinguishing observation, hypothesis, and verified defect.
- If risks are not provided, label proposed risks as hypotheses, not facts.

Output format:
1. **Charter:** mission, scope, risks, suggested timebox, setup needs.
2. **Exploration guide:** prioritized test ideas with observable checkpoints.
3. **Evidence and debrief:** notes fields, reproduction checklist, and review questions.
```

## Expected output
1. **Charter:** mission, scope, risks, suggested timebox, setup needs.
2. **Exploration guide:** prioritized test ideas with observable checkpoints.
3. **Evidence and debrief:** notes fields, reproduction checklist, and review questions.

## Example
**Synthetic input:**
```text
FEATURE_SCOPE: Course search page; search term, category filter, pagination.
KNOWN_RISKS: Filter state may be lost when moving between pages.
```

**Illustrative output (not executed):**
**Mission:** Explore whether course search results remain coherent when filters and pages change. **Timebox:** Suggested 30 minutes.

| Priority | Test idea | Observation checkpoint |
|---|---|---|
| High | Apply category filter, then move to page 2 | Filter selection and result relevance |
| High | Change filter while on a later page | Page state and results update coherently |
| Medium | Search for a term with no matches | Empty-state messaging |

**Session note template:** action, observed result, expected basis, screenshot/log reference, hypothesis, reproduction status. **Debrief:** Which state transitions were surprising? What needs a reproducible scripted test?

## Limitations
- Generated artifacts are design recommendations, not proof of execution or verified application behavior.
- Do not invent requirements, business rules, observed results, or credentials. Flag gaps for human review.
- Follow `00-Library-Guide/Guardrails-Data-Privacy.md` for privacy, evidence, authorization, and review requirements.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.1.0
- Status: Draft for team review
