# Form Business Problem Hypothesis Task Specification

## Basic Information

- **Task ID:** T10
- **Task name:** Form Business Problem Hypothesis
- **Task type:** Reason
- **Task owner:** Team Gambit (Adrian Jorge and Pedro Calvillo)

## 1. Task Description

Analyzes normalized business records and observable signals to identify potential business problems that could benefit from consulting services.

AI evaluates evidence such as customer complaints, expansion activity, operational challenges, business models, and publicly available performance indicators to develop reasonable business problem hypotheses.

Each hypothesis must include supporting evidence, source references, an explanation of the suspected problem, and any important uncertainties.

The task distinguishes confirmed observations from possible business problems. It does not assume that a business has a problem without sufficient supporting information.

## 2. Inputs

### Input 1

- **Input name:** normalized_business_records
- **Contents and format:** List or table containing unique businesses, industries, locations, observable signals, public contact information, and supporting source references.
- **Source:** T09: Normalize and Deduplicate Records

- **If a required input is missing or invalid:** Record missing or inconsistent information and return affected records to T09 for correction. If evidence is insufficient to form a reasonable hypothesis, mark the business as having insufficient evidence rather than inventing a problem. Send technical failures to T18: Handle Retrieval and Tool Exceptions.

## 3. Outputs

### Output 1

- **Output name:** business_problem_hypotheses
- **Contents and format:** List or table containing business identifier, suspected business problem, problem category, supporting observations, source links, reasoning, uncertainties, and preliminary confidence level. Clearly distinguish hypotheses from verified findings.
- **Next task or recipient:** T11: Match Hypothesis to Service
- **Complete when:** Each evaluated business has a documented hypothesis supported by traceable evidence or an explicit insufficient-evidence status. Only supported hypotheses are forwarded for service matching.

## 4. Planned Tools

### Tool 1

- **Tool name:** form_business_problem_hypothesis
- **Input:** normalized_business_records
- **Output:** business_problem_hypotheses
- **Implementation Route:** Functions/scripts and web API calls for AI-supported reasoning.
- **Integration approach:** Direct integration.
- **Role in this task:** Analyzes normalized business information, interprets observable signals, identifies plausible business problems, and generates hypotheses with supporting evidence, source references, and uncertainty indicators.
- **Task timeout:** 2 minutes total per task run, including retries.
- **Maximum retries:** 2
- **Retry only when:** Temporary API failures, network timeouts, rate limits, or recoverable processing errors occur. Wait 5 seconds or follow the service's required retry delay, whichever is longer. Do not retry simply because available evidence does not support a hypothesis.
- **On timeout, exhausted retries, or an error that cannot be retried:** Record the failure, affected business records, attempted operations, and any successfully generated hypotheses. Mark the task incomplete and send the case to T18: Handle Retrieval and Tool Exceptions. Do not forward incomplete or unsupported hypotheses as successful results.
