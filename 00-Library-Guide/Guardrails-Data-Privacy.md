
# Guardrails - Data Privacy

## Purpose
Ensure safe and responsible use of AI tools by protecting sensitive and confidential information across all QE activities.

## When to use
Before sharing requirements, test data, logs, screenshots, code or other project information with AI tools.

## Inputs required
- Data or information to be shared
- Organization-approved AI tool and applicable data policy

## Prompt
Review the provided information for sensitive data, credentials, personal information and confidential content. Identify potential privacy risks and recommend safe alternatives. Do not expose or reproduce sensitive values.

## Rules
- Use synthetic or properly sanitized test data.
- Never share passwords, API keys, tokens or unauthorized confidential information.
- Follow organizational security and data privacy policies.
- Validate AI-generated outputs before using them.
- Report suspected data exposure through approved channels.

## Expected output
- Data safety assessment
- Identified risks and recommended precautions
- Required approvals, if applicable

## Example
Unsafe: Real customer details, passwords or production records.

Safe: Fictional customer information, dummy credentials and synthetic test data.

## Limitations
- AI cannot guarantee data privacy or regulatory compliance.
- Sensitive information must be sanitized before submitting it to an AI tool.
- Applicable regulations depend on the project and organization.

## Owner / Version
- Owner: QE / Security Team
- Version: 1.0
