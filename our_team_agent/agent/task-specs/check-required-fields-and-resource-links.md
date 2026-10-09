# Check Required Fields and Resource Links Task Specification

## Basic Information

- **Task ID:** T17
- **Task name:** Check Required Fields and Resource Links
- **Task type:** Verify
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Validates consulting intelligence briefs and outreach messages created in T16 to ensure all required fields, supporting evidence, and resource links are present and correctly formatted.

The task checks that business information, problem hypotheses, recommended consulting services, opportunity scores, and contact details are consistent with previously collected and verified findings.

The task also checks that source links are correctly formatted and accessible where possible, and that factual claims reference appropriate supporting evidence.

Missing information, broken links, unsupported claims, or inconsistencies are flagged for correction. The task does not create new business information or independently revise research conclusions.

## 2. Inputs

### Input 1

- **Input name:** consulting_intelligence_brief
- **Contents and format:** One-page consulting brief containing business information, potential problems, recommended services, preliminary project scope, opportunity scores, supporting evidence, contact information, and source links.
- **Source:** T16: Draft Brief and Outreach Message

### Input 2

- **Input name:** outreach_message_draft
- **Contents and format:** Draft professional outreach message containing business context, relevant consulting services, proposed value, recipient information, and supporting references.
- **Source:** T16: Draft Brief and Outreach Message

### Input 3

- **Input name:** verified_research_and_service_matches
- **Contents and format:** Previously verified business claims, evidence statuses, source references, recommended consulting services, and identified uncertainties.
- **Source:** T11: Match Hypothesis to Service; T12: Check Support For Key Claims

- **If a required input is missing or invalid:** Record the missing or invalid information and identify the affected deliverable. Send incomplete or inconsistent results to T18: Handle Retrieval and Tool Exceptions for correction routing. Do not approve incomplete deliverables.

## 3. Outputs

### Output 1

- **Output name:** deliverable_validation_result
- **Contents and format:** Validation record containing the business identifier, required-field completion status, source-link status, evidence consistency results, identified errors, and overall validation status (passed or failed).
- **Next task or recipient:** T20: Review and Approve Result if validation passes; T18: Handle Retrieval and Tool Exceptions if validation fails.
- **Complete when:** Every required field, source reference, and factual claim has been checked against available research information, the validation result is recorded, and the appropriate next task is identified.

## 4. Planned Tools

### Tool 1

- **Tool name:** check_required_fields_and_resource_links
- **Input:** consulting_intelligence_brief; outreach_message_draft; verified_research_and_service_matches
- **Output:** deliverable_validation_result
- **Implementation Route:** Functions/scripts and web API calls.
- **Integration approach:** Direct integration.
- **Role in this task:** Examines generated consulting briefs and outreach drafts for required fields, correct formatting, usable source links, and consistency with verified research. Identifies missing information, unsupported statements, and inconsistencies before human approval.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 1
- **Retry only when:** Temporary network failures, source-link verification timeouts, rate limits, or recoverable processing errors occur. Wait 5 seconds or follow the required API delay. Do not retry missing fields or unsupported claims automatically.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure, affected documents, unavailable links, completed checks, and attempted operations. Mark the task incomplete and send the case to T18: Handle Retrieval and Tool Exceptions. Do not forward unvalidated deliverables to T20 as successfully verified.
