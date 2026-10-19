#### Create or Update a CI/CD Pipeline

```text
Review the existing CI/CD pipeline and automation framework's run commands.

Task:
{{PIPELINE_REQUIREMENT}}

Identify the current pipeline platform, build process, test commands,
environment configuration, reporting, and artifact handling.

Extend the existing pipeline to meet the requirement. Include relevant steps
such as dependency caching, build/lint, smoke and regression execution,
browser/environment/tag parameters, report publishing, failure evidence,
scheduling, and notifications where needed.

Use the project's existing secret-management approach. Define clear failure
conditions and preserve unrelated pipeline behavior.

Provide the complete pipeline changes, explain how to trigger the workflow,
and report validation results. Do not claim the pipeline executed unless
it actually ran.
```