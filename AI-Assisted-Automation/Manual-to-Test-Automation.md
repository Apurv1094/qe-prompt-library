#### Convert a Manual Test to Automation

```text
Convert the following manual test into an automated test using the existing
automation framework.

Manual test / scenario:
{{MANUAL_TEST_OR_SCENARIO}}

Expected result, if not already specified:
{{EXPECTED_RESULT_OR_NA}}

Relevant URLs(if not covered in the test case):
{{URLS}}

Instructions:
1. Inspect the existing test structure, page objects, setup/cleanup hooks,
   test-data handling, and naming conventions.
2. Reuse existing components and identify any missing page actions.
3. Create a clearly named automated test with one primary objective.
4. Follow existing assertion, test-data, and reporting conventions.
5. If the framework uses BDD, follow its existing feature-file and
   step-definition patterns. Use Scenario Outline and tags where appropriate.
6. Identify missing requirements or expected results instead of inventing
   business rules.

Provide the complete code, changed file paths, and instructions to run the test.
```

