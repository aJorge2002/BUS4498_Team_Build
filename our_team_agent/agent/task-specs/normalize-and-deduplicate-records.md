# Normalize and Deduplicate Records Task Specification

## Basic Information

- **Task ID:** T09
- **Task name:** Normalize and Deduplicate Records
- **Task type:** Act
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Standardizes business records, observable signals, and contact information collected from previous tasks into a consistent format.

Identifies and merges duplicate business records using business names, websites, locations, and other available identifying information.

Preserves all supporting source links, extracted signals, and contact details when merging records. Uncertain matches are flagged for review rather than automatically combined.

The task does not generate new business hypotheses or alter the meaning of collected evidence.

## 2. Inputs

### Input 1

- **Input name:** businesses and sources
- **Contents and format:** List or table containing candidate business names, industries, locations, websites, and supporting public sources.
- **Source:** T05: Discover Candidate Businesses

### Input 2

- **Input name:** observable_business_signals
- **Contents and format:** List or table containing business names, observed signals, categories, descriptions, observation dates, and supporting source links.
- **Source:** T08: Extract Observable Signals and Contacts

### Input 3

- **Input name:** public_business_contacts
- **Contents and format:** List or table containing business names, public contact details, contact pages, and supporting source links.
- **Source:** T08: Extract Observable Signals and Contacts

- **If a required input is missing or invalid:** Record missing or inconsistent information and identify the affected records. Return incomplete extraction results to T08 where correction is possible. Send technical processing failures to T18: Handle Retrieval and Tool Exceptions. Do not merge records when their identities cannot be reliably established.

## 3. Outputs

### Output 1

- **Output name:** normalized_business_records
- **Contents and format:** Standardized list or table containing unique business identifiers, business names, industries, locations, websites, observable signals, public contact information, and all supporting source references. Include duplicate-resolution status and unresolved identity conflicts.
- **Next task or recipient:** T10: Form Business Problem Hypothesis
- **Complete when:** Business records have been standardized, identifiable duplicates have been merged without losing evidence, uncertain matches have been flagged, and the results are ready for T10.

## 4. Planned Tools

### Tool 1

- **Tool name:** normalize_and_deduplicate_records
- **Input:** businesses and sources; observable_business_signals; public_business_contacts
- **Output:** normalized_business_records
- **Implementation Route:** Functions/scripts and database queries.
- **Integration approach:** Direct integration.
- **Role in this task:** Standardizes business names, locations, websites, signals, and contact information. Compares identifying fields to detect duplicates, merges confirmed duplicate records, preserves source references, and flags uncertain matches for review.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 1
- **Retry only when:** Temporary database connection failures, processing timeouts, or recoverable system errors occur. Wait 5 seconds before retrying. Repeated operations must not create duplicate records or overwrite existing evidence.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure, affected records, attempted operations, and any successfully processed information. Mark the task incomplete and route the case to T18: Handle Retrieval and Tool Exceptions. Preserve original records and do not send unverified merged records to T10.
