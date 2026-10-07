# Check Support For Key Claims Task Specification

## Basic Information

- **Task ID:** T12
- **Task name:** Check Support For Key Claims
- **Task type:** Verify
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

AI compares claims with missing, invalid, or inconsistent information. This step’s collected information is saved for the next research decision.

## 2. Inputs

### Input 1

- **Input name:** claims
- **Contents and format:** missing, invalid, or inconsistent information
- **Source:** T11: Match Hypothesis to Service

- **If a required input is missing or invalid:** If either input is missing, stop and send the case to T18: Handle Retrieval and Tool Exceptions.

## 3. Outputs

### Output 1

- **Output name:** collected information
- **Contents and format:** missing, invalid, or inconsistent information
- **Next task or recipient:** T13: Decide Whether to Investigate Further
- **Complete when:** This step’s collected information is saved for the next research decision.

## 4. Planned Tools

### Tool 1

- **Tool name:** check_support_for_key_claims
- **Input:** claims
- **Output:** collected information
- **Implementation Route:** functions/scripts
- **Integration approach:** direct integration
- **Role in this task:** AI compares claims with missing, invalid, or inconsistent information. This step’s collected information is saved for the next research decision.
- **Task timeout:** 3 minutes
- **Maximum retries:** 2
- **Retry only when:** Only on a timeout or output that does not cover every claim. The check is read-only, so retries cannot duplicate anything.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the status 'failed' with the error and the attempts made, pass no output downstream, and send the case to T18: Handle Retrieval and Tool Exceptions.
