# Choose the Next Research Action Task Specification

```yaml
# BASIC INFORMATION
task_id: "T06"
task_name: "Choose the Next Research Action"
task_owner: ""
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

- **Total task timeout:**
- **Maximum tool calls:**

### Tool 1

- **Tool name:** discover_candidate_businesses
- **Tool type:**
- **Supports these permitted subtasks:** refine the discovery queries
- **Allowed use:**
- **Prohibited use:**
- **Approval required:** Additional research and other changes must require user approval.
- **Timeout per call:**
- **Maximum retries per call:**
- **Retry conditions and failure response:**

### Tool 2

- **Tool name:** retrieve_permitted_public_resources
- **Tool type:**
- **Supports these permitted subtasks:** investigate an expansion signal; inspect a website
- **Allowed use:** Anything publicly available.
- **Prohibited use:**
- **Approval required:** Additional research and other changes must require user approval.
- **Timeout per call:**
- **Maximum retries per call:**
- **Retry conditions and failure response:**

## 4. How the Agent Should Reason

### Permitted Subtask 1

- **Subtask name:** investigate an expansion signal
- **Subtask description:** Findings guide what action is permitted to occur next.
- **Subtask boundary:**
- **Retry limits:**

### Permitted Subtask 2

- **Subtask name:** inspect a website
- **Subtask description:** Tools fetch websites, service pages, landing pages, reviews, listings, and job postings.
- **Subtask boundary:** Anything publicly available.
- **Retry limits:**

### Permitted Subtask 3

- **Subtask name:** refine the discovery queries
- **Subtask description:** refine the discovery queries if the candidate fits poorly.
- **Subtask boundary:** if the candidate fits poorly
- **Retry limits:**

- **Decision guidance:** Findings guide what action is permitted to occur next. Can investigate an expansion signal, inspect a website, or refine the discovery queries if the candidate fits poorly.

## 5. When to Stop or Hand Off to a Human

- **Stop successfully when:**
- **Hand off early when:** limits prevent resolution
- **Hand off to:** T19: Resolve Uncertain Findings and Exceptions

## 6. Outbound Deliverable

- **Status:**
- **Result or recommendation:**
- **Evidence summary:**
- **Subtasks performed:**
- **Unresolved issues:** missing, invalid, or inconsistent information
- **Handoff note:**
- **Next task or recipient:** T05: Discover Candidate Businesses; T07: Retrieve Permitted Public Resources
