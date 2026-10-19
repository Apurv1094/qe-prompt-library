#### P-02: Create or Update Driver / Browser Factory

```text
Review the existing browser/driver factory and test lifecycle.

Task:
{{DRIVER_OR_BROWSER_NEED}}

Inspect the current framework to identify supported browsers, execution modes,
driver setup, configuration, and test runner integration.

Implement the requested change by extending the existing factory and
lifecycle management. Preserve current capabilities, support headless or
remote execution where required, and ensure browser resources are released
safely even when a test fails.

Avoid creating a duplicate factory or changing unrelated tests.

Provide the complete code, required configuration changes, run instructions,
and validation results.