#### P-03: Create or Update Organisation-Wide Reusable Base Page

```text
Review the existing automation framework and its BasePage or equivalent
reusable interaction layer.

#### Task:
{{REUSABLE_ACTION_NEED}}

{{REUSABLE_ACTION_NEED}}: Describe the reusable action or enhancement required in the shared interaction layer. Specify the expected behaviour and any relevant constraints, if known. The AI should inspect the existing framework to determine the appropriate implementation.

Example : Create or update reusable click methods, dropdown handling methods, explicit wait methods, frame and window switching methods, JavaScript interaction fallback, exception handling and logging, screenshot capture for failed interactions, web table handling methods, backward compatibility with existing page objects, and adherence to organisation-wide coding standards.

Objective:
Implement or enhance the requested reusable functionality in alignment
with organisation-wide automation standards and framework design principles.

Instructions:
1. Inspect the existing framework architecture, BasePage, reusable
   interaction methods, and established coding conventions.

2. Identify existing implementations of the requested functionality
   before creating new methods. Extend or improve existing methods
   wherever appropriate to avoid duplication.

3. Ensure the implementation promotes reusability, maintainability,
   consistency, and scalability across page objects and test modules.

4. Follow established organisational standards for:
   - Coding conventions and naming
   - Wait strategies and synchronisation
   - Logging and error handling
   - Screenshot and evidence capture
   - Frame and window management
   - Exception handling and reporting
   - Reusable component design

5. Avoid hardcoding, duplicated logic, unnecessary dependencies,
   and project-specific implementations in shared components.

6. Use JavaScript-based interactions or other fallback mechanisms
   only when justified and compatible with organisational standards.

7. Maintain backward compatibility with existing page objects and
   test scripts wherever feasible. Identify any breaking changes
   and affected components before recommending them.

8. Reuse existing utilities, configuration mechanisms, and design
   patterns. Do not introduce new dependencies or architectural
   changes unless necessary and justified.

9. Validate the implementation against relevant existing tests,
   framework conventions, and applicable quality standards.
   Do not claim validation or test execution unless actually performed.

Expected Output:
- Summary of the existing implementation and identified gaps
- Recommended approach and justification
- Complete updated code, including affected files
- Explanation of how page objects and test modules should use it
- Impact assessment, including compatibility and migration needs
- Validation results, limitations, and any outstanding actions
```
