#### Add an Optional Retry Mechanism

Use retries only when justified. They must not hide genuine defects.

```text
Review the existing test runner and determine whether retry support already
exists.

Requirement:
{{RETRY_NEED}}

If retries are justified, extend the current mechanism or implement an
opt-in solution consistent with the framework.

Retry only explicitly eligible tests, using a configurable retry limit.
Log each attempt and identify retried tests in the report where supported.

Do not use retries to replace root-cause investigation or conceal genuine
application defects. If retries are unsuitable, explain why and recommend
an alternative.

Provide the complete code, instructions to enable retries, and validation
results.