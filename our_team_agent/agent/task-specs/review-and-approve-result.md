# Review and Approve Result Task Specification

## Basic Information

- **Task ID:** T20
- **Task name:** Review and Approve Result
- **Task type:** Decide
- **Task owner:** User / Human Reviewer

## 1. Task Description

Allows the user to review Gambit's completed business research, consulting briefs, outreach drafts, and supporting evidence before final approval.

The user checks whether the findings are accurate, relevant, and aligned with their consulting goals.

The user may approve the results, reject an opportunity, request changes, or authorize additional research.

Only approved results proceed to T21 for Excel export. Outreach messages are not automatically sent.

## 2. Inputs

### Input 1

- **Input name:** validated_research_results
- **Contents and format:** Consulting briefs, outreach drafts, business information, opportunity rankings, supporting sources, and validation statuses.
- **Source:** T16: Draft Brief and Outreach Message; T17: Check Required Fields and Resource Links

### Input 2

- **Input name:** human_resolution_decision
- **Contents and format:** Previous human decisions, accepted hypotheses, research authorizations, and unresolved uncertainties when applicable.
- **Source:** T19: Resolve Uncertain Findings and Exceptions

- **If a required input is missing or invalid:** Request correction from the originating task. Keep the review pending until required information is available and deliverables have passed T17 validation. Do not approve incomplete or unvalidated results.

## 3. Outputs

### Output 1

- **Output name:** final_review_decision
- **Contents and format:** Record containing the reviewed business, approval status, reviewer comments, requested changes, unresolved concerns, and date of decision.
- **Next task or recipient:** T21: Export approved Results to Excel if approved; T16 for document revisions; T06 for authorized additional research. Rejected opportunities are recorded and closed.
- **Complete when:** The user has reviewed the results, selected a decision, and the decision has been recorded.

## 4. Planned Tools

### Tool 1

- **Tool name:** review_and_approve_result
- **Input:** validated_research_results; human_resolution_decision
- **Output:** final_review_decision
- **Implementation Route:** Functions/scripts and database queries.
- **Integration approach:** Direct integration.
- **Role in this task:** Displays completed research and consulting deliverables for human review. Records approvals, rejections, requested changes, and research authorizations. Routes approved results to T21 and sends other decisions to the appropriate tasks.
- **Task timeout:** Human response deadline of 2 business days after assignment.
- **Maximum retries:** Not applicable — manual task.
- **Retry only when:** Not applicable.
- **On timeout, exhausted retries, or an error that cannot be retried:** Preserve reviewed information, mark the case as pending, and notify Team Gambit. Do not export unapproved results. If a decision cannot be saved, request that the reviewer resubmit it after the issue is resolved.
