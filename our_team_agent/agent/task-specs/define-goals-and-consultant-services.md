# Define Goals and Consultant Services Task Specification

## Basic Information

- **Task ID:** T01
- **Task name:** Define Goals and Consultant Services
- **Task type:** Act
- **Task owner:** User

## 1. Task Description

User inputs industry, location, services, and research limits. This is used to specify the target audience and business goals. If the user has created a profile, the agent will scan through the user’s data in T02. Otherwise, the agent jumps to T03

## 2. Inputs

### Input 1

- **Input name:** consultant_search_preferences // Industry, location, services, and research limits
- **Contents and format:** industry, location, services, and research limits
- **Source:** User

- **If a required input is missing or invalid:** The task stays open with the user until every required field is submitted. No downstream task starts.

## 3. Outputs

### Output 1

- **Output name:** consultant_search_profile // Target audience and business goals
- **Contents and format:** target audience and business goals
- **Next task or recipient:** T02: Scan Potential User Profile; T03: Validate Required Inputs
- **Complete when:** All required fields are submitted and saved.

## 4. Planned Tools

- **Task timeout:** Not applicable - user-driven data
- **Maximum retries:** Not applicable — manual task.
- **Retry only when:** Not applicable
- **On timeout, exhausted retries, or an error that cannot be retried:** Keep submitted inputs where possible, notify the user there has been an error. Do not move to next step unless issue is resolved.
