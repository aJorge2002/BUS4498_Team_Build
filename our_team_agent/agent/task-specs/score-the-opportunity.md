# Rank Scored Opportunities Task Specification

## Basic Information

- **Task ID:** T15
- **Task name:** Rank Scored Opportunities
- **Task type:** Act
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Ranks potential consulting opportunities using the weighted scores calculated in T14.

The task organizes businesses from highest to lowest opportunity score based on the predefined scoring criteria and weights approved by Team Gambit.

Each ranked opportunity retains its supporting evidence, individual criterion scores, overall score, and unresolved uncertainties.

The task does not change previously calculated scores or create new scoring criteria. Opportunities with incomplete or invalid scores are flagged rather than assigned an unsupported ranking.

## 2. Inputs

### Input 1

- **Input name:** opportunity_scores
- **Contents and format:** List or table containing business identifiers, individual criterion scores, predefined weights, overall weighted scores, supporting evidence, uncertainties, and scoring statuses.
- **Source:** T14: Score the Opportunity

- **If a required input is missing or invalid:** Identify missing or invalid scores and return affected records to T14 for correction. Do not assign rankings to opportunities without valid scores. Send technical processing failures to T18: Handle Retrieval and Tool Exceptions.

## 3. Outputs

### Output 1

- **Output name:** ranked_opportunities
- **Contents and format:** Ranked list or table containing business identifiers, business names, overall opportunity scores, ranking positions, relevant consulting services, supporting evidence, and unresolved uncertainties. Record any excluded or unranked opportunities and their reasons.
- **Next task or recipient:** T16: Draft Brief and Outreach Message
- **Complete when:** All eligible opportunities have been ranked using their validated weighted scores, supporting information has been preserved, and the ranked results are ready for T16.

## 4. Planned Tools

### Tool 1

- **Tool name:** rank_scored_opportunities
- **Input:** opportunity_scores
- **Output:** ranked_opportunities
- **Implementation Route:** Functions/scripts and database queries.
- **Integration approach:** Direct integration.
- **Role in this task:** Retrieves completed opportunity scores, sorts eligible businesses from highest to lowest score, assigns ranking positions, and preserves supporting evidence and uncertainties for the next task.
- **Task timeout:** 1 minute total per task run, including retries.
- **Maximum retries:** 1
- **Retry only when:** Temporary database connection failures, processing timeouts, or recoverable system errors occur. Wait 5 seconds before retrying. Do not retry invalid or missing scores automatically. Repeated attempts must not create duplicate ranking records.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure, affected opportunities, completed rankings, and attempted operations. Mark the task incomplete and send the case to T18: Handle Retrieval and Tool Exceptions. Do not forward incomplete rankings to T16 as completed results.
