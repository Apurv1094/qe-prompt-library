#### P-02: Create or Update Driver / Browser Factory

```text
Review the existing browser/driver factory and test lifecycle.

Task:
{{DRIVER_OR_BROWSER_NEED}}

The {{DRIVER_OR_BROWSER_NEED}} placeholder tells the AI what change is required in the existing driver or browser factory.

It allows the user to specify the desired driver-management behavior, such as adding browser support, changing driver initialization, enabling headless or remote execution, or improving thread safety and browser cleanup.

The AI uses this requirement to inspect the existing framework and implement the requested changes without creating a duplicate factory or modifying unrelated tests.

Inspect the current framework to identify supported browsers, execution modes,
driver setup, configuration, and test runner integration.

Implement the requested change by extending the existing factory and
lifecycle management. Preserve current capabilities, support headless or
remote execution where required, and ensure browser resources are released
safely even when a test fails.

Avoid creating a duplicate factory or changing unrelated tests.

Provide the complete code, required configuration changes, run instructions,
and validation results.