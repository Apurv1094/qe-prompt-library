# Regression Test Selection

## Purpose
Select impact-based regression coverage.

## When to use
Use this prompt when application code, features, configurations, or integrations change and the QA team needs to identify and prioritize relevant regression tests based on change impact, business criticality, and existing test coverage.

## Inputs required
- `{{CHANGE_SUMMARY}}` — **Required:** Provide the relevant change summary details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{TEST_INVENTORY}}` — **Required:** Available test cases with IDs, mapped features, criticality, and execution cost.
- `{{DEPENDENCY_MAP}}` — **Required:** Provide the relevant dependency map details, including scope, identifiers, dates, and supporting evidence where applicable.

## Prompt
```text
Act as a Senior Quality Assurance Engineer.
Task: Rank tests by changed behavior, dependencies, criticality and historical failures; provide selected, deferred and mandatory smoke tests with rationale.

Inputs:
CHANGE_SUMMARY:
{{CHANGE_SUMMARY}}
TEST_INVENTORY:
{{TEST_INVENTORY}}
DEPENDENCY_MAP:
{{DEPENDENCY_MAP}}

Rules:
- Map changes to impacted components and requirements.
- combine risk, critical paths and historical defects.
- justify selected and excluded tests.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```

## Expected output
Risk-ranked regression shortlist with test IDs, mapped changes, risk rationale, exclusions, coverage gaps, and execution order.

- Clearly separate observed findings from recommendations, and mark missing evidence as `Not provided`.

## Example
**Synthetic input:**
```text
CHANGED_COMPONENTS: Checkout coupon validation changed.
TEST_INVENTORY: CART-01 apply valid coupon; CART-02 reject expired coupon; LOGIN-01 valid login.
```

**Illustrative output (not executed):**

CART-01 | Include | Directly changed validation | P1; CART-02 | Include | Negative boundary | P1

*The sample demonstrates output format, not verified application behavior or an executed test.*

## Limitations
- Impact analysis may miss hidden dependencies.
- selective testing does not eliminate residual regression risk.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
