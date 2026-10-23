#### Set Up Parallel and Cross-Browser Execution

```text
Review the existing test execution configuration and parallel-safety.

Task:
{{EXECUTION_REQUIREMENT}}

Inspect the existing automation framework to identify:
- Automation tool, programming language, and test runner
- Supported browsers and execution environments
- Existing parallel execution capabilities and configuration
- Browser, driver, session, and resource lifecycle management
- Shared state, test data, and test isolation mechanisms
- Existing local, remote, Grid, container, or cloud execution setup
- Current CI/CD integration and execution conventions

Extend the existing configuration to support the requested execution
modes while following organisational standards and project conventions.

Implementation rules:
- Use the execution capabilities supported by the existing framework.
- Reuse existing configuration, utilities, and lifecycle management.
- Ensure independent browser sessions and appropriate test isolation.
- Identify shared mutable state, resource conflicts, and dependencies
  that could cause failures during parallel execution.
- Assess test parallel-safety before enabling parallel execution broadly.
- Support the requested browsers and execution environments.
- Avoid unnecessary dependencies, duplicated functionality, and
  incompatible configuration changes.
- Preserve existing behaviour and CI/CD compatibility wherever feasible.
- Do not assume that increasing the worker or thread count alone
  is sufficient for safe parallel execution.

Provide:
- Complete code and configuration changes
- Execution commands for the requested modes
- Required environment or infrastructure setup
- Troubleshooting guidance for common execution failures
- Actual validation results and any outstanding limitations

Do not claim that execution or validation succeeded unless it was
actually performed.
```

**Placeholder guidance for the user:**

`{{EXECUTION_REQUIREMENT}}` — Describe the required parallel and cross-browser execution behaviour, including the browsers to support, desired concurrency, execution environment (local, remote, container, or cloud), test-isolation requirements, and CI/CD needs. Specify only the requirements relevant to your project; the prompt will inspect the existing framework to determine the appropriate implementation.

**Example placeholder input (comma-separated):**

Enable parallel execution, support Chrome Firefox and Edge, configure 4 concurrent workers or threads as supported by the framework, support local and remote execution, use existing Grid or cloud infrastructure where available, isolate browser sessions and test data, maintain CI/CD compatibility.

