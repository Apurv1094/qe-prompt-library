# UI Workflow Script Generator

## Purpose
Implement workflow scripts from approved workflow definitions.

## When to use
Use this prompt when implement approved multi-step workflows inside an existing UI framework. Ensure the required inputs are available.

## Inputs required
- `{{EXISTING_FRAMEWORK_PATH}}` — **Required:** Existing UI automation project and reusable components.
- `{{GENERATED_WORKFLOWS}}` — **Required:** Approved ordered workflow IDs, linked test cases, actions and checkpoints.

## Prompt
```text
Role: Act as a Senior End-to-End UI Automation Engineer.

Task: Implement approved multi-step workflows inside an existing UI framework.

Inputs:
EXISTING_FRAMEWORK_PATH:
{{EXISTING_FRAMEWORK_PATH}}
GENERATED_WORKFLOWS:
{{GENERATED_WORKFLOWS}}

Rules:
- Preserve the supplied step order, test IDs, assertions and state transitions.
- Reuse existing fixtures, page objects and setup/teardown; avoid unnecessary duplicate actions.
- Check dependencies and isolate test state; avoid chaining unrelated scenarios.
- Verify locators when browser access is available; otherwise flag unverified details.
- Do not execute without authorization and do not report unobserved passes.

Deliverables:
- Workflow ID-to-script mapping and exact paths
- Ordered actions and assertion checkpoints
- Shared setup/cleanup, dependencies and execution command
- Validation status, risks and unresolved gaps
```

## Expected output
- Workflow ID-to-script mapping and exact paths
- Ordered actions and assertion checkpoints
- Shared setup/cleanup, dependencies and execution command
- Validation status, risks and unresolved gaps
- Clearly label assumptions, missing evidence, and whether files were created or tests executed.

## Example
**Synthetic input:**
```text
EXISTING_FRAMEWORK_PATH: ./ui-tests; GENERATED_WORKFLOWS: WF01 = TC01 login → TC02 add item → TC03 verify cart badge.
```

**Illustrative output (not executed):**
> WF01 → tests/workflows/cart.spec.ts; checkpoint 1 Products heading, checkpoint 2 cart badge=1; fixture creates isolated context; execution Not performed.

The example is illustrative only; use actual input evidence for real deliverables.

## Limitations
- Results depend on supplied requirements, repository access, tool availability and authorization.
- Generated code or recommendations are not verified until explicitly checked or executed.
- Shared privacy, evidence, authorization and human-review requirements: `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
