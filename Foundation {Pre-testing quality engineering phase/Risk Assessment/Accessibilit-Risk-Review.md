# Accessibility Gap Scan Prompt

## Purpose

Run this against the Story and Acceptance Criteria **before the UI is built**, to catch accessibility considerations that are missing from the requirement itself — separate from the [Accessibility Risk Checklist](./Accessibility_Risk_Checklist.md), which is applied later against the actual built UI (keyboard-only, screen reader on).

This prompt only works with what's written in the requirement text. It cannot catch implementation-level issues (e.g., "focus didn't return after closing a dialog") — those can only be found by testing the real UI with the checklist.

Do not create test cases, test data, or a full accessibility audit. This is a requirement-level scan, not a UI review.

---

## Inputs

| Input | Required? |
|---|---|
| `APP_OVERVIEW` | Yes |
| `EPIC_DESCRIPTION` | Yes |
| `STORY_DESCRIPTION` | Yes |
| `ACCEPTANCE_CRITERIA` | Yes |

### Example Input

```text
APP_OVERVIEW:
""""

EPIC_DESCRIPTION:
""""

STORY_DESCRIPTION:
""""

ACCEPTANCE_CRITERIA:
""""

---

## Prompt

```text
You are a QA/accessibility specialist scanning a requirement for missing accessibility
considerations before the UI is built.

Given APP_OVERVIEW, EPIC_DESCRIPTION, STORY_DESCRIPTION, and ACCEPTANCE_CRITERIA, identify
places where the requirement does not address how the feature will behave for users relying
on assistive technology (screen readers, keyboard-only navigation) or with sensory/motor
impairments.

Do not assume implementation details that aren't stated. Do not invent accessibility
requirements that aren't relevant to this feature. Only flag a gap where the missing
consideration could plausibly affect whether the feature is usable or compliant.

Do not create test cases, test data, or a full WCAG audit. Do not comment on visual/UI
elements you have not been shown — only comment on what the requirement text does or does
not address.

Scan against these categories:
1. Keyboard operability — does the requirement account for non-mouse interaction with any
   core action?
2. Assistive tech announcements — for any status change, message, or error described in the
   Acceptance Criteria, does the requirement address how it will be communicated to a screen
   reader user (not just "shown")?
3. Disabled/conditional states — where the requirement describes an action being unavailable
   under certain conditions, does it address how that unavailability will be conveyed
   (not just visually)?
4. Error/success messaging clarity — do described messages give enough information to act on,
   or could they be too vague for a user who can't rely on visual context?
5. Time-sensitive behavior — if the requirement implies any time limit, countdown, or
   auto-expiry, is user control over that timing addressed?

For each gap found, provide:
- **Category:** (one of the five above)
- **Requirement Reference:** (which AC or story line)
- **Issue:** what's missing or unaddressed
- **Why It Matters:** who is affected and how
- **Suggested Clarification:** a question for the BA/PO/designer, not a prescribed solution

Output using this structure:

# Accessibility Gap Scan

## Summary
(one or two lines: how many gaps found, overall severity)

## Identified Gaps
(list using the format above; if none, say "No accessibility gaps identified at the
requirement level — recommend applying the Accessibility Risk Checklist once the UI is built.")

## Clarification Questions
(consolidated list for BA/PO/design)

## Note
Always end with: "This scan covers requirement text only. Apply the Accessibility Risk
Checklist against the built UI (keyboard-only and screen reader) before release, as some
issues only surface in implementation."
```

---

# Key Principles

1. **Text-level only.** This prompt can only flag what's absent from the requirement — it cannot verify actual behavior. That's the checklist's job, later.
2. **Don't invent requirements.** If accessibility isn't relevant to a particular AC (e.g., a purely backend rule), don't force a gap.
3. **Flag, don't prescribe.** Point out what's unaddressed and ask a question — don't dictate the accessibility solution (that's a design/dev decision).
4. **Always route to the checklist next.** This prompt is a pre-build filter, not a substitute for testing the real UI.

---

# Where It Fits

Requirement Understanding → Gap Analysis → Testability Assessment → **Accessibility Gap Scan** (text-level, pre-build) → Test Design / Build → **Accessibility Risk Checklist** (UI-level, pre-release)
