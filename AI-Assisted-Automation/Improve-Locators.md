### Improve Locators

```text
Review locator stability in the existing automation framework.

Page, test, or area to review:
{{PAGE_OR_TEST_OR_NA}}

Inspect the existing page objects and use available browser tools to examine
the current DOM and relevant elements.

Identify fragile locators and replace them with stable alternatives grounded
in the actual page structure. Follow project conventions and prefer stable
test attributes, IDs, accessible roles/names, CSS, and XPath as a last resort.

Validate locator uniqueness where possible. Explain why each changed locator
is more reliable.

If no reliable locator can be identified, recommend the specific DOM or
test-attribute change needed from the development team.

Provide the complete changed code and validation results. Do not invent
elements or claim a locator was validated if it was not.
```
