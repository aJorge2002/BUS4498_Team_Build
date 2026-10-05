# Decide Whether to Investigate Further Task Specification

```yaml
# BASIC INFORMATION
task_id: "T13"
task_name: "Decide Whether to Investigate Further"
task_owner: ""
```

## 1. Task Goal

- **Objective:** Missing, invalid, or inconsistent information triggers selection for a query. Sufficient evidence ends the research. Exhausted

## 2. Inbound Inputs

### Input 1

- **Input name:** collected information
- **What it contains:** missing, invalid, or inconsistent information
- **Source:** T12: Check Support For Key Claims

## 3. Tool Permissions and Boundaries

### Task-Wide Limits

- **Total task timeout:**
- **Maximum tool calls:**

### Tool 1

- **Tool name:** check_support_for_key_claims
- **Tool type:**
- **Supports these permitted subtasks:** Check Support For Key Claims
- **Allowed use:**
- **Prohibited use:**
- **Approval required:** Additional research and other changes must require user approval.
- **Timeout per call:**
- **Maximum retries per call:**
- **Retry conditions and failure response:**

### Tool 2

- **Tool name:** choose_the_next_research_action
- **Tool type:**
- **Supports these permitted subtasks:** Choose the Next Research Action
- **Allowed use:**
- **Prohibited use:**
- **Approval required:** Additional research and other changes must require user approval.
- **Timeout per call:**
- **Maximum retries per call:**
- **Retry conditions and failure response:**

## 4. How the Agent Should Reason

### Permitted Subtask 1

- **Subtask name:** Check Support For Key Claims
- **Subtask description:** AI compares claims with missing, invalid, or inconsistent information. This step’s collected information is saved for the next research decision.
- **Subtask boundary:**
- **Retry limits:**

### Permitted Subtask 2

- **Subtask name:** Choose the Next Research Action
- **Subtask description:** Findings guide what action is permitted to occur next. Can investigate an expansion signal, inspect a website, or refine the discovery queries if the candidate fits poorly.
- **Subtask boundary:**
- **Retry limits:**

### Permitted Subtask 3

- **Subtask name:** Decide Whether to Investigate Further
- **Subtask description:** Missing, invalid, or inconsistent information triggers selection for a query. Sufficient evidence ends the research. Exhausted
- **Subtask boundary:** limits prevent resolution
- **Retry limits:**

- **Decision guidance:** Missing, invalid, or inconsistent information triggers selection for a query. Sufficient evidence ends the research.

## 5. When to Stop or Hand Off to a Human

- **Stop successfully when:** Sufficient evidence ends the research.
- **Hand off early when:** limits prevent resolution
- **Hand off to:** T19: Resolve Uncertain Findings and Exceptions

## 6. Outbound Deliverable

- **Status:**
- **Result or recommendation:**
- **Evidence summary:**
- **Subtasks performed:**
- **Unresolved issues:** missing, invalid, or inconsistent information
- **Handoff note:**
- **Next task or recipient:** T06: Choose the Next Research Action; T14: Score the Opportunity; T19: Resolve Uncertain Findings and Exceptions
