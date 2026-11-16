# Contribution Guide

## Purpose
Keep contributions consistent, safe and reviewable.

## When to use
Before adding, changing, reviewing or retiring a prompt.

## Inputs required
- Proposed prompt and use case
- Assigned owner

## Prompt
Review whether the proposal has a distinct QE purpose, minimal inputs, eight standard sections, synthetic example, measurable output and privacy safeguards. Compare with existing prompts for overlap.

## Expected output
Approve, request edits, merge or reject with reason.

## Example
Rename `Code_Review.md` to `Automation-Code-Review.md`; move to `03-Test-Automation/`.

## Limitations
Review does not replace security or legal approval.

## Owner / Version
- Owner: QE Prompt Library maintainers
- Version: 1.0.0

## Rules
- Use `Title-Case-With-Hyphens` for all files and folders; lifecycle folders use `00-` to `07-`. Avoid braces, spaces and underscores in paths.
- Use `{{UPPER_SNAKE_CASE}}` placeholders **inside files only**.
- Require PR review by a QE peer and relevant security/privacy owner for sensitive prompts.
- Semantic versioning: patch for copy fixes, minor for backward-compatible prompt changes, major for breaking input/output changes.
- Keep examples synthetic; check links, filenames, input contracts, and output quality.
- Retire duplicate prompts with a migration note in the PR; do not silently discard valuable behavior.
