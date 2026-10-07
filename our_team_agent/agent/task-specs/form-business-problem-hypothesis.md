# Form Business Problem Hypothesis Task Specification

## Basic Information

- **Task ID:** T10
- **Task name:** Form Business Problem Hypothesis
- **Task type:** Reason
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

AI interprets collected information and creates a list of client problems. This list will be saved as a separate PDF.

## 2. Inputs

### Input 1

- **Input name:** collected information
- **Contents and format:** One record per business with its observable signals, publicly listed contact details, and a source link for every item, with missing information flagged.
- **Source:** T09: Normalize and Deduplicate Records

- **If a required input is missing or invalid:** Stop, create no list, and send the case to T18: Handle Retrieval and Tool Exceptions.

## 3. Outputs

### Output 1

- **Output name:** list of client problems
- **Contents and format:** a list of client problems. This list will be saved as a separate PDF. Each problem names the business it applies to, the evidence for it, and the source links.
- **Next task or recipient:** T11: Match Hypothesis to Service
- **Complete when:** Every listed problem cites at least one source, and the PDF copy is saved and opens.

## 4. Planned Tools

### Tool 1

- **Tool name:** form_business_problem_hypothesis
- **Input:** collected information
- **Output:** list of client problems
- **Implementation Route:** functions/scripts
- **Integration approach:** direct integration
- **Role in this task:** AI interprets collected information and creates a list of client problems. This list will be saved as a separate PDF.
- **Task timeout:** 3 minutes
- **Maximum retries:** 2
- **Retry only when:** The call times out, the output has a problem with no evidence cited, or the PDF write fails. The PDF is named with the run ID, so a retry replaces the same file instead of creating a duplicate.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the status "failed" with the error and the attempts made, pass no output downstream, and send the case to T18: Handle Retrieval and Tool Exceptions.
