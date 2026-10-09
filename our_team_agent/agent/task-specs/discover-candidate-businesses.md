# Discover Candidate Businesses Task Specification

## Basic Information

- **Task ID:** T05
- **Task name:** Discover Candidate Businesses
- **Task type:** Retrieve
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Executes supplied search queries using the user's industry, location, and research limits. Identifies potential client businesses and collects their names, locations, industries, websites, and supporting public sources. Does not analyze business problems or determine consulting opportunities.

## 2. Inputs

### Input 1

- **Input name:** queries
- **Contents and format:** List of search queries containing industry and location filters, consulting service relevance, and applicable research limits.
- **Source:** T04: Prepare Initial Search Queries; T06: Choose the Next Research Action

- **If a required input is missing or invalid:** Stop execution and return invalid queries to T04 for correction. If the issue is caused by a tool or retrieval failure, send the case to T18: Handle Retrieval and Tool Exceptions.

## 3. Outputs

### Output 1

- **Output name:** businesses and sources
- **Contents and format:** List or table containing candidate business names, industries or categories, locations, available websites, supporting source links, and search status. Record searches that return no results.
- **Next task or recipient:** T06: Choose the Next Research Action
- **Complete when:** Permitted queries have been executed within research limits, results and supporting sources have been recorded, and the search status is available to T06. Zero results is an acceptable completed outcome.

## 4. Planned Tools

### Tool 1

- **Tool name:** discover_candidate_businesses
- **Input:** queries
- **Output:** businesses and sources
- **Implementation Route:** Web API calls.
- **Integration approach:** Direct integration.
- **Role in this task:** Executes search queries using the user's industry and location filters. Retrieves matching business information and public source links, records search results, and returns candidate businesses for further research decisions.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 2
- **Retry only when:** A temporary network timeout, rate limit, or recoverable server error occurs. Wait 5 seconds or follow the API's required retry delay, whichever is longer. Do not retry invalid queries, unauthorized requests, or permanent errors. Avoid counting repeated results as new businesses.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure, affected queries, attempted requests, and any successfully retrieved results. Mark the task incomplete and send the case to T18: Handle Retrieval and Tool Exceptions. Do not pass incomplete results to T06 as a successful search.
