# General Defect Logger

## Purpose

Convert a QA's basic bug description into a clear, structured, and actionable defect report.

The QA can provide the issue in natural language without following any predefined format.

---

## When to Use

Use this prompt when a QA identifies a defect and wants to convert their basic observation into a properly structured defect report.

---

## Input

Paste the basic bug description below.

The description can be written in natural language and may contain any information the QA knows, such as:

* Environment
* Feature / Module
* Actions performed
* Steps followed
* Expected behavior
* Actual behavior
* Error message
* Test data
* Browser / Device
* Evidence

### Bug Description

```While using the Course App, I logged in with a valid student account and navigated to one of my enrolled courses. I opened a video lesson and started playing it. During playback, I opened the video player's settings and changed the video quality. After that, I also adjusted the playback speed. Once both settings were changed, the video's audio started breaking up / becoming distorted, while the video continued to play.```


### Evidence

```[Attach or provide evidence here, if available]```

### Optional Input

```[Video Transcript of Evidence (if available)]```


## Input Guidelines

* The QA can describe the issue in any natural-language format.
* No predefined structure is required.
* The QA does not need to provide every possible field.
* Extract the relevant information from the provided description.
* Preserve the meaning of the QA's description.
* Do not ask the QA to rewrite the description in a specific format.

---

## Agent Responsibilities

The agent should:

1. Understand the reported issue.
2. Create a clear and concise defect title.
3. Generate a brief defect description.
4. Extract the steps to reproduce.
5. Separate expected and actual results.
6. Capture the environment and other available context.
7. Include evidence when provided.
8. Recommend severity and priority when sufficient information is available.
9. Identify important missing information.
10. Keep the final defect concise and actionable.

---

## Defect Title Rules

The title should:

* Be concise.
* Clearly describe the problem.
* Identify the affected feature or area where possible.
* Focus on the observed behavior.
* Avoid unnecessary technical details.
* Avoid assumptions about the root cause.

---

## Description Rules

The description should briefly explain:

* Where the issue occurs.
* What action was performed.
* What problem was observed.
* Any relevant condition provided in the input.

Keep the description factual and concise.

Do not add technical causes or assumptions that are not supported by the input.

---

## Steps to Reproduce Rules

Extract the actions described by the QA and convert them into clear, numbered steps.

Steps should:

* Be sequential.
* Be easy to follow.
* Contain only known or directly derived information.
* Include relevant preconditions when provided.

Do not invent:

* URLs
* User credentials
* Test data
* Navigation paths
* Application states
* Configuration
* Additional actions

If required information is unavailable, mark it as **Unknown / Not Provided**.

---

## Expected vs Actual Rules

Clearly separate:

### Expected Result

Describe what should happen based on the information provided by the QA or the known requirement/acceptance criteria.

### Actual Result

Describe what was actually observed.

Do not mix expected and actual behavior.

If either cannot be determined from the available information, mark it as:

**Unknown / Not Provided**

---

## Evidence Handling

Include evidence when it is provided with the defect input.

Evidence may include:

* Screenshots
* Videos
* Logs
* Error messages
* Browser console output
* API/network information
* Test execution evidence

Do not fabricate or assume evidence.

If no evidence is provided:

**Not Provided**

---

## Severity & Priority Guidelines

Provide recommended Severity and Priority only when sufficient information is available.

The recommendation should be based on the described impact and urgency.

If sufficient information is not available:

**Requires Assessment**

Clearly indicate that these are recommendations and not officially assigned values.

---

## Missing Information / Clarification

Identify only important missing information that may affect:

* Reproduction
* Investigation
* Understanding of the issue
* Assessment of impact

Do not unnecessarily block defect creation because optional information is missing.

---

## Output Structure

### Defect Title

[Clear and concise defect title]

### Description

[Brief description of the issue]

### Environment

[Environment or Unknown / Not Provided]

### Steps to Reproduce

1. [Step]
2. [Step]
3. [Step]

### Expected Result

[Expected behavior]

### Actual Result

[Observed behavior]

### Evidence

[Available evidence or Not Provided]

### Severity

[Recommended severity or Requires Assessment]

### Priority

[Recommended priority or Requires Assessment]

### Missing Information

* [Important missing information, if any]

---

## Quality Rules

### 1. No Fabrication

The agent must never fabricate:

* Application behavior
* Test data
* Environment details
* Reproduction steps
* Error messages
* Evidence
* Root cause
* Technical details

If information is unavailable, mark it as:

**Unknown / Not Provided**

### 2. No Unsupported Assumptions

Do not present assumptions as facts.

### 3. No Root Cause Guessing

The defect should describe the observed problem.

Do not invent or assume the technical root cause.

### 4. Preserve QA Intent

Improve the wording and structure without changing the meaning of the original report.

### 5. Keep It Concise

The generated defect should be suitable for regular day-to-day defect logging.

Avoid unnecessary analysis or lengthy explanations.

### 6. Keep Expected and Actual Separate

Expected Result describes what should happen.

Actual Result describes what happened.

### 7. Make It Actionable

The final defect should provide enough information for a developer or QA to understand and investigate the issue.

### 8. Highlight Important Gaps

If important information is missing, identify it instead of silently making assumptions.