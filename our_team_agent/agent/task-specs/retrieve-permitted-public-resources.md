# Retrieve Permitted Public Resources Task Specification

## Basic Information

- **Task ID:** T07
- **Task name:** Retrieve Permitted Public Resources
- **Task type:** Retrieve
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Retrieves publicly available information about candidate businesses selected for further investigation in T06.

The task collects relevant business websites, service pages, landing pages, public reviews, business listings, and job postings.

Research must remain within the user's approved industry, location, and research limits. The task does not bypass website restrictions, access private information, contact businesses, or form business problem hypotheses.

## 2. Inputs

### Input 1

- **Input name:** next_research_action
- **Contents and format:** Research instructions identifying the target business, relevant website or public source, research objective, and applicable research limits.
- **Source:** T06: Choose the Next Research Action

### Input 2

- **Input name:** businesses and sources
- **Contents and format:** List or table containing candidate business names, locations, industries, available websites, and supporting source links.
- **Source:** T05: Discover Candidate Businesses

- **If a required input is missing or invalid:** Stop retrieval and record the missing or invalid information. Return incorrect research instructions to T06 for correction. Send technical retrieval failures to T18: Handle Retrieval and Tool Exceptions.

## 3. Outputs

### Output 1

- **Output name:** retrieved_public_resources
- **Contents and format:** Collection of retrieved public information containing the business name, source URL, source type, retrieval date, relevant page content, and retrieval status. Record unavailable or inaccessible resources without inventing missing information.
- **Next task or recipient:** T08: Extract Observable Signals and Contacts
- **Complete when:** Permitted public resources have been retrieved or their unavailability documented, source references have been recorded, and the results are ready for T08.

## 4. Planned Tools

### Tool 1

- **Tool name:** retrieve_permitted_public_resources
- **Input:** next_research_action; businesses and sources
- **Output:** retrieved_public_resources
- **Implementation Route:** Web API calls and functions/scripts.
- **Integration approach:** Direct integration.
- **Role in this task:** Retrieves approved public business information from websites, directories, review platforms, and other permitted sources. Records relevant page content, source URLs, retrieval timestamps, and retrieval statuses for subsequent evidence extraction.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 2
- **Retry only when:** Temporary network errors, request timeouts, rate limits, or recoverable server failures occur. Wait 5 seconds or follow the source's required retry delay, whichever is longer. Do not retry restricted pages, denied access, or permanent errors.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the affected source, error type, attempts made, and any successfully retrieved information. Mark the affected retrieval as incomplete and send the technical failure to T18: Handle Retrieval and Tool Exceptions. Do not treat missing information as verified evidence.
