# Operational Logic

## Overview

The RevOps Intelligence Engine is designed around two operational phases:

1. call intelligence capture and validation
2. post-validation outcome execution

This allows the system to separate intelligence generation from business action.

---

## Phase 1: Call Intelligence Capture

After a sales call ends, Fathom sends transcript and metadata into the workflow.

The system then:

- receives the transcript
- generates a unique call ID
- runs AI analysis
- writes a structured Airtable record
- sends a Slack validation request to the rep

The result is a normalized deal intelligence record ready for review.

---

## Phase 2: Outcome Execution

Once the rep validates the record, the system routes the deal into an execution path based on final outcome.

### WON

- create onboarding workflow
- notify internal team
- mark execution complete

### FOLLOW-UP

- generate next-step strategy
- draft personalized follow-up email
- notify rep in Slack

### LOST

- generate nurture or re-engagement plan
- draft nurture email
- record loss reasoning

### INVALID

- exclude record from execution
- log reliability issue
- notify RevOps if needed

---

## Why Human Validation Matters

This system includes a human-in-the-loop step to avoid automating decisions off unvalidated AI output.

That design choice improves trust, data quality, and operational reliability.

---

## Reporting Use Cases

The resulting structured data can support:

- call outcome reporting
- objection trend analysis
- rep coaching reviews
- pipeline quality checks
- downstream workflow visibility
