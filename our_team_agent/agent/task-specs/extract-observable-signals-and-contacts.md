# Extract Observable Signals and Contacts Task Specification

## Basic Information

- **Task ID:** T08
- **Task name:** Extract Observable Signals and Contacts
- **Task type:** Sense
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Analyzes public business information retrieved in T07 to identify observable signals relevant to potential consulting opportunities.

Extracts information such as membership models, business locations, expansion announcements, service complaints, scheduling complaints, and outdated forms or systems.

Also identifies publicly available business contact information, including company email addresses, business phone numbers, contact pages, and relevant professional contacts.

Each extracted finding must be associated with its original source. The task records missing or uncertain information without assuming that a business problem exists.

## 2. Inputs

### Input 1

- **Input name:** retrieved_public_resources
- **Contents and format:** Collection of publicly available business information containing business names, source URLs, source types, retrieval dates, page content, and retrieval statuses.
- **Source:** T07: Retrieve Permitted Public Resources

- **If a required input is missing or invalid:** Record missing or unusable information. If the source must be retrieved again, return the request to T07. Send technical processing failures to T18: Handle Retrieval and Tool Exceptions. Do not invent missing information.

## 3. Outputs

### Output 1

- **Output name:** observable_business_signals
- **Contents and format:** List or table containing business name, observed signal, signal category, factual description, supporting source URL, observation date where available, and extraction status. Clearly identify uncertain or unsupported findings.
- **Next task or recipient:** T09: Normalize and Deduplicate Records
- **Complete when:** Available business information has been examined, relevant observable signals have been recorded with source references, and missing information has been identified.

### Output 2

- **Output name:** public_business_contacts
- **Contents and format:** List or table containing business name, publicly listed business email address, phone number, contact page, relevant professional contact if available, and supporting source URL. Missing contact information must be identified.
- **Next task or recipient:** T09: Normalize and Deduplicate Records
- **Complete when:** Relevant publicly available business contact information has been extracted, source references have been recorded, and unavailable contact fields have been marked as missing.

## 4. Planned Tools

### Tool 1

- **Tool name:** extract_observable_signals_and_contacts
- **Input:** retrieved_public_resources
- **Output:** observable_business_signals; public_business_contacts
- **Implementation Route:** Functions/scripts and web API calls for AI-supported extraction.
- **Integration approach:** Direct integration.
- **Role in this task:** Examines retrieved public business information, extracts observable business signals and permitted contact details, categorizes findings, and associates each finding with its supporting source. Records missing or uncertain information without generating unsupported conclusions.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 2
- **Retry only when:** Temporary API failures, processing timeouts, rate limits, or recoverable system errors occur. Wait 5 seconds or follow the service's required retry delay. Do not retry missing source information or restricted content automatically.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the affected businesses, unavailable information, processing attempts, and any successfully extracted findings. Mark the task incomplete and send the case to T18: Handle Retrieval and Tool Exceptions. Do not pass incomplete findings to T09 as verified results.
