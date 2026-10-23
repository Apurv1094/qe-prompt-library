#### P-04: Create or Update a Page Object

```text
Create or update the Page Object for the "{{PAGE_NAME}}" page in the
existing automation framework.

Page details:
- URL: {{PAGE_URL_OR_NA}}
- Task / expected user behavior: {{TASK_OR_EXPECTED_BEHAVIOR}}

Note: If the {{PAGE_NAME}} already exists, then don't create the new {{PAGE_NAME}}

Instructions:
1. Inspect the existing framework and follow its page-object conventions.
2. Use available browser automation tools to inspect the page and identify
   relevant interactive elements, labels, inputs, buttons, and page structure.
3. Identify stable locators from the actual page. Prefer stable test attributes,
   IDs, accessible roles/names, CSS, and XPath as a last resort.
4. Create reusable methods representing user actions. Keep locators in the
   Page Object and assertions in tests, following project conventions.
5. Reuse existing utilities and avoid unnecessary getters, abstractions,
   dependencies, or duplicate methods.
6. If an action navigates to another page, return the next Page Object only
   after confirming navigation has completed, where appropriate.
7. Validate locator uniqueness and behavior where possible. Do not invent
   elements or claim validation was performed if it was not.
8. If browser inspection is unavailable, use available DOM/HTML or request
   the minimum information needed to identify the elements accurately.

Provide the complete code, expected file path, assumptions, and validation
results.