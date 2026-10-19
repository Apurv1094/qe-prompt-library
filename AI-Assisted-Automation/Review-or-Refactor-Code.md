#### Review and Refactor Code

```text
Act as a Senior QA Automation Engineer and review the following code or change
in the context of the existing framework.

File, class, test, or change:
{{CODE_LOCATION_OR_CHANGE}}

Inspect the relevant implementation and project conventions before
recommending changes.

Review applicable areas such as locator stability, waits, assertions,
duplication, hardcoded data, configuration, thread safety, error handling,
naming, maintainability, and security.

First provide a table with:
Issue | Severity (High/Medium/Low) | File/Location | Recommended Fix

Then provide a focused refactor where appropriate. Preserve existing
behavior unless a change is necessary, and explain any behavior changes.

Do not refactor unrelated files or introduce unnecessary abstractions.
Provide the complete changed code and validation results.