# Draft Brief and Outreach Message Task Specification

## Basic Information

- **Task ID:** T16
- **Task name:** Draft Brief and Outreach Message
- **Task type:** Reason
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Agent creates one page brief with all information collected. Information on draft consists of a summary, potential value, connections, contact ease, hypothesis, project scope, potential shareholders, potential sponsors, and potential connections.

## 2. Inputs

### Input 1

- **Input name:** all information collected
- **Contents and format:** Ranked list of opportunities with each opportunity's score and rank, plus the supporting evidence for each: business record, contacts, hypothesis, matched service, and source links.
- **Source:** T15: Rank Scored Opportunities

- **If a required input is missing or invalid:** Stop, create no draft, and send the case to T18: Handle Retrieval and Tool Exceptions.

## 3. Outputs

### Output 1

- **Output name:** one page brief
- **Contents and format:** a summary, potential value, connections, contact ease, hypothesis, project scope, potential shareholders, potential sponsors, and potential connections.
- **Next task or recipient:** T17: Check Required Fields and Resource Links
- **Complete when:** Every section of the brief is filled and each claim in it links to a source.

## 4. Planned Tools

### Tool 1

- **Tool name:** draft_brief_and_outreach_message
- **Input:** all information collected
- **Output:** one page brief
- **Implementation Route:** functions/scripts
- **Integration approach:** direct integration
- **Role in this task:** Agent creates one page brief with all information collected. Information on draft consists of a summary, potential value, connections, contact ease, hypothesis, project scope, potential shareholders, potential sponsors, and potential connections.
- **Task timeout:** 3 minutes
- **Maximum retries:** 2
- **Retry only when:** The call times out or the draft is missing a required section. Drafts are only saved, never sent, and each is saved under the run ID, so a retry cannot duplicate anything.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the status "failed" with the error and the attempts made, pass no output downstream, and send the case to T18: Handle Retrieval and Tool Exceptions.
