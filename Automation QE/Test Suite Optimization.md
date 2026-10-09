# Test Suite Optimization

**Module:** Automation QE
**Sub Module:** Failure & Maintenance
**Purpose:** Keep the automation suite fast, trustworthy, and proportionate to risk — by removing duplication, retiring dead tests, rebalancing the test pyramid, and cutting runtime without losing coverage. Runs periodically on suite health data, and on demand when pipeline runtime or flake rate breaches its threshold.

---

## When to use this prompt

- When suite runtime breaches the pipeline budget and teams start skipping or disabling tests to get a green build.
- During scheduled suite health reviews (sprint-end, release-end, or monthly), using run history rather than a single execution.
- When Report Analysis keeps surfacing the same tests in the flaky watchlist run after run.
- When Script Maintenance returns a `RETIRE` verdict, or when the same scenario is found covered at multiple layers.
- Before scaling parallel execution — optimizing a bloated suite first is cheaper than buying more runners.

---

## What Test Suite Optimization is (and isn't)

This is a **portfolio-level decision step** — "which tests should exist, at which layer, and in what shape?" It is **not** triage of a single run (that's Report Analysis) and **not** repairing an individual script (that's Script Maintenance). It is also **not** a runtime-reduction exercise at any cost: deleting tests to make the pipeline fast is coverage loss, not optimization. Every removal here must be justified by duplication, obsolescence, or coverage that exists at a cheaper layer.

---

## Prompt

```
You are a senior test automation architect optimizing an automation suite.
Your job is to decide which tests should be kept, merged, moved to another
layer, refactored, or retired — and to reduce runtime and flake without
reducing risk coverage. You are not triaging a single run, and you are not
repairing individual scripts.

Context:
- Application / module: {APP_OR_MODULE}
- Suite scope: {SMOKE | REGRESSION | FULL | API | UI_E2E}
- Current suite size: {TEST_COUNT}
- Current runtime: {RUNTIME} (budget: {RUNTIME_BUDGET})
- Execution mode: {SEQUENTIAL | PARALLEL_N}
- Current flake rate: {FLAKE_RATE_OR_UNKNOWN}
- Risk / priority areas of the product: {CRITICAL_AREAS}
- Constraints: {ENV_LIMITS_DATA_LIMITS_LICENCE_LIMITS_OR_NONE}

Suite inventory (test names, layer, tags, avg duration, pass/fail history):
"""
{PASTE_SUITE_INVENTORY}
"""

Coverage / requirement mapping (if available):
"""
{PASTE_COVERAGE_MAPPING_OR_NONE}
"""

Analyse the suite across each of the following areas. For each one, state
the finding and the evidence behind it (if none, say "No finding"):

1. **Duplication & Overlap**
   Which tests verify the same behaviour, in whole or in part? Name the
   specific tests and which one should survive, and why.

2. **Layer Placement (Pyramid Balance)**
   Which scenarios are being validated at a more expensive layer than
   necessary (UI test that could be an API or unit test)? State the target
   layer and what is lost by moving it.

3. **Obsolete & Dead Tests**
   Which tests cover removed features, deprecated flows, or permanently
   disabled/skipped paths? Evidence must show the test is dead, not just
   currently failing.

4. **Flake Concentration**
   Which tests account for most of the instability? Rank by flip count or
   failure-without-code-change. Do not label anything flaky on a single
   failure.

5. **Runtime Hotspots**
   Which tests or setup steps consume disproportionate runtime? Identify
   the cause (waits, data setup, repeated login, heavy fixtures, serial
   dependencies) and the specific reduction.

6. **Parallel-Safety & Isolation**
   Which tests block parallel execution through shared data, fixed IDs,
   global state, or inter-test ordering? State what must change to make
   them independent.

7. **Tagging & Suite Segmentation**
   Is the suite sliceable into smoke / critical-path / full regression by
   risk? Propose the segmentation and what each tier should run on
   (per-commit, per-PR, nightly, pre-release).

8. **Coverage Risk of the Proposed Changes**
   For every removal or merge, state the requirement or risk area that
   would lose coverage, and whether it is covered elsewhere. If coverage
   would genuinely be lost, mark the change DO_NOT_REMOVE.

Every recommendation must be a concrete, owner-assignable change with an
expected effect — not a vague "reduce duplication" or "improve speed."

Output in this format:

## Suite Health Verdict
[Healthy — within budget and stable / Needs Tuning — runtime or flake over
threshold / Needs Restructure — duplication or layer imbalance is
systemic]

## Current Baseline
Test count, runtime, flake rate, pass rate, layer distribution — as given.
State "Not supplied" for anything missing; do not estimate.

## Optimization Actions
| # | Test / Group | Action | Rationale | Evidence | Expected Effect | Coverage Risk | Owner |
|---|---|---|---|---|---|---|---|

Action must be one of: KEEP, MERGE, MOVE_LAYER, REFACTOR, ISOLATE,
RETAG, QUARANTINE, RETIRE, DO_NOT_REMOVE.

## Proposed Suite Segmentation
| Tier | Trigger | Contents | Target Runtime |
|---|---|---|---|

## Projected Outcome
Runtime, test count, and flake-rate change — stated as a range, with the
assumption behind each figure.

## Coverage Statement
What the suite still verifies after these changes, and any accepted
coverage trade-off.

## Missing Data / Open Questions
- ...
```

---

## Example

**Context:** UI E2E regression suite; 240 tests; runtime 96 min against a 30 min budget; parallel 4; flake rate 7%.

**Inventory (excerpt):** *12 tests each log in through the UI before asserting an API-visible result. `login_invalid_password` exists in 3 specs with identical steps. `legacy_coupon_flow` skipped for 9 months. `cart_merge_test` and `cart_sync_test` both fail intermittently when run in parallel — both write to the same seeded user.*

**Test Suite Optimization (excerpt):**

**Suite Health Verdict:** Needs Restructure — runtime is 3.2× the budget and the overrun is driven by layer misplacement, not slow infrastructure.

| # | Test / Group | Action | Rationale | Evidence | Expected Effect | Coverage Risk | Owner |
|---|---|---|---|---|---|---|---|
| 1 | 12 UI tests asserting API-visible results | MOVE_LAYER | Outcome is verifiable at the API layer; UI adds no new assertion | All 12 assert response-backed state, not rendering | −28 min est. | None — same assertions, cheaper layer | Automation |
| 2 | `login_invalid_password` ×3 | MERGE | Identical steps and assertions in 3 specs | Step-for-step duplicate | −2 min, −2 tests | None | Automation |
| 3 | `legacy_coupon_flow` | RETIRE | Feature removed; skipped 9 months | Permanently skipped, flow no longer in product | −1 test | None — feature does not exist | QE Lead |
| 4 | `cart_merge_test`, `cart_sync_test` | ISOLATE | Shared seeded user collides under parallel run | Both fail only in parallel, pass serially | Flake −3pp | None | Automation |
| 5 | `checkout_tax_calculation` | DO_NOT_REMOVE | Looks duplicated with `order_total_test` but covers a distinct tax-jurisdiction rule | Only test mapped to REQ-TAX-114 | — | Removal would lose sole coverage | QE Lead |

**Proposed Suite Segmentation:**

| Tier | Trigger | Contents | Target Runtime |
|---|---|---|---|
| Smoke | Per commit | 18 critical-path tests | < 5 min |
| Regression | Per PR | API-layer + high-risk UI | < 25 min |
| Full | Nightly | Everything, including long tail | No cap |

**Projected Outcome:** 240 → 224 tests; runtime 96 → 30–38 min at parallel 4; flake 7% → ~4%. Figures assume the 12 migrated tests keep their current assertion depth at the API layer.

**Coverage Statement:** No requirement loses its only covering test. Accepted trade-off: the 12 migrated scenarios no longer exercise the UI rendering path — covered separately by the smoke tier.

---

## Notes for reviewers

- Optimization is measured in **coverage per minute**, not minutes saved. Any action that cuts runtime while dropping a requirement's only test is a failure of this prompt, which is why Coverage Risk and `DO_NOT_REMOVE` are mandatory outputs.
- This prompt needs **run history, not one run**. Flake and obsolescence claims made from a single execution are guesses — if history isn't supplied, it should say so under Missing Data rather than ranking tests.
- Keep the split with the sibling prompts clean: `report-analysis.md` decides what broke in one run, `script-maintenance.md` changes *how a test works*, and this prompt changes *which tests exist, at which layer, and in which tier*.
- `RETIRE` should never be justified by "it keeps failing." That's a Script Maintenance input. Retirement requires evidence the covered behaviour no longer exists.
- Never let the model invent test names, durations, flake rates, requirement IDs, or coverage mappings that weren't in the pasted inventory. Projected figures must carry their assumption, as in the example.
- Fix parallel-safety (`ISOLATE`) **before** increasing parallel workers — per the roadmap's Parallel Test Execution row, more workers amplify shared-data collisions instead of resolving them.
- Output feeds the Automation Quality Gate (tier thresholds and runtime budgets), Test Execution Pipeline (which tier runs on which trigger), and Reusable Component Design (duplication that should collapse into shared components rather than be deleted).
