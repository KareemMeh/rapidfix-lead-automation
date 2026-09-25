# Setup

## Requirements

- n8n
- HubSpot account
- Google account
- Slack workspace

## Required Credentials

Configure these credentials inside n8n:

- Google Sheets OAuth2
- Google Sheets Trigger OAuth2
- Gmail OAuth2
- HubSpot OAuth2
- Slack Bot

Credentials and secrets are not included in this repository.

## Import Workflows

Import:

- `workflows/RapidFix Multi-Source Lead Intake.json`
- `workflows/Lead Scoring Engine Lab.json`

## Data Tables

Create the required n8n Data Tables described in:

`docs/data-tables.md`

Then populate the scoring rules using:

`sample-data/scoring-rules-v1.json`

## External Resources

Create:

- Google Form lead source
- Google Sheets Lead Audit sheet
- HubSpot contact custom properties
- Slack urgent leads channel

Update workflow resource IDs and credentials for your own environment.