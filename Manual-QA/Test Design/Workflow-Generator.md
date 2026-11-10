# Workflow Generator

## Purpose

Analyze existing test cases and combine related validations into practical, reusable testing workflows. A workflow is a logical sequence of test cases that can be checked during one continuous user journey, reducing repeated setup and actions while preserving individual test case coverage.

---

## Required Input

### TEST_CASES

```text
{{TEST_CASES}}
```

Provide test case IDs, descriptions, steps or actions, expected results, and prerequisites where available. This is the **only required input**.

---

## Reusable Prompt

Act as a Senior QA Engineer optimizing manual and automated test execution.

Using only the supplied `TEST_CASES`, identify related cases and generate efficient testing workflows. Infer the logical execution sequence from the test case descriptions, steps, expected results, and prerequisites. Combine validations when the same setup, application state, or user journey can be reused safely.

### Rules

1. Group test cases based on shared prerequisites, reusable actions, compatible application state, or a natural sequence of user activities.
2. Arrange actions in a logical order and avoid repeating setup (such as login) where it can be reused safely.
3. Do not group cases with conflicting user roles, test data, prerequisites, or state changes merely to reduce the number of workflows.
4. Preserve every test case ID and its own expected result; do not remove, change, or silently merge away test coverage.
5. Where one action enables multiple checks, list each distinct validation and its related test case ID.
6. Separate or reset workflows when logout, destructive operations, role changes, or other state changes make continued execution unreliable.
7. Do not invent missing steps, expected results, data, or application behavior. Mark uncertainties as `Needs clarification`.
8. Keep workflows concise and suitable for manual execution or conversion into automation.
9. Keep cases that cannot safely be combined as standalone workflows.
10. Treat generated workflows as proposed execution plans, not evidence that tests were executed or passed.

---

## Expected Output

### 1. Workflow Summary

| Workflow ID | Workflow Name | Test Case IDs | Reason for Grouping |
|---|---|---|---|
| WF-01 | ... | ... | ... |

### 2. Detailed Workflows

For each workflow, provide:

**Workflow ID:** WF-01  
**Workflow Name:** ...  
**Covered Test Cases:** ...  
**Preconditions:** ...

| Step | Action / Validation | Related Test Case ID(s) | Expected Result |
|---|---|---|---|
| 1 | ... | ... | ... |

**Reset / Cleanup (if required):** ...  
**Notes / Clarifications:** ...

### 3. Test Case Coverage Mapping

| Test Case ID | Assigned Workflow ID | Status / Notes |
|---|---|---|
| TC-01 | WF-01 | Covered |

Include every supplied test case. Use `Needs clarification` where a case cannot be placed reliably.

### 4. Execution Optimization

Briefly identify repeated setup or actions avoided by the proposed grouping. Do not claim measured time savings without execution evidence.

---

## Example Input

### TEST_CASES

```text
TC-01: Log in with valid credentials; expected: login succeeds and dashboard opens.
TC-02: Verify dashboard title; expected: "ShopEasy Dashboard".
TC-03: Verify application logo; expected: ShopEasy logo is visible.
TC-04: Verify navigation menu; expected: Products, Cart, and Profile links are visible.
TC-05: Verify welcome section; expected: welcome message is displayed.
TC-06: Open Products; expected: product listing opens.
TC-07: Verify product names and prices; expected: each listed product shows a name and price.
TC-08: Add an available product to cart; expected: cart count increases by one.
```

## Example Workflow Summary

| Workflow ID | Workflow Name | Test Case IDs | Reason for Grouping |
|---|---|---|---|
| WF-01 | Login and Dashboard Checks | TC-01, TC-02, TC-03, TC-04, TC-05 | Log in once and perform all dashboard validations together |
| WF-02 | Product Listing and Cart Update | TC-06, TC-07, TC-08 | Reuse the product listing state for sequential checks and cart action |

**Note:** WF-02 assumes an authenticated session is available; otherwise authentication is a prerequisite. Verify product availability and cart state before the add-to-cart action. These assumptions require confirmation if not supplied in the test cases.
