# Script Maintenance

**Module:** Automation QE
**Sub Module:** Failure & Maintenance
**Purpose:** Decide and specify the correct repair for an automation script that has broken, drifted, or become unreliable — at the right level (local fix vs. reusable component vs. framework), without masking a real product defect. Runs after Report Analysis has classified a failure as SCRIPT_DEFECT, TIMING_FLAKY, TEST_DATA, or CONFIG.

---

## When to use this prompt

- Right after Report Analysis hands you a cluster labelled SCRIPT_DEFECT, TIMING_FLAKY, TEST_DATA, or CONFIG.
- When the application changed intentionally (new UI, renamed field, changed API contract) and existing scripts must be realigned.
- When a test is "fixed" repeatedly run after run — a signal the repair is happening at the wrong level.
- Before un-quarantining a test, to confirm the underlying cause was actually addressed.

---

## What Script Maintenance is (and isn't)

This is a **repair-design step** — "what exactly must change in the automation code, and at which layer?" It is **not** triage (that's Report Analysis, which decides *whether* the script is at fault), and it is **not** suite-level restructuring, dedup, or runtime reduction (that's Test Suite Optimization). It is also **not** a place to make a failing test pass by weakening an assertion or adding blind retries — if the product is wrong, this prompt must refuse the fix and route it back as a defect.

---

## Prompt

```
You are a senior test automation engineer deciding how to repair a broken
or unreliable automation script. Your job is to specify the correct fix at
the correct layer — not to re-triage the failure, and not to make the test
pass by weakening it.

Context:
- Application / module: {APP_OR_MODULE}
- Suite type: {API | UI_E2E | MIXED}
- Framework & language: {FRAMEWORK}
- Triage classification from Report Analysis: {SCRIPT_DEFECT | TIMING_FLAKY |
  TEST_DATA | CONFIG}
- What changed in the product (if known): {APP_CHANGE_OR_UNKNOWN}
- Failure history: {FAILS_ALWAYS | FAILS_INTERMITTENTLY | FAILS_ON_ONE_ENV}

Failing script / step definitions / page objects:
"""
{PASTE_SCRIPT_AND_HELPERS}
"""

Failure evidence (stack trace, assertion message, logs):
"""
{PASTE_FAILURE_EVIDENCE}
"""

Assess each of the following areas. For each one, state the finding and
the evidence behind it (if none, say "No finding"):

1. **Fix Legitimacy**
   Does the evidence actually support a script-side fix? If the product
   behaviour looks wrong, output DO_NOT_FIX_SCRIPT and state the defect
   to raise instead.

2. **Locator / Contract Drift**
   Are selectors, endpoints, payload fields, or response schemas out of
   sync with the current application? Name the exact locator or field and
   the stable alternative.

3. **Synchronisation Strategy**
   Is the failure caused by waits, sleeps, or race conditions? Specify the
   deterministic condition to wait on (element state, network idle, status
   transition) instead of a time-based wait.

4. **Assertion Integrity**
   Is the assertion too strict, too loose, or asserting the wrong thing?
   Any change that reduces coverage must be called out explicitly as a
   coverage trade-off.

5. **Test Data & Isolation**
   Does the script depend on pre-existing, shared, or order-dependent
   data? Specify the setup/teardown or data-generation change needed so
   the test can run standalone and in parallel.

6. **Fix Layer**
   Should this change live in the test, a page object / API client, a
   reusable component, or the framework? If the same symptom affects
   multiple tests, the fix belongs upstream — say so.

7. **Blast Radius**
   Which other tests, components, or suites are affected by this change?
   List what must be re-run to prove nothing regressed.

8. **Verification & Exit Criteria**
   How will the fix be proven? Specify re-run count, environments, and the
   condition for closing or un-quarantining the test.

Every recommendation must be a concrete change a named owner can implement
today — not a vague "improve stability" or "add better waits."

Output in this format:

## Maintenance Verdict
[FIX_SCRIPT — script-side defect confirmed / FIX_UPSTREAM — framework or
reusable component change required / DO_NOT_FIX_SCRIPT — product defect,
route back / RETIRE — test no longer valid]

## Root Cause of Breakage
- ...

## Change Plan
| # | File / Component | Change | Fix Layer | Reason | Risk |
|---|---|---|---|---|---|

## Coverage Impact
What the test verified before vs. after. State "No reduction" if nothing
was weakened.

## Blast Radius & Re-run Set
- ...

## Verification & Exit Criteria
- ...

## Missing Evidence / Open Questions
- ...
```

---

## Example

**Context:** Triage classification `SCRIPT_DEFECT`; UI E2E suite; fails always since the last release.

**Evidence (excerpt):** *`NoSuchElementException: #billing-submit-btn`. Release notes: checkout form rebuilt as a component; submit button now `[data-testid="checkout-submit"]`. Same locator is hard-coded in 6 specs.*

**Script Maintenance (excerpt):**

**Maintenance Verdict:** FIX_UPSTREAM — the locator is duplicated across 6 specs; repairing one spec leaves five to break again.

| # | File / Component | Change | Fix Layer | Reason | Risk |
|---|---|---|---|---|---|
| 1 | `CheckoutPage` object | Add `submitButton` using `[data-testid="checkout-submit"]` | Page object | Single source of truth for the new component | Low |
| 2 | 6 affected specs | Replace hard-coded `#billing-submit-btn` with `CheckoutPage.submitButton` | Test | Removes duplicated locator | Low |
| 3 | `CheckoutPage.submit()` | Wait on button `enabled` before click, not a 2s sleep | Page object | Form enables submit after async validation | Low |

**Coverage Impact:** No reduction — assertions unchanged, only locator and wait strategy replaced.

**Blast Radius & Re-run Set:** Full checkout suite (18 tests) plus the 2 payment specs that reuse `CheckoutPage`.

**Verification & Exit Criteria:** 3 consecutive green runs of the checkout suite on staging, including one parallel run, before the change merges.

---

## Notes for reviewers

- This prompt must never "fix" a failing test by relaxing an assertion, adding a blind retry, or catching and swallowing an error. Those are coverage losses disguised as maintenance — the Coverage Impact section exists to make them visible.
- Pair it with `report-analysis.md` upstream: if the classification is `PRODUCT_DEFECT` or `ENVIRONMENT`, this prompt should return `DO_NOT_FIX_SCRIPT` rather than attempting a repair.
- Repeated local fixes for the same symptom are the main signal to escalate the fix layer. If the same breakage hits three or more tests, the change belongs in a reusable component per Reusable Component Design, not in the tests.
- Never let the model invent locators, endpoints, field names, file paths, or framework APIs that weren't present in the pasted code. If the needed selector isn't in the evidence, it should ask for the DOM snippet or contract.
- Any change to a shared component must carry a blast radius and a named re-run set — that's the difference between maintenance and a silent regression.
- Overlap with Test Suite Optimization is expected (a flaky test may be both repaired here and restructured there). Keep the split clean: this prompt changes *how a test works*, the other changes *which tests exist and how they're organised*.
- Output feeds the Automation Quality Gate (un-quarantine decisions) and Test Suite Optimization (tests flagged RETIRE).
