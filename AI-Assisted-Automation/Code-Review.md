---
description: Review code changes for correctness, quality, security, maintainability, and compliance with applicable project standards
argument-hint: [file-path, PR/MR-number, or change-reference]
---

# Code Review

## Objective

Review the specified code changes for correctness, security, maintainability, test coverage, and adherence to the project's existing conventions and applicable standards.

Provide actionable feedback based on the actual code and available project context. Do not invent issues, requirements, standards, or test results.

## Review Scope

If an argument is provided, determine the review scope as follows:

- **File path:** Review the specified file and inspect relevant dependencies or related files when necessary.
- **PR/MR number or change reference:** Review the corresponding pull request, merge request, or change set using the repository's available tools.
- **Other supported reference:** Resolve the reference using the available repository context and tools.

If no argument is provided:

- Review staged changes by default.
- If staged changes are unavailable or empty, report this and ask whether the user wants to review unstaged changes, a specific file, or a PR/MR.
- Do not silently expand the scope beyond the requested changes.

Before reviewing, inspect relevant project documentation, coding guidelines, contribution standards, security policies, and architecture conventions when available.

Use the project's existing language, framework, tooling, and conventions. Do not assume a particular programming language, repository host, build tool, or framework.

## Review Checklist

### 1. Correctness and Code Quality

- [ ] Code behaves as intended and satisfies the stated requirements.
- [ ] Logic is correct, including boundary conditions and error scenarios.
- [ ] Functions, classes, and modules have clear responsibilities.
- [ ] Naming is clear and consistent with project conventions.
- [ ] Error handling is appropriate and actionable.
- [ ] Types, data structures, and language features are used correctly.
- [ ] No unnecessary duplication, dead code, or avoidable complexity.
- [ ] No debugging statements or unintended temporary code.
- [ ] Resource cleanup and lifecycle management are handled appropriately.

### 2. Security and Data Protection

- [ ] No hardcoded credentials, secrets, tokens, or private keys.
- [ ] External inputs are validated and handled safely.
- [ ] Database queries and commands are protected against injection.
- [ ] Authentication and authorization are enforced where required.
- [ ] Sensitive information is not exposed through logs, errors, or responses.
- [ ] File access, network requests, and external integrations are handled securely.
- [ ] Dependencies and security-sensitive operations follow applicable project policies.

Apply only the checks relevant to the technologies and functionality being reviewed.

### 3. Testing and Reliability

- [ ] New or changed behavior has appropriate test coverage.
- [ ] Absolute Xpaths should not be allowed.
- [ ] Avoid Duplicate logic.
- [ ] Positive, negative, boundary, and relevant failure scenarios are considered.
- [ ] Existing tests remain compatible with the changes.
- [ ] Tests are readable, deterministic, and maintainable.
- [ ] Asynchronous operations, concurrency, retries, and timeouts are handled correctly where applicable.
- [ ] Tests avoid unnecessary dependencies on execution order, timing, or external state.
- [ ] Relevant validation commands or tests are run when tools and the environment permit.

Clearly distinguish tests that were executed from tests that are recommended but were not executed.

### 4. Architecture and Maintainability

- [ ] Changes follow established architectural patterns.
- [ ] Responsibilities are separated appropriately.
- [ ] Dependencies are introduced only when justified.
- [ ] No unintended circular dependencies or tight coupling.
- [ ] Public interfaces and contracts remain compatible, or breaking changes are documented.
- [ ] Performance and scalability implications are considered where relevant.
- [ ] Changes are appropriately scoped and avoid unrelated modifications.

### 5. Configuration and Behavioral Changes

- [ ] Configuration changes are consistent with existing conventions.
- [ ] Environment-specific values are handled appropriately.
- [ ] Behavior-changing modifications follow applicable rollout, compatibility, and rollback practices.
- [ ] Feature flags or equivalent controls are used when required by project or release standards.
- [ ] Where feature flags are required, defaults, naming, lifecycle, and flag-on/flag-off behavior follow the applicable standards.
- [ ] If a feature flag is not needed, the reason is documented when required by project policy.
- [ ] Database, API, schema, and configuration migrations are safe and appropriately documented.

Do not require feature flags for every behavioral change. Apply the project's actual release and rollout policies.

### 6. Documentation and Standards

- [ ] Comments explain non-obvious logic rather than restating the code.
- [ ] Public interfaces, configuration options, and significant behavior are documented where appropriate.
- [ ] Relevant setup instructions or project documentation are updated when needed.
- [ ] Changes comply with applicable coding, testing, security, and contribution standards.
- [ ] Existing conventions are preserved unless there is a justified reason to change them.

## Review Guidelines

1. Prioritize actionable defects over personal style preferences.
2. Report only issues supported by the code, repository context, or stated requirements.
3. For each issue, identify the affected file and line or code section whenever available.
4. Explain the problem, its impact, and a practical recommendation.
5. Assign severity based on impact and likelihood, using the project's severity definitions when available.
6. Avoid reporting the same underlying issue multiple times.
7. Do not suggest changes that unnecessarily duplicate existing functionality or conflict with established patterns.
8. Do not modify files, commit changes, or create pull-request comments unless explicitly requested.
9. If repository access, documentation, or execution tools are unavailable, state the limitation rather than claiming verification.
10. If no issues are identified, state that no actionable issues were found within the reviewed scope. Do not claim the code is completely defect-free.

## Review Output

### Must Fix (Blocking)

Issues that should prevent merging until resolved, such as:

- Security vulnerabilities or sensitive-data exposure.
- Confirmed functional defects or data corruption risks.
- Significant regressions or incompatible changes without an acceptable migration path.
- Violations of mandatory project or release requirements.
- Critical reliability issues.

For each finding, include:

- **Location:** File and line or code section.
- **Issue:** What is wrong.
- **Impact:** Why it matters.
- **Recommendation:** How to address it.

If there are no blocking issues, explicitly state that none were identified.

### Should Fix (Non-blocking)

Issues that should preferably be addressed, such as maintainability concerns, incomplete edge-case handling, or avoidable performance problems.

Include the location, rationale, and suggested improvement.

### Nice to Have

Optional improvements, such as readability enhancements, simplifications, or future refactoring opportunities.

### Positive Feedback

Highlight effective design decisions, clear implementation, useful tests, good error handling, or other practices worth retaining.

### Review Summary

Provide a concise summary containing:

- Overall assessment: Approve, Approve with Suggestions, or Changes Requested.
- Number of findings by severity.
- Areas reviewed.
- Tests or validation performed and their actual results.
- Any unverified areas or limitations.

Base the assessment on the findings and applicable project review policy. Do not imply that tests passed or that standards were verified unless evidence supports that conclusion.