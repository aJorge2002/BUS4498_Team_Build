# Match Hypothesis to Service Task Specification

## Basic Information

- **Task ID:** T11
- **Task name:** Match Hypothesis to Service
- **Task type:** Reason
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Analyzes business problem hypotheses from T10 and compares them with the consulting services, skills, and experience identified in T01 and T02.

AI evaluates three criteria:

1. **Service fit:** Whether the consulting service addresses the suspected business problem.
2. **Consultant fit:** Whether the user has the relevant skills and experience to perform the service.
3. **Preliminary feasibility:** Whether the potential project appears realistic given its expected complexity, data requirements, and known constraints.

The task identifies suitable consulting opportunities, records uncertainties, and flags problems outside the user's capabilities.

It does not verify that the suspected business problem actually exists or that the business will provide the data needed for the project.

## 2. Inputs

### Input 1

- **Input name:** business_problem_hypotheses
- **Contents and format:** List or table containing suspected business problems, categories, supporting observations, source references, reasoning, and uncertainties.
- **Source:** T10: Form Business Problem Hypothesis

### Input 2

- **Input name:** consultant_services_and_capabilities
- **Contents and format:** Record containing consulting services, technical skills, professional experience, industry preferences, and relevant qualifications. Includes available information from the optional user profile.
- **Source:** T01: Define Goals and Consultant Services; T02: Scan Potential User Profile

- **If a required input is missing or invalid:** Record missing information and identify the affected hypothesis or consultant qualification. Return invalid business hypotheses to T10 for correction. Request missing consultant information from T01 when necessary. Send technical failures to T18: Handle Retrieval and Tool Exceptions. Do not assume missing capabilities or project resources exist.

## 3. Outputs

### Output 1

- **Output name:** service_match_assessments
- **Contents and format:** List or table containing the business identifier, original hypothesis, recommended consulting service, service fit, consultant fit, preliminary feasibility, supporting reasoning, missing requirements, and matching status. Statuses include matched, review required, insufficient information, and no match.
- **Next task or recipient:** T12: Check Support For Key Claims
- **Complete when:** Each hypothesis has been evaluated against available consulting services and capabilities, matching decisions and uncertainties have been recorded, and the assessment is ready for evidence verification. Unsupported matches must not be represented as confirmed opportunities.

## 4. Planned Tools

### Tool 1

- **Tool name:** match_hypothesis_to_service
- **Input:** business_problem_hypotheses; consultant_services_and_capabilities
- **Output:** service_match_assessments
- **Implementation Route:** Functions/scripts and web API calls for AI-supported matching.
- **Integration approach:** Direct integration.
- **Role in this task:** Compares suspected business problems with available consulting services and consultant capabilities. Evaluates service relevance, required qualifications, and preliminary project feasibility. Returns a documented matching assessment with uncertainties and supporting reasoning.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 2
- **Retry only when:** Temporary AI API failures, network timeouts, rate limits, or recoverable processing errors occur. Wait 5 seconds or follow the service's required retry delay, whichever is longer. Do not retry simply because a hypothesis has no suitable consulting service.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure, affected hypotheses, completed assessments, and attempted operations. Mark the task incomplete and send the case to T18: Handle Retrieval and Tool Exceptions. Do not pass incomplete matching results to T12 as successful assessments.
