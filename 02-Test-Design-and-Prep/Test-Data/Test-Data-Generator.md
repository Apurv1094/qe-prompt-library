# Test Data Generator

## Purpose
Produce safe, reusable synthetic data for planned test scenarios.

## When to use
When test scenarios and field constraints are known and test execution data is needed.

## Inputs required
- `{{TEST_SCENARIOS}}` — **Required:** Scenario IDs and conditions that need representative test records.
- `{{DATA_RULES}}` — **Required:** Field types, lengths, formats, allowed values, uniqueness, and cross-field constraints.

## Prompt
```text
Act as a Senior Test Data Engineer working with a delivery team.
Task: Produce safe, reusable synthetic data for planned test scenarios.

Inputs:
TEST_SCENARIOS:
{{TEST_SCENARIOS}}
DATA_RULES:
{{DATA_RULES}}

Instructions:
- Generate only fictional values; never use actual personal records, secrets, or production extracts.
- Cover valid, invalid, boundary, and edge values supported by the supplied rules.
- Link each dataset to a scenario and expected validation result.
- Include reusable fixture examples and deterministic generation guidance when applicable.
- If a rule is missing, label the corresponding expected outcome Unknown rather than inventing it.

Output format:
1. **Test data matrix:** Data ID, linked scenario, input fields/values, category, expected validity, rationale.
2. **Reusable fixture:** copy-ready JSON or CSV with synthetic values.
3. **Rule gaps:** constraints that need clarification before further data is generated.
```

## Expected output
1. **Test data matrix:** Data ID, linked scenario, input fields/values, category, expected validity, rationale.
2. **Reusable fixture:** copy-ready JSON or CSV with synthetic values.
3. **Rule gaps:** constraints that need clarification before further data is generated.

## Example
**Synthetic input:**
```text
TEST_SCENARIOS: SC-01 Accept valid student ID; SC-02 Reject malformed student ID.
DATA_RULES: Student ID must contain exactly eight numeric digits.
```

**Illustrative output (not executed):**
| Data ID | Scenario | Student ID | Category | Expected |
|---|---|---|---|---|
| TD-01 | SC-01 | 12345678 | Valid | Accepted |
| TD-02 | SC-02 | 1234567 | Boundary: 7 digits | Rejected |
| TD-03 | SC-02 | 123456789 | Boundary: 9 digits | Rejected |
| TD-04 | SC-02 | ABCD1234 | Invalid characters | Rejected |

Fixture (synthetic): `[{"id":"TD-01","studentId":"12345678"},{"id":"TD-02","studentId":"1234567"}]`. No actual student records are used.

## Limitations
- Generated artifacts are design recommendations, not proof of execution or verified application behavior.
- Do not invent requirements, business rules, observed results, or credentials. Flag gaps for human review.
- Follow `00-Library-Guide/Guardrails-Data-Privacy.md` for privacy, evidence, authorization, and review requirements.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.1.0
- Status: Draft for team review
