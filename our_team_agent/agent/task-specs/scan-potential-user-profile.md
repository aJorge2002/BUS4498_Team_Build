# Scan Potential User Profile Task Specification

## Basic Information

- **Task ID:** T02
- **Task name:** Scan Potential User Profile
- **Task type:** Reason
- **Task owner:** AI Agent

## 1. Task Description

AI evaluates an existing profile. This information may include criteria such as the user’s resume, experience, and preferred industries, GitHub, LinkedIn, school affiliation, and portfolio. Missing or incorrect entries are identified. 

## 2. Inputs

### Input 1

- **Input name:** consultant_profile
- **Contents and format:** The user’s resume, experience, and preferred industries, GitHub, LinkedIn, school affiliation, and portfolio.
- **Source:** T01: Define Goals and Consultant Services

- **If a required input is missing or invalid:** If no profile exists, agent proceeds to T03. If there is an error, issue is recorded. 

## 3. Outputs

### Output 1

- **Output name:** analyzed_consultant_profile
- **Contents and format:**
- **Next task or recipient:** T03: Validate Required Inputs
- **Complete when:** Information has been analyzed., relevant skills are gathered., output is saved successfully. 

## 4. Planned Tools

### Tool 1

- **Tool name:** scan_potential_user_profile
- **Input:** consultant_profile
- **Output:** analyzed_consultant_profile
- **Implementation Route:** Database queries, file operations, and web API calls
- **Integration approach:** Direct integration 
- **Role in this task:** If the user has a profile, AI will evaluate it. This information may include criteria such as the user’s resume, experience, and preferred industries, GitHub, LinkedIn, school affiliation, and portfolio.
- **Task timeout:** 60 seconds
- **Maximum retries:** 2 retries
- **Retry only when:** Temporary API failures, rate limits, or network timeouts
- **On timeout, exhausted retries, or an error that cannot be retried:** Preserve available information. Diagnose and record the error. Mark the analysis as incomplete and proceed to T03
