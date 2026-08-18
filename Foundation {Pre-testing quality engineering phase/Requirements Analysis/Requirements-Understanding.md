# Requirement Understanding Prompt

## Purpose

Use this prompt to build a clear and structured understanding of a requirement before requirement gap analysis, risk assessment, test design, or test case creation begins.

The QA provides four inputs:

1. App Overview
2. Epic Description
3. Story Description
4. Acceptance Criteria

The output explains **what the requirement means in simple language**. It must not create test cases or perform detailed requirement gap analysis.

---

## Input

```text
APP_OVERVIEW:
"""
{APP_OVERVIEW}
"""

EPIC_DESCRIPTION:
"""
{EPIC_DESCRIPTION}
"""

STORY_DESCRIPTION:
"""
{STORY_DESCRIPTION}
"""

ACCEPTANCE_CRITERIA:
"""
{ACCEPTANCE_CRITERIA}
"""
```

---

## Prompt

```text
You are a senior QA engineer responsible for understanding a requirement before test design begins.

Using the App Overview, Epic Description, Story Description, and Acceptance Criteria provided below, build a clear and structured understanding of the requirement.

Your goal is to explain the requirement in simple language so that a QA, developer, BA, or Product Owner can understand what the feature is expected to do.

Do not create test cases, test scenarios, test data, automation recommendations, or detailed testing strategies.

APP OVERVIEW:
"""
{APP_OVERVIEW}
"""

EPIC DESCRIPTION:
"""
{EPIC_DESCRIPTION}
"""

STORY DESCRIPTION:
"""
{STORY_DESCRIPTION}
"""

ACCEPTANCE CRITERIA:
"""
{ACCEPTANCE_CRITERIA}
"""

Analyze the information together and provide:

1. Requirement Summary
   - Explain what this story is intended to achieve in simple language.
   - Keep the explanation concise and avoid copying the original wording.

2. Actor & Goal
   - Identify who is performing or benefiting from the functionality.
   - Explain what they want to achieve.

3. Core Flow
   - Describe the expected business flow step by step.
   - Include the starting point, key actions/conditions, and expected outcome.
   - Use only behavior supported by the provided requirement.

4. Business Rules
   - Extract explicit business rules, conditions, validations, limits, or constraints stated in the Epic, Story, or Acceptance Criteria.
   - Do not invent rules that are not supported by the input.

5. Systems / Components Involved
   - Identify applications, modules, APIs, services, databases, integrations, or external systems explicitly mentioned or clearly required by the requirement.
   - If a component is inferred rather than explicitly stated, mark it as an assumption.

6. Assumptions
   - List only assumptions required to understand the requirement.
   - Clearly distinguish assumptions from facts stated in the requirement.

7. Open Questions
   - Identify information that is unclear or cannot be confidently understood from the provided inputs.
   - Phrase each item as a question that can be taken to the BA/Product Owner.
   - Do not turn this section into a full requirement gap analysis.

Output using exactly this structure:

# Requirement Understanding

## Requirement Summary

## Actor & Goal

## Core Flow

## Business Rules

## Systems / Components Involved

## Assumptions

## Open Questions
```

---

## Expected Output

The output should provide a **simple, structured understanding of the story** that can be used as the foundation for the next QA activities.

It should answer:

- What is the feature supposed to do?
- Who is involved?
- What is the expected business flow?
- What rules are explicitly defined?
- Which systems/components are involved?
- What assumptions were made?
- What needs clarification before proceeding?

---

## Scope Boundaries

### This prompt SHOULD:

- Simplify and restate the requirement.
- Connect the Epic context with the Story and Acceptance Criteria.
- Extract explicit business rules.
- Explain the expected flow.
- Identify actors and systems.
- Surface assumptions.
- Identify questions that prevent confident understanding.

### This prompt SHOULD NOT:

- Create test cases.
- Create test scenarios.
- Generate test data.
- Perform detailed requirement gap analysis.
- Perform risk assessment.
- Decide manual vs automation.
- Define test scope.
- Define testing approach.
- Recommend automation candidates.
- Identify regression scenarios.
- Write defects.

Those activities belong to separate QE prompts.

---

## Standard Input Contract

| Input | Purpose |
|---|---|
| `APP_OVERVIEW` | Provides the high-level context of the application/product |
| `EPIC_DESCRIPTION` | Provides the broader business objective and feature context |
| `STORY_DESCRIPTION` | Defines the specific requirement being understood |
| `ACCEPTANCE_CRITERIA` | Defines the conditions that must be satisfied by the story |

### Important

The requirement should be provided **once using these four standard inputs**. Do not create separate input placeholders for different requirement formats unless a separate prompt specifically requires them.
