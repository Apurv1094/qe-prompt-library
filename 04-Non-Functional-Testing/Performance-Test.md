# Performance Test

## Purpose
Plan meaningful load and performance checks.

## When to use
Use this prompt when evaluating application performance under different workloads to identify response time issues, throughput limitations, resource bottlenecks, and potential scalability risks.

## Inputs required
- `{{SYSTEM_SCOPE}}` — **Required:** Provide the relevant system scope details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{WORKLOAD_EXPECTATIONS}}` — **Required:** Provide the relevant workload expectations details, including scope, identifiers, dates, and supporting evidence where applicable.
- `{{PERFORMANCE_TARGETS}}` — **Required:** Provide the relevant performance targets details, including scope, identifiers, dates, and supporting evidence where applicable.

## Prompt
```text
Act as a Senior Performance Test Engineer.
Task: Define user journeys, load model, metrics, ramp-up, thresholds, observability and environment caveats; do not fabricate benchmarks.

Inputs:
SYSTEM_SCOPE:
{{SYSTEM_SCOPE}}
WORKLOAD_EXPECTATIONS:
{{WORKLOAD_EXPECTATIONS}}
PERFORMANCE_TARGETS:
{{PERFORMANCE_TARGETS}}

Rules:
- Define workload model, baseline, concurrency, ramp-up, SLAs and observability.
- use non-destructive loads within approved capacity.
- Distinguish observed evidence from assumptions and recommendations.
- Do not invent execution results, metrics, approvals, or system behavior.
- Identify missing inputs and explain how they limit conclusions.
- Respect authorized scope, confidentiality, and human approval requirements.
```


## Expected Output

Generate a comprehensive **Performance Test Plan** containing the following sections:

1. **Workload Model**
   - Total concurrent virtual users.
   - User distribution across business operations.
   - Expected request volume or throughput, if available.
   - Workload assumptions and missing information.

2. **Performance Scenario Matrix**

   Include the following columns:
   - Scenario ID
   - Scenario Description
   - Test Type (Load, Stress, Spike, or Endurance)
   - Concurrent Users
   - Ramp-up Duration
   - Steady-state Duration
   - Acceptance Criteria
   - Execution Status

3. **Performance Metrics**
   - Response time (average, p90, p95, p99).
   - Throughput (requests/second).
   - Error rate.
   - CPU and memory utilization.
   - Active connections and resource consumption, where applicable.

4. **Environment Prerequisites**
   - Performance testing environment and infrastructure.
   - Test data requirements.
   - Load generation tools and monitoring configuration.
   - Network and environment dependencies.

5. **Result Interpretation**
   - Compare measured results against acceptance thresholds.
   - Identify performance bottlenecks and potential risks.
   - Separate observed findings from recommendations.
   - Mark unavailable execution evidence as `Not provided`.

## Example

**Synthetic input:**

```text
WORKLOAD_PROFILE:
- 100 concurrent users:
- 70% browsing products
- 30% searching products

PERFORMANCE_REQUIREMENTS:
- p95 response time < 2 seconds
```

**Illustrative output (not executed):**

### 1. Workload Model

| Parameter | Value |
|---|---|
| Total Concurrent Users | 100 |
| Browse Users | 70 |
| Search Users | 30 |
| Target Throughput | Not provided |
| Think Time | Not provided |
| Workload Pattern | Constant concurrency assumed for illustration |

### 2. Performance Scenario Matrix

*Durations below are proposed planning values, not supplied requirements.*

| Scenario ID | Scenario Description | Test Type | Concurrent Users | Ramp-up Duration | Steady-state Duration | Acceptance Criteria | Execution Status |
|---|---|---|---|---|---|---|---|
| PERF-01 | Browse products | Load | 70 | 5 min | 15 min | p95 < 2 s | Not executed |
| PERF-02 | Search products | Load | 30 | 5 min | 15 min | p95 < 2 s | Not executed |
| PERF-03 | Mixed browse and search workload (70:30) | Load | 100 total | 5 min | 15 min | p95 < 2 s | Not executed |

*PERF-01 and PERF-02 represent individual workload components. PERF-03 represents the combined workload; these are alternative test configurations, not 200 simultaneous users.*

### 3. Performance Metrics

| Metric | Acceptance Threshold | Actual Result |
|---|---|---|
| p95 Response Time | < 2 seconds | Not provided |
| Average Response Time | Not provided | Not provided |
| p90 / p99 Response Time | Not provided | Not provided |
| Throughput | Not provided | Not provided |
| Error Rate | Not provided | Not provided |
| CPU Utilization | Not provided | Not provided |
| Memory Utilization | Not provided | Not provided |

### 4. Environment Prerequisites

| Prerequisite | Details / Status |
|---|---|
| Test Environment | Not provided |
| Performance Tool | JMeter or k6 (suggested) |
| Test Data | Product catalog and valid search queries required |
| Monitoring | Application and infrastructure monitoring recommended |
| Network Configuration | Not provided |
| Environment Capacity | Must support 100 concurrent users |

### 5. Result Interpretation

**Observed Findings:**
- No performance tests have been executed.
- Actual response times, throughput, and resource utilization are not available.

**Recommendations:**
- Execute the mixed-workload load test with 100 concurrent users.
- Measure p95 response time separately for browsing and searching, and for the overall workload.
- Compare measured p95 values against the 2-second acceptance threshold.
- Monitor throughput, errors, CPU, and memory to identify potential bottlenecks.
- Confirm proposed ramp-up and test durations before execution.

*This example illustrates the expected performance test planning output. No tests were executed, and no performance results have been verified.*

## Limitations
- Synthetic workloads may not mirror real traffic.
- results are environment-specific and require approved load limits.

Shared privacy, evidence, authorization and human-review requirements are defined in `00-Library-Guide/Guardrails-Data-Privacy.md`.

## Owner / Version
- Owner: QE Prompt Library maintainers (assign named owner before publication)
- Version: 1.2.0
- Status: Draft for team review
