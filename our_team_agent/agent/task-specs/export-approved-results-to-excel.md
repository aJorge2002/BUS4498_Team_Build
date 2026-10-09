# Export approved Results to Excel Task Specification

## Basic Information

- **Task ID:** T21
- **Task name:** Export approved Results to Excel
- **Task type:** Act
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Exports approved consulting opportunities from T20 into a structured Excel spreadsheet for business outreach, research tracking, and potential presentations.

The spreadsheet organizes business information, identified problem hypotheses, recommended consulting services, opportunity scores, public contact information, and supporting sources.

Only approved results are exported. Missing information is clearly marked, and unverified hypotheses remain identified as potential problems.

The task does not change research findings, generate new scores, or contact businesses.

## 2. Inputs

### Input 1

- **Input name:** final_review_decision
- **Contents and format:** Record containing reviewed business identifiers, approval statuses, reviewer comments, and final decisions.
- **Source:** T20: Review and Approve Result

### Input 2

- **Input name:** approved_opportunity_records
- **Contents and format:** List or table containing business names, industries, locations, websites, opportunity rankings, weighted scores, identified problems, recommended services, contact information, supporting evidence, and source links.
- **Source:** T15: Rank Scored Opportunities; T16: Draft Brief and Outreach Message; T17: Check Required Fields and Resource Links

- **If a required input is missing or invalid:** Stop the affected export and identify the missing information. Return approval issues to T20 and incomplete records to their originating tasks. Send technical failures to T18: Handle Retrieval and Tool Exceptions. Do not export unapproved opportunities.

## 3. Outputs

### Output 1

- **Output name:** approved_opportunities_excel
- **Contents and format:** Excel workbook (.xlsx) containing approved business opportunities organized in a table with business name, industry, location, website, potential business problem, recommended consulting service, opportunity score, ranking, available business contacts, source links, and unresolved uncertainties.
- **Next task or recipient:** User / Team Gambit; saved to the designated output location.
- **Complete when:** The Excel workbook has been generated, saved successfully, checked for required fields and approval status, and made available to the user.

## 4. Planned Tools

### Tool 1

- **Tool name:** export_approved_results_to_excel
- **Input:** final_review_decision; approved_opportunity_records
- **Output:** approved_opportunities_excel
- **Implementation Route:** Functions/scripts and database queries.
- **Integration approach:** Direct integration.
- **Role in this task:** Retrieves approved consulting opportunity records, organizes the information into an Excel workbook, preserves supporting evidence and source links, and saves the completed file for user access.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 1
- **Retry only when:** Temporary database errors, file-generation failures, or recoverable system errors occur. Wait 5 seconds before retrying. Do not retry invalid records or missing approvals automatically. Use the same export identifier to prevent duplicate files.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure, affected opportunities, attempted operations, and any incomplete export files. Mark the task incomplete and send the case to T18: Handle Retrieval and Tool Exceptions. Do not present incomplete exports as successfully completed.
