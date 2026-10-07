# Discover Candidate Businesses Task Specification

## Basic Information

- **Task ID:** T05
- **Task name:** Discover Candidate Businesses
- **Task type:** Retrieve
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Execute supplied queries with correct industry and location filters. Returns businesses and sources.

## 2. Inputs

### Input 1

- **Input name:** queries
- **Contents and format:** supplied queries with correct industry and location filters
- **Source:** T04: Prepare Initial Search Queries; T06: Choose the Next Research Action

- **If a required input is missing or invalid:** Stop, return no businesses, and send the case to T18: Handle Retrieval and Tool Exceptions.

## 3. Outputs

### Output 1

- **Output name:** businesses and sources
- **Contents and format:** businesses and sources
- **Next task or recipient:** T06: Choose the Next Research Action
- **Complete when:** Returns businesses and sources.

## 4. Planned Tools

### Tool 1

- **Tool name:** discover_candidate_businesses
- **Input:** queries
- **Output:** businesses and sources
- **Implementation Route:** web API calls
- **Integration approach:** direct integration
- **Role in this task:** Execute supplied queries with correct industry and location filters. Returns businesses and sources.
- **Task timeout:** 2 minutes
- **Maximum retries:** 2
- **Retry only when:** The call times out, is rate-limited, or returns a temporary server error, waiting 5 seconds between attempts. Searching is read-only, so a retry cannot duplicate anything.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the status "failed" with the error and the attempts made, pass no output downstream, and send the case to T18: Handle Retrieval and Tool Exceptions.
