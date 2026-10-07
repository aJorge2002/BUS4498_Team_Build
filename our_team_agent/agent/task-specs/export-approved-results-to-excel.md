# Export approved Results to Excel Task Specification

## Basic Information

- **Task ID:** T21
- **Task name:** Export approved Results to Excel
- **Task type:** Act
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Analysis results are moved to excel for potential presentations.

## 2. Inputs

### Input 1

- **Input name:** approved Results
- **Contents and format:** Analysis results: the approved ranked opportunities, with each one's rank, business name, score, contact details, and source links.
- **Source:** T20: Review and Approve Result

- **If a required input is missing or invalid:** Stop, create no file, and send the case to T19: Resolve Uncertain Findings and Exceptions so the user knows nothing was exported.

## 3. Outputs

### Output 1

- **Output name:** excel
- **Contents and format:** excel for potential presentations. An Excel workbook with one row per approved opportunity: rank, business, score, contact details, and source links.
- **Next task or recipient:** User
- **Complete when:** Analysis results are moved to excel for potential presentations. The file opens and has one row for every approved opportunity.

## 4. Planned Tools

### Tool 1

- **Tool name:** export_approved_results_to_excel
- **Input:** approved Results
- **Output:** excel
- **Implementation Route:** file operations
- **Integration approach:** direct integration
- **Role in this task:** Analysis results are moved to excel for potential presentations.
- **Task timeout:** 1 minute
- **Maximum retries:** 2
- **Retry only when:** The file write fails, waiting 5 seconds between attempts. The file is named with the run ID, so a retry replaces the same file instead of creating a duplicate.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the status "export failed" with the error and the attempts made, create no partial file, and send the case to T19: Resolve Uncertain Findings and Exceptions.
