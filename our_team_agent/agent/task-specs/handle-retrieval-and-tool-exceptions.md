# Handle Retrieval and Tool Exceptions Task Specification

## Basic Information

- **Task ID:** T18
- **Task name:** Handle Retrieval and Tool Exceptions
- **Task type:** Act
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Review if all information is significant enough for potential. If too many issues arise, return to T12 or move to T19.

## 2. Inputs

### Input 1

- **Input name:** information
- **Contents and format:** An exception report with the ID of the task that failed, the error or failed check, the attempts made, and the list of issues (such as missing fields, broken links, or pages that could not be retrieved).
- **Source:** T05: Discover Candidate Businesses; T07: Retrieve Permitted Public Resources; T17: Check Required Fields and Resource Links

- **If a required input is missing or invalid:** Stop and send the case to T19: Resolve Uncertain Findings and Exceptions, because the failure cannot be assessed without a report.

## 3. Outputs

### Output 1

- **Output name:** Exceptions
- **Contents and format:** If too many issues arise, return to T12 or move to T19. A recorded decision of "recoverable" with the issues to recheck, or "too many issues" with the full issue list.
- **Next task or recipient:** T12: Check Support For Key Claims; T19: Resolve Uncertain Findings and Exceptions
- **Complete when:** A decision is recorded with the reason and the issue list.

## 4. Planned Tools

### Tool 1

- **Tool name:** handle_retrieval_and_tool_exceptions
- **Input:** information
- **Output:** Exceptions
- **Implementation Route:** functions/scripts
- **Integration approach:** direct integration
- **Role in this task:** Review if all information is significant enough for potential. If too many issues arise, return to T12 or move to T19. Applies a fixed rule: a small number of recoverable issues (for example, a missing field or one broken link) goes back to T12, and anything else goes to the user.
- **Task timeout:** 30 seconds
- **Maximum retries:** 1
- **Retry only when:** The script fails unexpectedly. The rule changes no records, so a retry cannot duplicate anything.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the status "exception routing failed" and send the case to T19: Resolve Uncertain Findings and Exceptions. Do not continue as if the exceptions were resolved.
