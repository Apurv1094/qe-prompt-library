# Requirement Gap Analysis

**Module:** Foundation — Pre-testing Quality Engineering Phase
**Sub Module:** Requirements Analysis
**Purpose:** Probe a requirement for real-world scenarios and edge conditions it doesn't address — regardless of how well-formed its structure is. Runs alongside Requirement Completeness Review, after Requirement Understanding.

---

## When to use this prompt

- Right after Requirement Understanding, to surface scenarios the requirement is silent on before test design begins.
- During requirement/story refinement, to raise "what about..." questions with Business/Dev before sign-off.
- When a requirement looks structurally complete but you suspect real usage will hit situations it doesn't cover.

---

## What Gap Analysis is (and isn't)

This is a **scenario/coverage check** — "what situations exist that this requirement doesn't account for?" It is **not** a structural check (that's Requirement Completeness Review, which asks "does this requirement have all its pieces?"). Expect some overlap between the two — a missing failure-handling clause can show up in both, framed differently.

---

## Prompt

```
You are a senior QA engineer probing a requirement for gaps in scenario
coverage. Your job is to identify real-world situations, edge conditions,
and interactions the requirement does not address — not to check its
structural completeness (that is a separate step), and not to write test
cases.

Requirement (or the restated understanding from Requirement Understanding):
"""
{PASTE_REQUIREMENT_OR_RESTATED_SUMMARY}
"""

Probe the requirement across each of the following gap categories. For
each one, list the specific scenarios/questions this requirement does
not address (if none, say "No gap identified"):

1. **Alternate/Secondary Flows**
   Are there other valid paths to the same outcome that aren't mentioned
   (e.g., repeating the action, undoing it, an alternate entry point)?

2. **Concurrent/Simultaneous Actions**
   What happens if this action is performed twice, by two users, or from
   two devices/sessions at the same time?

3. **State Changes Over Time**
   What happens if related data changes between steps (e.g., the target
   record is deleted, permissions change mid-flow, a dependency expires)?

4. **Boundary/Unusual Input**
   What untested input shapes could occur (unexpected format, unusual
   but valid values, culturally/locale-specific variations)?

5. **Downstream/Side Effects**
   Does this action affect anything elsewhere in the system that isn't
   mentioned (other screens, notifications, reports, related records)?

6. **Reversal/Undo**
   Can this action be undone, reversed, or corrected? Is that addressed?

7. **Interaction with Other Features**
   Does this requirement interact with existing features/permissions/
   business rules that could conflict or need reconciling?

8. **Moderation/Review/Compliance**
   If content or data is involved, is there any review, approval, or
   compliance step expected before it takes effect — and is that stated?

For every gap identified, phrase it as a specific open question that
could be sent back to Business/Dev — not a vague "consider edge cases."

Output in this format:

## Overall Gap Risk
[Low — requirement covers realistic scenarios / Medium — some notable
gaps / High — significant scenario coverage missing]

## Gaps by Category
| Category | Gap Identified | Question for Business/Dev |
|---|---|---|
| Alternate/Secondary Flows | ... | ... |
| Concurrent/Simultaneous Actions | ... | ... |
| State Changes Over Time | ... | ... |
| Boundary/Unusual Input | ... | ... |
| Downstream/Side Effects | ... | ... |
| Reversal/Undo | ... | ... |
| Interaction with Other Features | ... | ... |
| Moderation/Review/Compliance | ... | ... |

## Highest-Priority Gaps to Resolve Before Test Design
- ...
```

---

## Example

**Requirement:** *"Users can upload a profile picture. The image is displayed on their profile page."*

**Gap Analysis (excerpt):**
| Category | Gap Identified | Question for Business/Dev |
|---|---|---|
| Alternate/Secondary Flows | No mention of replacing or removing an existing picture | Does a new upload replace the old one, or can users have none? |
| Concurrent/Simultaneous Actions | No mention of simultaneous uploads from two devices | What happens if the same user uploads from two sessions at once? |
| Moderation/Review/Compliance | No mention of content review before the image goes live | Is there any moderation step, or is the image public immediately? |

---

## Notes for reviewers

- This checks **scenarios**, not **shape** — pair it with `requirement-completeness-review.md` for full pre-testing coverage of a requirement.
- Some overlap with Completeness Review is expected (e.g., missing failure handling shows up in both). That's fine — they're framing the same underlying issue from two angles.
- The output here feeds directly into Missing Scenario Identification and Test Strategy — treat "Highest-Priority Gaps" as a pre-checklist for what test design must not skip.
