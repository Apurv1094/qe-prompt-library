#### Add an Optional Retry Mechanism

Use retries only when justified. They must not hide genuine defects.

```text
Review the existing test runner and determine whether retry support already
exists.

Requirement:
{{RETRY_NEED}}

Placeholder: {{RETRY_NEED}}

Describe whether retries are required and, if so, specify which tests or failure conditions are eligible for retry, the maximum retry attempts, and any reporting expectations.

Examples:

Retry failed tests up to 2 times.

Retry only transient failures; do not retry assertion failures.

Do not implement retries; focus on root-cause analysis.

If the requirement does not specify these details, inspect the existing framework and recommend suitable defaults or ask for clarification when necessary. Do not assume that every failure should be retried.

If retries are justified, extend the current mechanism or implement an
opt-in solution consistent with the framework.

Retry only explicitly eligible tests, using a configurable retry limit.
Log each attempt and identify retried tests in the report where supported.

Do not use retries to replace root-cause investigation or conceal genuine
application defects. If retries are unsuitable, explain why and recommend
an alternative.

Provide the complete code, instructions to enable retries, and validation
results.