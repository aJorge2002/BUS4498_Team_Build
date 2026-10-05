# Extract Observable Signals and Contacts Task Specification

## Basic Information

- **Task ID:** T08
- **Task name:** Extract Observable Signals and Contacts
- **Task type:** Sense
- **Task owner:**

## 1. Task Description

AI extracts memberships, models, locations, expansion plans, service complaints, scheduling complaints, and outdated forms. Marks missing information. Sources are also outputted.

## 2. Inputs

### Input 1

- **Input name:** Public Resources
- **Contents and format:** websites, service pages, landing pages, reviews, listings, and job postings.
- **Source:** T07: Retrieve Permitted Public Resources

- **If a required input is missing or invalid:**

## 3. Outputs

### Output 1

- **Output name:** Observable Signals and Contacts
- **Contents and format:** memberships, models, locations, expansion plans, service complaints, scheduling complaints, and outdated forms.
- **Next task or recipient:** T09: Normalize and Deduplicate Records
- **Complete when:** Sources are also outputted.

## 4. Planned Tools

### Tool 1

- **Tool name:** extract_observable_signals_and_contacts
- **Input:** Public Resources
- **Output:** Observable Signals and Contacts
- **Implementation Route:**
- **Integration approach:**
- **Role in this task:** AI extracts memberships, models, locations, expansion plans, service complaints, scheduling complaints, and outdated forms. Marks missing information. Sources are also outputted.
- **Task timeout:**
- **Maximum retries:**
- **Retry only when:**
- **On timeout, exhausted retries, or an error that cannot be retried:**
