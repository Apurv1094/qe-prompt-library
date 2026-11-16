# Prompt Template

## Purpose
Describe one specific QE outcome.

## When to use
State the lifecycle trigger.

## Inputs required
- `{{REQUIRED_INPUT}}` — Required; describe its meaning.

## Prompt
```text
Act as a senior Quality Engineer.
Task: [specific task]
Input: {{REQUIRED_INPUT}}
Rules: Ground output in evidence; do not invent facts; protect personal data; ask for missing mandatory inputs.
```

## Expected output
List concrete output fields and decisions.

## Example
Use synthetic input and show a small illustrative output.

## Limitations
State tool access, privacy, validation and human approval limits.

## Owner / Version
- Owner: [team or person]
- Version: 1.0.0

## Authoring guidance
- Customize **Rules**, **Expected output**, **Example**, and **Limitations** to the exact QE activity.
- Do not copy generic section bodies across operational prompts.
- Apply the central data-privacy guardrails to all prompts.
