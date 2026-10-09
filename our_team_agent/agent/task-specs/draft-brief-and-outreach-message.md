# Draft Brief and Outreach Message Task Specification

## Basic Information

- **Task ID:** T16
- **Task name:** Draft Brief and Outreach Message
- **Task type:** Act
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Creates a one-page consulting intelligence brief and personalized outreach message for selected business opportunities ranked in T15.

The brief summarizes the business, potential consulting value, identified connections, contact accessibility, business problem hypothesis, and preliminary project scope. It also identifies potential shareholders, sponsors, and relevant professional connections when supported by available information.

AI uses verified research findings, supporting sources, opportunity scores, and consultant capabilities to generate professional drafts.

The task distinguishes verified facts from hypotheses, does not invent missing information, and does not contact businesses. All drafts must undergo validation and human approval before external use.

## 2. Inputs

### Input 1

- **Input name:** ranked_opportunities
- **Contents and format:** Ranked list or table containing business identifiers, business names, opportunity scores, ranking positions, consulting services, and unresolved uncertainties.
- **Source:** T15: Rank Scored Opportunities

### Input 2

- **Input name:** verified_business_information
- **Contents and format:** Business information, public contact details, observable signals, supporting source links, verified claims, and unresolved findings.
- **Source:** T08: Extract Observable Signals and Contacts; T09: Normalize and Deduplicate Records; T12: Check Support For Key Claims

### Input 3

- **Input name:** consulting_opportunity_details
- **Contents and format:** Business problem hypotheses, recommended consulting services, consultant qualifications, preliminary project feasibility, potential value, and scoring explanations.
- **Source:** T10: Form Business Problem Hypothesis; T11: Match Hypothesis to Service; T14: Score the Opportunity

- **If a required input is missing or invalid:** Record missing information and request correction from the originating task. Clearly label unavailable optional information. If essential information or supporting evidence is missing, do not generate unsupported claims. Send technical processing failures to T18: Handle Retrieval and Tool Exceptions.

## 3. Outputs

### Output 1

- **Output name:** consulting_intelligence_brief
- **Contents and format:** One-page draft containing the business name, industry, location, business summary, potential consulting value, identified business problem hypothesis, supporting evidence and sources, recommended services, preliminary project scope, opportunity score, contact accessibility, potential shareholders, sponsors, relevant connections, and unresolved uncertainties.
- **Next task or recipient:** T17: Check Required Fields and Resource Links
- **Complete when:** A one-page draft has been prepared using available evidence, required sections are populated or explicitly marked as unavailable, and supporting sources are included.

### Output 2

- **Output name:** outreach_message_draft
- **Contents and format:** Personalized email or professional outreach message containing the recipient or business name, relevant business context, potential consulting value, brief introduction, and proposed next step. Include a source reference for factual claims used in the message.
- **Next task or recipient:** T17: Check Required Fields and Resource Links
- **Complete when:** A professional outreach draft has been generated, factual statements are traceable to available evidence, and the message is ready for validation and human review.

## 4. Planned Tools

### Tool 1

- **Tool name:** draft_brief_and_outreach_message
- **Input:** ranked_opportunities; verified_business_information; consulting_opportunity_details
- **Output:** consulting_intelligence_brief; outreach_message_draft
- **Implementation Route:** Functions/scripts and web API calls for AI-supported drafting.
- **Integration approach:** Direct integration.
- **Role in this task:** Analyzes ranked consulting opportunities and previously collected research to produce one-page intelligence briefs and personalized outreach drafts. Incorporates supporting evidence, recommended consulting services, potential project value, and relevant business contacts without inventing missing information or sending messages.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 2
- **Retry only when:** Temporary AI API failures, network timeouts, rate limits, or recoverable processing errors occur. Wait 5 seconds or follow the service's required retry delay, whichever is longer. Do not retry simply because information is unavailable. Prevent duplicate saved drafts when an attempt is repeated.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure, affected opportunities, attempted operations, and any completed drafts. Mark the task incomplete and send the case to T18: Handle Retrieval and Tool Exceptions. Do not forward incomplete drafts to T17 as completed deliverables.
