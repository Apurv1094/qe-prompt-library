# QE Prompt Library — Guide

## Purpose
Provide a lightweight, reusable, privacy-safe QE prompt library ordered from discovery to improvement.

## When to use
Use this guide before selecting a prompt.

## Inputs required
- QE activity and sanitized supporting evidence.

## Prompt
Select the numbered lifecycle folder, open the most specific prompt, replace every `{{PLACEHOLDER}}` with synthetic or approved sanitized information, and review the output before use.

## Expected output
An evidence-based QE deliverable that can be checked by a human reviewer.

## Example
For a new story, start at `01-Foundation/Requirements-Analysis/Requirement-Understanding.md`, then proceed to test design and automation as needed.

## Limitations
Prompts are instructions, not autonomous agents. A model without access to code or tools cannot inspect or execute them. Never paste secret Keys, API Keys, tokens or credentials.

## Owner / Version
- Owner: QE Prompt Library maintainers
- Version: 1.0.0

## Lifecycle
00 Guide → 01 Foundation → 02 Test Design and Prep → 03 Test Automation → 04 Non-Functional Testing → 05 Execution and Analysis → 06 Reporting and Release → 07 Continuous Improvement.

## Scope clarification
The framework generators create **new** frameworks; script generators inspect **existing** frameworks. UI Workflow Script Generator consumes the output of Workflow Generator. Manual-to-Automation includes the handoff.
