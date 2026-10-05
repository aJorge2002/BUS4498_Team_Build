# Scan Potential User Profile Task Specification

## Basic Information

- **Task ID:** T02
- **Task name:** Scan Potential User Profile
- **Task type:** Reason
- **Task owner:**

## 1. Task Description

If the user has a profile, AI will evaluate it. This information may include criteria such as the user’s resume, experience, and preferred industries, GitHub, LinkedIn, school affiliation, and portfolio.

## 2. Inputs

### Input 1

- **Input name:** profile
- **Contents and format:** the user’s resume, experience, and preferred industries, GitHub, LinkedIn, school affiliation, and portfolio.
- **Source:** T01: Define Goals and Consultant Services

- **If a required input is missing or invalid:**

## 3. Outputs

### Output 1

- **Output name:** profile
- **Contents and format:**
- **Next task or recipient:** T03: Validate Required Inputs
- **Complete when:**

## 4. Planned Tools

### Tool 1

- **Tool name:** scan_potential_user_profile
- **Input:** profile
- **Output:** profile
- **Implementation Route:**
- **Integration approach:**
- **Role in this task:** If the user has a profile, AI will evaluate it. This information may include criteria such as the user’s resume, experience, and preferred industries, GitHub, LinkedIn, school affiliation, and portfolio.
- **Task timeout:**
- **Maximum retries:**
- **Retry only when:**
- **On timeout, exhausted retries, or an error that cannot be retried:**
