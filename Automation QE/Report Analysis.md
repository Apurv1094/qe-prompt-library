# Report Analysis

**Module:** Automation QE
**Sub Module:** Failure & Maintenance
**Purpose:** Turn a raw automation execution report into a triaged, decision-ready analysis — what failed, why it failed, who owns it, and whether the build is safe to promote. Runs after every pipeline execution that produces failures, and feeds Script Maintenance and Test Suite Optimization.

---

## When to use this prompt

- Immediately after a CI/pipeline run produces failures, before anyone starts "fixing" individual tests.
- Before a release or quality-gate decision, to convert a red report into a promote/hold verdict with reasoning.
- During suite health reviews, when you need to separate genuine product defects from script, data, and environment noise.

---

## What Report Analysis is (and isn't)

This is a **cause-classification and verdict step** — "what actually broke, and is this build safe?" It is **not** report generation or dashboard design (that sits under Framework & Standards as Automation Reporting), and it is **not** the fix itself (that's Script Maintenance). Expect some overlap with Test Suite Optimization — a slow, flaky cluster surfaces in both, framed differently: here as a failure cause, there as a suite-design problem.

---

## Prompt

```
You are a senior test automation engineer performing failure triage on an
automation execution report. Your job is to classify failures by root
cause and issue a build verdict — not to generate a report, and not to
write the fix.

Context:
- Application / module: {APP_OR_MODULE}
- Suite type: {API | UI_E2E | MIXED}
- Environment: {ENV}
- Build / commit: {BUILD_ID} / {COMMIT}
- Framework & runner: {FRAMEWORK}
- Known issues / quarantined tests: {KNOWN_ISSUES_OR_NONE}

Report data (summary + failure logs / stack traces):
"""
{PASTE_REPORT_SUMMARY_AND_FAILURE_LOGS}
"""

Analyse the report across each of the following areas. For each one,
state the specific finding and the evidence behind it (if none, say
"No finding"):

1. **Run Health**
   Total, passed, failed, skipped, pass rate, duration, slowest areas.
   Flag any numbers that contradict each other.

2. **Failure Clustering**
   Group failures by shared root cause, not by test name. Collapse
   failures that share one stack trace or one upstream cause.

3. **Cause Classification**
   Label every cluster using exactly one of:
   PRODUCT_DEFECT, SCRIPT_DEFECT, TEST_DATA, ENVIRONMENT,
   TIMING_FLAKY, CONFIG, THIRD_PARTY, KNOWN_ISSUE.
   Quote the exact log line, assertion, or status code that justifies it.

4. **Intermittency Check**
   Is there evidence a failure is non-deterministic (retry passed, same
   test differs across runs)? Do not label anything flaky on a single
   failure.

5. **Ownership & Priority**
   Assign an owner role (Dev / Automation / QE Data / DevOps) and a
   priority P1-P4 per cluster, with the reason for the priority.

6. **Next Action**
   One action per cluster: fix product, fix script, refresh test data,
   fix environment, correct config, add deterministic wait, or quarantine
   (quarantine must carry a review/expiry date).

7. **Build Verdict**
   PROMOTE or HOLD for this build, with the blocking clusters named.

8. **Missing Evidence**
   What artefact is needed to close an unresolved cluster (screenshot,
   HAR, server log, DB snapshot)? If the cause cannot be determined from
   what was supplied, output INSUFFICIENT_EVIDENCE rather than guessing.

For every cluster, phrase the next action as something a named owner can
start today — not a vague "investigate failures."

Output in this format:

## Overall Build Risk
[Low — isolated non-blocking failures / Medium — notable failures needing
triage / High — blocking or widespread failure]

## Run Health Summary
- ...

## Failure Clusters
| # | Cluster | Affected Tests | Classification | Evidence | Owner | Priority | Next Action |
|---|---|---|---|---|---|---|---|

## Flaky Watchlist
| Test | Evidence of Intermittency | Suspected Driver | Recommendation |
|---|---|---|---|

## Build Verdict
PROMOTE | HOLD — with the blocking clusters named.

## Missing Artefacts / Open Questions
- ...
```

---

## Example

**Report (excerpt):** *"142 tests, 128 passed, 11 failed, 3 skipped. 9 failures: `java.net.ConnectException: payments-svc:8080`. 1 failure: `Expected total 1200.00 but was 1080.00`. 1 failure: `ElementNotInteractableException` on #submit, passed on retry."*

**Report Analysis (excerpt):**

| # | Cluster | Classification | Evidence | Owner | Priority | Next Action |
|---|---|---|---|---|---|---|
| 1 | Payments service unreachable | ENVIRONMENT | `ConnectException: payments-svc:8080` across 9 tests | DevOps | P1 | Confirm payments-svc deployment on this env, then re-run the 9 tests |
| 2 | Order total mismatch | PRODUCT_DEFECT | `Expected 1200.00 but was 1080.00` — discount applied twice | Dev | P1 | Raise defect with the failing payload; test logic verified correct |
| 3 | Submit button not interactable | TIMING_FLAKY | Failed once, passed on retry, same build | Automation | P3 | Replace implicit wait with explicit clickable condition |

**Build Verdict:** HOLD — Cluster 2 is a confirmed product defect in order totals; Cluster 1 blocks 9 tests from producing any result.

---

## Notes for reviewers

- This checks **cause**, not **presentation** — pair it with `automation-reporting.md` (relocated under Framework & Standards per the roadmap) for the report format itself.
- Product vs. script defect must always be justified by quoted evidence. An unevidenced guess here sends the wrong team the wrong bug.
- Never let the model invent test names, defect IDs, counts, owners, or dates that weren't supplied in the input.
- The output feeds directly into Script Maintenance (SCRIPT_DEFECT clusters), Test Suite Optimization (TIMING_FLAKY and slow areas), and the Automation Quality Gate (the verdict informs the gate threshold).
- A single failure is never enough to declare a test flaky — require cross-run or retry evidence.
