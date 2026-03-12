# Airtable Schema

## Overview

This project uses Airtable as the structured CRM intelligence layer for storing sales call records, AI-generated deal intelligence, and workflow execution status.

The schema is designed to support both analysis and execution.

---

## Table 1: `deals_calls`

This table stores the primary call and deal intelligence record.

### Purpose

Convert each sales call into a normalized record that can support reporting, validation, and downstream workflows.

### Fields

| Field | Type | Description |
|---|---|---|
| call_id | text | Primary record identifier |
| prospect_name | text | Prospect or company name |
| outcome | single select | WON, FOLLOW-UP, LOST, INVALID |
| deal_value | number | Estimated or confirmed revenue value |
| deal_health | single select | STRONG, MODERATE, AT_RISK, CLOSED_WON, CLOSED_LOST |
| decision_category | single select | Reason category behind deal movement |
| decision_driver | long text | Primary reason driving the decision |
| summary | long text | AI-generated call summary |
| discovery_quality_score | number | Score from 1–5 |
| discovery_gaps | long text | Missing discovery elements |
| sales_skill_focus | text | Suggested coaching focus |
| coaching_feedback | long text | Rep coaching feedback |
| objection_handling_script | long text | Suggested objection response |
| next_action | text | Recommended next move |
| next_step_quality | single select | Clear & Scheduled, Verbal but Vague, No Next Step Mentioned |
| close_probability_estimate | single select | HIGH, MEDIUM, LOW |
| implementation_priorities | long text | Priorities for onboarding or next stage |
| customer_success_risks | long text | Potential post-sale risks |
| expansion_signals | long text | Upsell or expansion indicators |
| call_sentiment_score | number | Sentiment score from 1–5 |
| confidence_score | number | AI confidence score |
| slack_summary | short text | Slack-ready summary |
| follow_up_email_draft | long text | AI-generated email draft |
| rep_confirmed | checkbox | Rep confirmed record |
| workflows_executed | checkbox | Downstream workflows completed |
| rep_id | linked record | Link to reps table |

---

## Table 2: `reps`

Stores rep information used for ownership and reporting.

### Fields

| Field | Type | Description |
|---|---|---|
| rep_id | text | Unique rep identifier |
| rep_name | text | Rep name |
| team | text | Team or segment |
| manager | text | Manager name |

---

## Table 3: `reliability_logs`

Stores workflow errors, invalid records, and exceptions.

### Fields

| Field | Type | Description |
|---|---|---|
| timestamp | date/time | Log timestamp |
| call_id | text | Related call ID |
| error_type | single select | invalid_outcome, json_parse_error, api_error, unknown |
| error_message | long text | Error details |
| status | single select | open, resolved |
| resolved_by | text | Owner of resolution |

---

## Why Airtable

Airtable works well for this project because it supports:

- structured RevOps data modeling
- easy rep validation workflows
- flexible reporting
- rapid operational iteration
