# Score the Opportunity Task Specification

## Basic Information

- **Task ID:** T14
- **Task name:** Score the Opportunity
- **Task type:** Reason
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Evaluates potential consulting opportunities using a predefined weighted scoring model based on five criteria:

1. **Likely Need:** Evidence indicating the business may benefit from consulting services.
2. **Potential Value:** Estimated significance of the opportunity to the business.
3. **Connection Potential:** Available professional, institutional, or organizational connections that may facilitate engagement.
4. **Contact Ease:** Availability and accessibility of verified business contact information.
5. **Consultant Fit:** Alignment between the business problem and the consultant's services, skills, and experience.

AI evaluates each criterion using available business findings, verified evidence, and service match assessments. The task applies predefined scoring rules and weights to calculate an overall opportunity score.

Missing or uncertain information must be identified. The task does not invent business performance figures or treat suspected problems as confirmed.

## 2. Inputs

### Input 1

- **Input name:** research_decision
- **Contents and format:** Record containing business identifier, evidence sufficiency decision, supporting reasoning, and unresolved issues.
- **Source:** T13: Decide Whether to Investigate Further

### Input 2

- **Input name:** service_match_assessments
- **Contents and format:** Business problem hypotheses, recommended consulting services, consultant fit assessments, preliminary feasibility, and supporting reasoning.
- **Source:** T11: Match Hypothesis to Service

### Input 3

- **Input name:** verified_business_information
- **Contents and format:** Business identifiers, verified observations, supporting sources, public contact information, relevant connections, evidence quality, and unresolved claims.
- **Source:** T08: Extract Observable Signals and Contacts; T09: Normalize and Deduplicate Records; T12: Check Support For Key Claims

### Input 4

- **Input name:** opportunity_scoring_criteria
- **Contents and format:** Predefined scoring criteria, scoring scales, weights, and rules for handling missing information.
- **Source:** Team Gambit's approved scoring model and workflow configuration.

- **If a required input is missing or invalid:** Record the missing or invalid information and request correction from the originating task. If scoring criteria or weights are unavailable, stop and refer the case to Team Gambit. Do not calculate scores using invented information or unapproved weights.

## 3. Outputs

### Output 1

- **Output name:** opportunity_scores
- **Contents and format:** List or table containing business identifier, scores for likely need, potential value, connection potential, contact ease, and consultant fit; applicable weights; overall weighted score; supporting evidence; missing information; and scoring status.
- **Next task or recipient:** T15: Rank Scored Opportunities
- **Complete when:** Each eligible opportunity has been evaluated using the approved scoring criteria, scores and supporting evidence have been recorded, and completed assessments are ready for ranking.

## 4. Planned Tools

### Tool 1

- **Tool name:** score_the_opportunity
- **Input:** research_decision; service_match_assessments; verified_business_information; opportunity_scoring_criteria
- **Output:** opportunity_scores
- **Implementation Route:** Functions/scripts and web API calls for AI-supported evaluation.
- **Integration approach:** Direct integration.
- **Role in this task:** Evaluates each consulting opportunity against predefined scoring criteria, assigns evidence-based criterion scores, applies approved weights, and calculates an overall opportunity score. Returns scoring results with supporting evidence and uncertainty indicators.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 1
- **Retry only when:** Temporary API failures, processing timeouts, or recoverable system errors occur. Wait 5 seconds or follow the service's required retry delay. Do not retry simply because an opportunity receives a low score. Repeated attempts must not create duplicate scoring records.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure, affected opportunities, completed assessments, and attempted operations. Mark the task incomplete and send the case to T18: Handle Retrieval and Tool Exceptions. Do not forward incomplete scoring results to T15 as successfully scored opportunities.
