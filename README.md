# RapidFix Lead Automation

Production-minded multi-source lead intake and routing automation built with n8n.

## Overview

RapidFix Lead Automation captures leads from multiple sources, normalizes the data into a canonical structure, validates submissions, prevents duplicate processing, scores and classifies leads, routes them based on business rules, syncs contacts with HubSpot, sends customer acknowledgements, sends internal Slack alerts, and records business audit data in Google Sheets.

## Current Lead Sources

- Website Form
- Google Form
- Meta Lead Ads planned

## Integrations

- n8n
- HubSpot CRM
- Google Sheets
- Gmail
- Slack

## Core Workflow

Lead Source  
→ Source Adapter  
→ Canonical Lead Model  
→ Format Validation  
→ Idempotency Check  
→ Lead Scoring  
→ Lead Classification  
→ Routing  
→ HubSpot CRM Sync  
→ Customer Email  
→ Slack Alert  
→ Google Sheets Audit

## Lead Scoring

Lead scoring is configuration-driven using an n8n Data Table.

Factors currently include:

- Urgency
- Service Type
- Property Type
- Lead Source

Scoring rules are versioned and stored separately from workflow logic.

## Routing Rules

Routing uses first-match priority logic.

Current routing order:

1. Emergency Major Plumbing → Plumbing Emergency Queue
2. Emergency HVAC → HVAC Emergency Queue
3. Commercial Property → Commercial Services Team
4. Hot Lead → Priority Dispatch
5. Fallback → Standard Dispatch

## Idempotency

Each source generates a stable submission ID.

The `processed_submissions` Data Table is used to prevent the same submission from being processed multiple times.

## CRM

HubSpot is used as the CRM source of truth.

Contacts are created or updated using email identity.

Custom properties include:

- Lead Source
- Service Type
- Urgency
- Lead Score
- Lead Classification
- Dispatch Route
- Last Submission ID
- Routing Reason

## Notifications

Customer acknowledgement emails are sent using Gmail.

Priority and hot leads can trigger Slack alerts for internal dispatch teams.

## Audit

Google Sheets records business-level processing results including:

- Submission ID
- Correlation ID
- Source
- Customer
- Score
- Classification
- Route
- HubSpot Contact ID
- CRM Action
- CRM Status
- Email Status
- Slack Status
- Overall Status

## Repository Structure

```text
rapidfix-lead-automation/
├── workflows/
│   ├── RapidFix Multi-Source Lead Intake.json
│   └── Lead Scoring Engine Lab.json
├── docs/
│   └── data-tables.md
├── sample-data/
│   └── scoring-rules-v1.json
├── screenshots/
├── .gitignore
└── README.md