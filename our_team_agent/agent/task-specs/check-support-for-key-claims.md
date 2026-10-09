# Check Support For Key Claims Task Specification

## Basic Information

- **Task ID:** T12
- **Task name:** Check Support For Key Claims
- **Task type:** Verify
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Evaluates business problem hypotheses and service match assessments to determine whether their key factual claims are supported by reliable, traceable evidence.

AI compares each claim with the original source material, checks for missing or inconsistent information, and identifies unsupported conclusions.

Claims are classified as supported, partially supported, contradicted, or insufficient evidence.

The task distinguishes verified business observations from unconfirmed business problem hypotheses. It does not assume that a suspected problem exists simply because a consulting service could address it.

Findings are recorded for T13 to determine whether additional research is necessary.

## 2. Inputs

### Input 1

- **Input name:** service_match_assessments
- **Contents and format:** List or table containing business identifiers, problem hypotheses, recommended consulting services, matching assessments, supporting reasoning, and unresolved questions.
- **Source:** T11: Match Hypothesis to Service

### Input 2

- **Input name:** business_evidence_and_sources
- **Contents and format:** Business observations, original source links, available source content, retrieval dates, and supporting evidence associated with each hypothesis.
- **Source:** T07: Retrieve Permitted Public Resources; T08: Extract Observable Signals and Contacts; T09: Normalize and Deduplicate Records; T10: Form Business Problem Hypothesis

- **If a required input is missing or invalid:** Record the affected claims and identify the missing or invalid evidence. Mark claims that cannot be checked as insufficient evidence. Send technical processing failures to T18: Handle Retrieval and Tool Exceptions. Do not classify unverifiable claims as supported.

## 3. Outputs

### Output 1

- **Output name:** claim_verification_results
- **Contents and format:** List or table containing business identifier, claim, supporting source references, verification status, evidence summary, identified contradictions, missing information, and unresolved research questions.
- **Next task or recipient:** T13: Decide Whether to Investigate Further
- **Complete when:** Every key claim has been evaluated against available evidence, its verification status has been recorded, and unresolved issues have been documented for T13.

## 4. Planned Tools

### Tool 1

- **Tool name:** check_support_for_key_claims
- **Input:** service_match_assessments; business_evidence_and_sources
- **Output:** claim_verification_results
- **Implementation Route:** Functions/scripts and web API calls for AI-supported evidence assessment.
- **Integration approach:** Direct integration.
- **Role in this task:** Compares factual claims and business hypotheses against retrieved source material. Identifies supporting evidence, contradictions, missing information, and unsupported conclusions. Returns documented verification results for subsequent research decisions.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 2
- **Retry only when:** Temporary API failures, network timeouts, rate limits, or recoverable processing errors occur. Wait 5 seconds or follow the service's required retry delay, whichever is longer. Do not retry merely because evidence is insufficient or contradictory.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure, affected claims, available evidence, and completed verification results. Mark the task incomplete and send the case to T18: Handle Retrieval and Tool Exceptions. Do not treat unchecked claims as verified.
