# Choose the Next Research Action Task Specification

```yaml
# BASIC INFORMATION
task_id: "T06"
task_name: "Choose the Next Research Action"
task_owner: "Team Gambit (Adrian Jorge and Pedro Calvillo) "
```

## 1. Task Goal

- **Objective:** Findings guide what action is permitted to occur next. Can investigate an expansion signal, inspect a website, or refine the discovery queries if the candidate fits poorly.

## 2. Inbound Inputs

### Input 1

- **Input name:** Findings
- **What it contains:** businesses and sources
- **Source:** T05: Discover Candidate Businesses; T13: Decide Whether to Investigate Further

## 3. Tool Permissions and Boundaries

### Task-Wide Limits

- **Total task timeout:** 10 minutes
- **Maximum tool calls:** 6

### Tool 1

- **Tool name:** discover_candidate_businesses
- **Tool type:** Read-only web search
- **Supports these permitted subtasks:** refine the discovery queries
- **Allowed use:** Run revised queries using the user's industry and location filters, and return businesses with their source links.
- **Prohibited use:** Changing the user's industry or location filters, contacting any business, or searching beyond the user's research limits.
- **Approval required:** Additional research and other changes must require user approval.
- **Timeout per call:** 30 seconds
- **Maximum retries per call:** 2
- **Retry conditions and failure response:** Retry on timeout or an error response. After the second retry fails, stop using this tool, record the failure, and choose another permitted subtask or hand off to T19.

### Tool 2

- **Tool name:** retrieve_permitted_public_resources
- **Tool type:** Read-only web page retrieval
- **Supports these permitted subtasks:** investigate an expansion signal; inspect a website
- **Allowed use:** Anything publicly available.
- **Prohibited use:** Pages that require a login or payment, submitting forms, bypassing access restrictions, collecting private personal data, or contacting any business.
- **Approval required:** Additional research and other changes must require user approval.
- **Timeout per call:** 30 seconds
- **Maximum retries per call:** 2
- **Retry conditions and failure response:** Retry on timeout or a temporary error. If the page is unavailable or restricted, do not retry, record it as missing, and choose another permitted subtask or hand off to T19.

## 4. How the Agent Should Reason

### Permitted Subtask 1

- **Subtask name:** investigate an expansion signal
- **Subtask description:** Findings guide what action is permitted to occur next.
- **Subtask boundary:** Public sources only, one business at a time, within the user's research limits.
- **Retry limits:** 1

### Permitted Subtask 2

- **Subtask name:** inspect a website
- **Subtask description:** Tools fetch websites, service pages, landing pages, reviews, listings, and job postings.
- **Subtask boundary:** Anything publicly available.
- **Retry limits:** 1

### Permitted Subtask 3

- **Subtask name:** refine the discovery queries
- **Subtask description:** refine the discovery queries if the candidate fits poorly.
- **Subtask boundary:** if the candidate fits poorly
- **Retry limits:** 2

- **Decision guidance:** Findings guide what action is permitted to occur next. Can investigate an expansion signal, inspect a website, or refine the discovery queries if the candidate fits poorly.

## 5. When to Stop or Hand Off to a Human

- **Stop successfully when:** One permitted next action is selected, is supported by a cited finding and source, and fits within the user's research limits and the task-wide limits.
- **Hand off early when:** limits prevent resolution
- **Hand off to:** T19: Resolve Uncertain Findings and Exceptions

## 6. Outbound Deliverable

- **Status:** Completed or escalated to human.
- **Result or recommendation:** The selected next action and its target business. If escalated before reaching a supported result, write undetermined.
- **Evidence summary:** The findings and sources that justify the chosen action, or why no action could be chosen.
- **Subtasks performed:** Permitted subtasks completed, including repeated attempts.
- **Unresolved issues:** missing, invalid, or inconsistent information
- **Handoff note:** If escalated, what was tried, what blocked progress, and what the user needs to decide. Not applicable for a completed task.
- **Next task or recipient:** T05: Discover Candidate Businesses; T07: Retrieve Permitted Public Resources
