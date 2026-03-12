# Make Workflow Architecture

## Overview

This project uses Make as the orchestration layer for ingesting transcripts, running AI analysis, writing structured records, and routing validated deals into downstream workflows.

---

## Workflow Pipeline

Fathom Transcript Event
      ↓
Webhook Trigger
      ↓
Generate Call ID
      ↓
OpenAI Analysis
      ↓
JSON Parsing
      ↓
Airtable Record Creation
      ↓
Slack Validation Request
      ↓
Outcome-Based Routing

---

## Workflow Modules
1. Webhook Trigger

The workflow begins when Fathom sends a completed transcript payload.

The payload includes transcript text and call metadata.

2. Generate Call ID

A unique call identifier is created for each transcript.

Example format:

CALL-YYYYMMDD-HHmmss

This ID is used to track the record across systems.

3. OpenAI Analysis

The transcript is sent to OpenAI using a structured RevOps prompt.

The model returns strict JSON containing:
- deal outcome
- deal value
- deal health
- decision category
- objection analysis
- coaching feedback
- follow-up email draft
- Slack summary

4. JSON Parsing

The returned JSON is parsed into structured fields.

This step enforces:
- enums
- numeric values
- field mapping consistency

5. Airtable Record Creation

A new deal record is created in Airtable using the generated call ID.

The workflow writes:
- call metadata
- AI-generated intelligence
- validation fields
- automation status fields

6. Slack Validation Request

A message is sent to the rep in Slack with:
- prospect name
- AI-generated outcome
- summary
- link to the Airtable record

The rep validates the record before automation continues.

7. Outcome Routing

After validation, the workflow branches into one of four paths:
- WON
- FOLLOW-UP
- LOST
- INVALID

Each path executes a different downstream automation sequence.

---

## Reliability Considerations

Important workflow safeguards include:
- validation checkpoint before execution
- enum-based branching logic
- fallback handling for unexpected outcomes
- error logging for invalid or failed records
