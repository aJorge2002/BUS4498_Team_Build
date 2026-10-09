# Decide Whether to Investigate Further Task Specification

```yaml
# BASIC INFORMATION
task_id: "T13"
task_name: "Decide Whether to Investigate Further"
task_owner: "Team Gambit (Adrian Jorge and Pedro Calvillo)"
```

## 1. Task Goal

- **Objective:** Evaluate verified findings, missing or inconsistent information, previous research attempts, and remaining research limits to determine whether sufficient evidence exists to score an opportunity, additional research is needed, or human intervention is required.

## 2. Inbound Inputs

### Input 1

- **Input name:** claim_verification_results
- **What it contains:** Verified claims, supporting evidence, source references, missing information, contradictory findings, and unresolved questions.
- **Source:** T12: Check Support For Key Claims

### Input 2

- **Input name:** research_history_and_limits
- **What it contains:** Previous research attempts, completed queries, remaining research limits, approved industry and location filters, and existing research authorization.
- **Source:** T03: Validate Required Inputs; T06: Choose the Next Research Action; T07: Retrieve Permitted Public Resources; T19: Resolve Uncertain Findings and Exceptions when authorization has been granted.

## 3. Tool Permissions and Boundaries

### Task-Wide Limits

- **Total task timeout:** 5 minutes, including retries and waiting.
- **Maximum tool calls:** 5, including retries.

### Tool 1

- **Tool name:** assess_evidence_sufficiency
- **Tool type:** Language-model call
- **Supports these permitted subtasks:** Assess Evidence Sufficiency
- **Allowed use:** Analyze existing verification results, supporting sources, and unresolved findings to determine whether evidence is sufficient for preliminary opportunity scoring. Identify gaps that could benefit from additional research.
- **Prohibited use:** Running searches, retrieving pages, changing verification results, inventing evidence, or contacting businesses.
- **Approval required:** None within the allowed use.
- **Timeout per call:** 60 seconds
- **Maximum retries per call:** 1
- **Retry conditions and failure response:** Retry once after a temporary API error, timeout, or invalid response format. If the retry fails, record the error and escalate to T19.

### Tool 2

- **Tool name:** check_remaining_research_limits
- **Tool type:** Python script
- **Supports these permitted subtasks:** Check Remaining Research Limits
- **Allowed use:** Compare previous research usage against the user's research limits and determine whether additional research is permitted under existing authorization.
- **Prohibited use:** Modifying limits, resetting research counts, running searches, or granting research authorization.
- **Approval required:** None within the allowed use.
- **Timeout per call:** 10 seconds
- **Maximum retries per call:** 1
- **Retry conditions and failure response:** Retry once after a temporary processing error. If the retry fails, record the error, treat remaining limits as unknown, and escalate to T19.

## 4. How the Agent Should Reason

### Permitted Subtask 1

- **Subtask name:** Assess Evidence Sufficiency
- **Subtask description:** Examine claim verification results, supporting evidence, inconsistencies, and missing information to determine whether the opportunity can reasonably proceed to preliminary scoring.
- **Subtask boundary:** Use existing information only. Do not retrieve new evidence, change verification statuses, or present suspected problems as confirmed facts.
- **Retry limits:** 1

### Permitted Subtask 2

- **Subtask name:** Check Remaining Research Limits
- **Subtask description:** Review completed research activity, remaining limits, and authorization status to determine whether additional investigation is permitted.
- **Subtask boundary:** Do not change research limits, authorize additional research, or execute searches.
- **Retry limits:** 1

### Permitted Subtask 3

- **Subtask name:** Determine Next Research Decision
- **Subtask description:** Decide whether to proceed to opportunity scoring, recommend additional research, or escalate unresolved issues for human review.
- **Subtask boundary:** Additional research must address a specific evidence gap and receive the required user authorization. T13 may propose research but cannot execute it. Research outside approved limits must be escalated to T19.
- **Retry limits:** 0

- **Decision guidance:** Select permitted subtasks based on the most important remaining uncertainty rather than following a fixed sequence. Proceed to T14 when existing evidence is sufficient for preliminary opportunity scoring. Return to T06 when additional research is needed and already authorized. Otherwise, request approval through T19. Stop when further research cannot meaningfully improve the decision or when task limits are reached.

## 5. When to Stop or Hand Off to a Human

- **Stop successfully when:** A supported research decision has been recorded and routed to T14 for scoring or T06 for already-authorized additional research.
- **Hand off early when:** Research limits are exhausted, additional research requires approval, important evidence conflicts cannot be resolved, tools fail, or no permitted subtask can make useful progress.
- **Hand off to:** T19: Resolve Uncertain Findings and Exceptions, for human review and authorization.

Stop at the first applicable research limit, task-wide limit, or handoff condition. Do not continue autonomous action while awaiting human review.

## 6. Outbound Deliverable

- **Status:** Completed or escalated to human.
- **Result or recommendation:** Proceed to scoring, investigate further, or escalate for human review. Include the reason for the decision and any specific evidence gap requiring investigation. If no supported decision can be reached, record undetermined.
- **Evidence summary:** Claim verification statuses, supporting sources, contradictory findings, and the evidence supporting the decision.
- **Subtasks performed:** Completed evidence assessments, research-limit checks, and repeated attempts.
- **Unresolved issues:** Missing, invalid, inconsistent, or insufficient information.
- **Handoff note:** When escalated, identify previous research attempts, unresolved findings, exhausted limits, and the decision or authorization required from the user. Not applicable for completed tasks.
- **Next task or recipient:** T06: Choose the Next Research Action; T14: Score the Opportunity; T19: Resolve Uncertain Findings and Exceptions.
