# Extract Observable Signals and Contacts Task Specification

## Basic Information

- **Task ID:** T08
- **Task name:** Extract Observable Signals and Contacts
- **Task type:** Sense
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

AI extracts memberships, models, locations, expansion plans, service complaints, scheduling complaints, and outdated forms. Marks missing information. Sources are also outputted.

## 2. Inputs

### Input 1

- **Input name:** Public Resources
- **Contents and format:** websites, service pages, landing pages, reviews, listings, and job postings. Page text with the source URL and retrieval time for each page.
- **Source:** T07: Retrieve Permitted Public Resources

- **If a required input is missing or invalid:** Stop, extract nothing, and send the case to T18: Handle Retrieval and Tool Exceptions.

## 3. Outputs

### Output 1

- **Output name:** Observable Signals and Contacts
- **Contents and format:** memberships, models, locations, expansion plans, service complaints, scheduling complaints, and outdated forms, plus publicly listed contact details. One record per business, with a source URL for every item and a flag on every field that could not be found.
- **Next task or recipient:** T09: Normalize and Deduplicate Records
- **Complete when:** Sources are also outputted. Every extracted item has a source URL, and missing information is flagged rather than left blank.

## 4. Planned Tools

### Tool 1

- **Tool name:** extract_observable_signals_and_contacts
- **Input:** Public Resources
- **Output:** Observable Signals and Contacts
- **Implementation Route:** functions/scripts
- **Integration approach:** direct integration
- **Role in this task:** AI extracts memberships, models, locations, expansion plans, service complaints, scheduling complaints, and outdated forms. Marks missing information. Sources are also outputted.
- **Task timeout:** 2 minutes
- **Maximum retries:** 2
- **Retry only when:** The call times out or the output does not match the expected record structure. Nothing is saved until the output is valid, so a retry cannot create duplicate records.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the status "failed" with the error and the attempts made, pass no output downstream, and send the case to T18: Handle Retrieval and Tool Exceptions.
