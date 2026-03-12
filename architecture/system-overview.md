# System Architecture Overview

## Project

RevOps Intelligence Engine

An AI-powered workflow that transforms sales call transcripts into structured deal intelligence and automated revenue workflows.

---

## System Goal

The goal of this system is to convert unstructured sales conversations into standardized records that can support pipeline visibility, rep coaching, and downstream execution.

The system combines transcript ingestion, AI analysis, structured data modeling, human validation, and outcome-based automation.

---

## High Level Architecture

Sales Call Transcript
      ↓
Webhook Ingestion
      ↓
AI Deal Intelligence Analysis
      ↓
Structured CRM Database
      ↓
Rep Validation
      ↓
Automation Outcomes

---

## Key Components

Event Source
The system begins with a completed sales call captured by Fathom.

Inputs include:
- transcript text
- meeting metadata
- prospect details
- call context

---

## Data Ingestion
A custom webhook receives the transcript payload and routes it into the workflow.

This layer is responsible for:
- receiving transcript events
- generating a unique call ID
- normalizing the payload for downstream analysis

---

## AI Deal Intelligence Engine

The transcript is analyzed by OpenAI using a structured prompt designed for revenue operations.

The AI extracts fields such as:
- outcome
- deal health
- decision category
- objections
- next steps
- coaching feedback
- follow-up email draft

---

## Structured CRM Database

The extracted intelligence is written into Airtable using a normalized schema.

This creates a standardized record for:
- reporting
- coaching
- rep validation
- downstream automation

---

## Human Validation

A Slack message is sent to the rep for review and confirmation.

This step provides a human checkpoint before automation outcomes are executed.

---

## Automation Outcomes

Once validated, the workflow branches based on final outcome:
- WON
- FOLLOW-UP
- LOST
- INVALID

Each branch triggers the appropriate downstream actions and logs the result.
