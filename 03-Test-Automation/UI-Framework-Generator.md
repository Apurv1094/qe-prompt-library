# UI Framework Generator

## Purpose
Create a new reusable UI automation framework.

## When to use
Use this prompt when design and, when authorized, scaffold a reusable UI automation framework. Ensure the required inputs are available.

## Inputs required
- `{{TOOL}}` — **Required:** Selected browser automation tool and version, such as Playwright.
- `{{LANGUAGE}}` — **Required:** Programming language and runtime, such as TypeScript with Node.js.
- `{{DESIGN_PATTERN}}` — **Required:** Preferred architecture such as Page Object Model or fixtures-first.
- `{{PROJECT_REQUIREMENTS}}` — **Required:** Browsers, environments, reporting, test data, CI and execution constraints.

## Prompt
```text
Role: Act as a Senior UI Automation Architect.

Task: Design and, when authorized, scaffold a reusable UI automation framework.

Inputs:
TOOL:
{{TOOL}}
LANGUAGE:
{{LANGUAGE}}
DESIGN_PATTERN:
{{DESIGN_PATTERN}}
PROJECT_REQUIREMENTS:
{{PROJECT_REQUIREMENTS}}

Rules:
- Honor tool, language and selected design pattern; do not force Page Objects if not requested.
- Provide isolated tests, resilient locator conventions, fixtures, config, data and reporting.
- Avoid hardcoded secrets, brittle selectors and arbitrary sleeps.
- Only write files when authorized; inspect destination and avoid overwrites.
- Distinguish generated examples from browser-verified selectors and executed tests.

Deliverables:
- Directory tree, dependency and configuration files
- Fixtures, reusable abstractions, sample UI test and reporting/CI configuration
- Setup commands and validation status
```

## Expected output
- Directory tree, dependency and configuration files
- Fixtures, reusable abstractions, sample UI test and reporting/CI configuration
- Setup commands and validation status
- Clearly label assumptions, missing evidence, and whether files were created or tests executed.

## Example
**Synthetic input:**
```text
TOOL: Playwright; LANGUAGE: TypeScript; DESIGN_PATTERN: Page Object Model; PROJECT_REQUIREMENTS: Chromium, HTML report and CI smoke job.
```

**Illustrative output (not executed):**
> playwright.config.ts → chromium + html reporter; pages/LoginPage.ts → semantic login locators (must verify on AUT); tests/login.spec.ts → sample; command: npx playwright test; not executed.

The example is illustrative only; use actual input evidence for real deliverables.

## Limitations
- Results depend on supplied requirements, repository access, tool availability and authorization.
- Generated code or recommendations are not verified until explicitly checked or executed.
- Shared privacy, evidence, authorization and human-review requirements: `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
