# Check Required Fields and Resource Links Task Specification

## Basic Information

- **Task ID:** T17
- **Task name:** Check Required Fields and Resource Links
- **Task type:** Verify
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Verify structure and evidence. Using information from T11.

## 2. Inputs

### Input 1

- **Input name:** information from T11
- **Contents and format:** structure and evidence
- **Source:** T11: Match Hypothesis to Service; T16: Draft Brief and Outreach Message

- **If a required input is missing or invalid:**

## 3. Outputs

### Output 1

- **Output name:** Required Fields and Resource Links
- **Contents and format:** Pass or fail, with a list of missing sections and broken or unsupported links.
- **Next task or recipient:** T18: Handle Retrieval and Tool Exceptions; T20: Review and Approve Result
- **Complete when:** A pass or fail status is recorded with every issue listed.

## 4. Planned Tools

### Tool 1

- **Tool name:** check_required_fields_and_resource_links
- **Input:** information from T11
- **Output:** Required Fields and Resource Links
- **Implementation Route:** functions/scripts
- **Integration approach:** direct integration
- **Role in this task:** Verify structure and evidence. Using information from T11.
- **Task timeout:** 2 minutes
- **Maximum retries:** 2
- **Retry only when:** Only when a link request times out, waiting 5 seconds between attempts. The checks are read-only, so retries cannot duplicate anything.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the status 'check failed' with the error and send the case to T18: Handle Retrieval and Tool Exceptions.
