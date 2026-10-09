# Prepare Initial Search Queries Task Specification

## Basic Information

- **Task ID:** T04
- **Task name:** Prepare Initial Search Queries
- **Task type:** Reason
- **Task owner:** AI Agent

## 1. Task Description

Translates validated user preferences into relevant search queries for discovering potential business clients. Uses industry, location, consulting services, and research limits to prepare targeted queries. Does not execute searches or determine subsequent research actions.

## 2. Inputs

### Input 1

- **Input name:** validated_search_preferences
- **Contents and format:** Validated record containing target industries, locations, consulting services, and research limits.
- **Source:** T03: Validate Required Inputs

- **If a required input is missing or invalid:** Stop query preparation and return to T03 for validation. Do not generate queries using incomplete or invalid information.

## 3. Outputs

### Output 1

- **Output name:** initial_search_queries
- **Contents and format:** List of relevant search queries with associated industry and location filters, consulting service relevance, and applicable research limits.
- **Next task or recipient:** T05: Discover Candidate Businesses
- **Complete when:** A nonempty list of relevant, nonduplicate queries is prepared, checked against the user's research scope, and passed to T05.

## 4. Planned Tools

### Tool 1

- **Tool name:** prepare_initial_search_queries
- **Input:** validated_search_preferences
- **Output:** initial_search_queries
- **Implementation Route:** Functions/scripts and web API calls if using an AI model.
- **Integration approach:** Direct integration.
- **Role in this task:** Converts validated industries, locations, consulting services, and research limits into targeted search queries for T05 without executing searches.
- **Task timeout:** 60 seconds total per task run, including retries.
- **Maximum retries:** 2
- **Retry only when:** Temporary API failures, network timeouts, or recoverable processing errors. Wait briefly before retrying. Do not retry invalid inputs.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure and any successfully prepared queries, mark the task incomplete, and route to T18: Handle Retrieval and Tool Exceptions. Do not proceed to T05 as though query preparation succeeded.# Prepare Initial Search Queries Task Specification

## Basic Information

- **Task ID:** T04
- **Task name:** Prepare Initial Search Queries
- **Task type:** Reason
- **Task owner:** AI Agent

## 1. Task Description

Translates validated user preferences into relevant search queries for discovering potential business clients. Uses industry, location, consulting services, and research limits to prepare targeted queries. Does not execute searches or determine subsequent research actions.

## 2. Inputs

### Input 1

- **Input name:** validated_search_preferences
- **Contents and format:** Validated record containing target industries, locations, consulting services, and research limits.
- **Source:** T03: Validate Required Inputs

- **If a required input is missing or invalid:** Stop query preparation and return to T03 for validation. Do not generate queries using incomplete or invalid information.

## 3. Outputs

### Output 1

- **Output name:** initial_search_queries
- **Contents and format:** List of relevant search queries with associated industry and location filters, consulting service relevance, and applicable research limits.
- **Next task or recipient:** T05: Discover Candidate Businesses
- **Complete when:** A nonempty list of relevant, nonduplicate queries is prepared, checked against the user's research scope, and passed to T05.

## 4. Planned Tools

### Tool 1

- **Tool name:** prepare_initial_search_queries
- **Input:** validated_search_preferences
- **Output:** initial_search_queries
- **Implementation Route:** Functions/scripts and web API calls if using an AI model.
- **Integration approach:** Direct integration.
- **Role in this task:** Converts validated industries, locations, consulting services, and research limits into targeted search queries for T05 without executing searches.
- **Task timeout:** 60 seconds total per task run, including retries.
- **Maximum retries:** 2
- **Retry only when:** Temporary API failures, network timeouts, or recoverable processing errors. Wait briefly before retrying. Do not retry invalid inputs.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure and any successfully prepared queries, mark the task incomplete, and route to T18: Handle Retrieval and Tool Exceptions. Do not proceed to T05 as though query preparation succeeded.
