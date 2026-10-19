#### P-09: Add or Update Reporting and Failure Evidence

```text
Review the existing reporting and failure-evidence implementation.

Task:
{{REPORTING_NEED}}

Inspect the current reporting tool, test listeners/hooks, logging, screenshot
capture, and supported video/trace capabilities.

Extend the existing setup to meet the requirement. Attach failure evidence
to reports where supported, follow existing naming conventions, and implement
retention or cleanup only when needed.

Avoid introducing a second reporting system unless there is a clear reason.

Provide the complete code, configuration changes, instructions to generate
and view reports, and validation results.