# Decide Whether to Investigate Further Task Specification

```yaml
# BASIC INFORMATION
task_id: "T13"
task_name: "Decide Whether to Investigate Further"
task_owner: "Team Gambit (Adrian Jorge and Pedro Calvillo)"
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

- **Total task timeout:** 5 minutes
- **Maximum tool calls:** 5

### Tool 1

- **Tool name:** check_support_for_key_claims
- **Tool type:** Language-model call
- **Supports these permitted subtasks:** Check Support For Key Claims
- **Allowed use:** Read the Claim support findings and the Research limits, and return a sufficiency finding or a proposed follow-up query with the gap it addresses.
- **Prohibited use:** Running searches, retrieving pages, contacting any business, changing the user's industry or location filters, or editing the findings.
- **Approval required:** Additional research and other changes must require user approval.
- **Timeout per call:** 60 seconds
- **Maximum retries per call:** 1
- **Retry conditions and failure response:** Retry once on a timeout or output that does not match the expected structure. If the retry fails, record the failure and hand off to T19.

### Tool 2

- **Tool name:** choose_the_next_research_action
- **Tool type:** Python script
- **Supports these permitted subtasks:** Choose the Next Research Action
- **Allowed use:** Compare the Research usage so far with the user's Research limits and return whether any limit is exhausted.
- **Prohibited use:** Changing any limit, resetting usage counts, or starting any research.
- **Approval required:** Additional research and other changes must require user approval.
- **Timeout per call:** 10 seconds
- **Maximum retries per call:** 1
- **Retry conditions and failure response:** Retry once on a script error. The check changes no records, so a retry cannot duplicate anything. If the retry fails, treat the limits as unknown and hand off to T19.

## 4. How the Agent Should Reason

### Permitted Subtask 1

- **Subtask name:** Check Support For Key Claims
- **Subtask description:** AI compares claims with missing, invalid, or inconsistent information. This step’s collected information is saved for the next research decision.
- **Subtask boundary:** Uses only the existing findings and their sources. May not retrieve new information or change a claim's status.
- **Retry limits:** 1

### Permitted Subtask 2

- **Subtask name:** Choose the Next Research Action
- **Subtask description:** Findings guide what action is permitted to occur next. Can investigate an expansion signal, inspect a website, or refine the discovery queries if the candidate fits poorly.
- **Subtask boundary:** Only when a gap exists and no research limit is exhausted. The query must keep the user's industry and location filters. It is passed to T06 and not run by this task.
- **Retry limits:** 1

### Permitted Subtask 3

- **Subtask name:** Decide Whether to Investigate Further
- **Subtask description:** Missing, invalid, or inconsistent information triggers selection for a query. Sufficient evidence ends the research. Exhausted
- **Subtask boundary:** limits prevent resolution
- **Retry limits:** 1

- **Decision guidance:** Missing, invalid, or inconsistent information triggers selection for a query. Sufficient evidence ends the research.

## 5. When to Stop or Hand Off to a Human

- **Stop successfully when:** Sufficient evidence ends the research.
- **Hand off early when:** limits prevent resolution
- **Hand off to:** T19: Resolve Uncertain Findings and Exceptions

## 6. Outbound Deliverable

- **Status:** Completed or escalated to human.
- **Result or recommendation:** Either "sufficient evidence" or "investigate further" with the selected follow-up query and the gap it addresses. If escalated before reaching a supported result, write undetermined.
- **Evidence summary:** The claim statuses and findings behind the decision, or why no decision could be reached.
- **Subtasks performed:** Permitted subtasks completed, including repeated attempts.
- **Unresolved issues:** missing, invalid, or inconsistent information
- **Handoff note:** Reason for stopping, unresolved claims, and what the user needs to decide. Not applicable for a completed task.
- **Next task or recipient:** T06: Choose the Next Research Action; T14: Score the Opportunity; T19: Resolve Uncertain Findings and Exceptions
