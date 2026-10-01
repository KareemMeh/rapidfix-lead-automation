# RapidFix Lead Automation

Production-style lead automation built with **n8n**, combining multi-source lead intake, validation, deduplication, rule-based decisioning, AI-assisted analysis, CRM synchronization, notifications, audit logging, and reliability patterns.

Built as a portfolio project to demonstrate real-world automation architecture, API integrations, AI-assisted decisioning, and failure-handling strategies.

---

## Project Evolution

RapidFix was developed in two major versions.

### V1 — Rules-Based Automation

The first version focused on deterministic lead processing and business rules.

Main capabilities:

- Multi-source lead intake
- Canonical lead normalization
- Input validation
- Deduplication / idempotency
- Rule-based lead scoring
- Lead classification
- Business-rule routing
- HubSpot CRM synchronization
- Gmail notifications
- Slack alerts
- Google Sheets audit logging

---

### V2 — AI-Assisted Hybrid Automation

V2 extends the original rules-based system with AI-assisted interpretation while keeping business decisions deterministic and auditable.

Main additions:

- AI analysis of free-text lead messages
- Structured AI signals
- AI output validation
- Confidence-based fallback
- Hybrid AI + rule-based scoring
- Effective urgency resolution
- Improved final classification
- Improved routing logic
- Retry logic for external integrations
- Explicit failure branches
- Dead-Letter Queue pattern
- Integration recovery workflow
- Improved auditability

---

## Architecture

```text
Lead Sources
   │
   ├── Website Form
   ├── Google Form
   └── Other / API Sources
            │
            ▼
      Source Adapters
            │
            ▼
      Canonical Lead Model
            │
            ▼
        Validation
            │
            ▼
 Deduplication / Idempotency
            │
            ▼
      Rule-Based Scoring
            │
            ├──────────────┐
            │              │
            ▼              ▼
      AI Analysis      AI Failure
            │              │
            ▼              │
     Validate AI Output    │
            │              │
            ▼              │
      Confidence Check     │
            │              │
            ▼              │
      Hybrid Scoring       │
            │              │
            └──────┬───────┘
                   ▼
          Rules-Only Fallback
            when required
                   │
                   ▼
         Final Classification
                   │
                   ▼
             Final Routing
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
     HubSpot     Gmail      Slack
        │          │          │
        └──────────┴──────────┘
                   │
                   ▼
              Audit Logging
                   │
                   ▼
        Retry / Failure Handling
                   │
                   ▼
         Dead-Letter Queue
```

## Core Design Principle

AI interprets ambiguity. Code calculates. Rules decide. Humans handle uncertainty.

RapidFix does not allow the AI model to become the only decision-maker.
AI is used to interpret ambiguous free-text signals, while deterministic code and business rules remain responsible for scoring, classification, and routing.
If AI analysis fails, returns invalid output, or does not meet the required confidence level, the workflow falls back to the original rule engine.
AI-Assisted Decisioning
V2 analyzes signals such as:

- Purchase intent
- Business impact
- Specificity
- Urgency inferred from the message
- AI confidence
- AI summary
- AI reasoning
  These signals are converted into a structured AI score and combined with the existing rule score.
  Example:
  Rule Score

* # AI Signal Score
  Hybrid Score

The hybrid score is then used to calculate the final lead classification.
Lead Routing
Routing decisions are based on explicit business rules.
Examples include:
Emergency + Major Plumbing
→ Plumbing Emergency Queue

Emergency + HVAC
→ HVAC Emergency Queue

Commercial Property
→ Commercial Services Team

Priority Lead
→ Priority Dispatch

Fallback
→ Standard Dispatch

This keeps routing logic inspectable and predictable.
Reliability Design
RapidFix V2 includes production-minded reliability patterns.
Local Retry
External integrations use bounded retry logic for temporary failures such as:

- API timeouts
- Rate limits
- Temporary provider outages
- Network errors
  Explicit Failure Paths
  Handled integration failures produce structured status fields instead of silently failing.
  Examples:
  crmStatus
  emailStatus
  slackStatus

AI Fallback
AI failure does not stop lead processing.
AI Technical Failure
↓
Rules-Only Decision

Dead-Letter Queue
Failed integration operations can be stored in a Dead-Letter Queue after retries are exhausted.
A dedicated retry workflow can later retry only the failed operation instead of replaying the entire lead workflow.
This reduces the risk of duplicate CRM updates, duplicate emails, or repeated notifications.
Integrations
RapidFix demonstrates integration with:

- HubSpot CRM
- Gmail
- Slack
- Google Sheets
- Gemini / LLM API
- REST APIs
- Webhooks
  Technology Stack
- n8n
- REST APIs
- Webhooks
- HTTP
- JSON
- JavaScript expressions
- HubSpot CRM
- Gmail
- Slack
- Google Sheets
- Gemini / LLM integration
- Git
- GitHub
  Repository Structure
  rapidfix-lead-automation/
  │
  ├── workflows/
  │ ├── v1/
  │ └── v2/
  │
  ├── docs/
  │
  ├── sample-data/
  │
  ├── screenshots/
  │
  ├── demo/
  │
  ├── .gitignore
  │
  └── README.md

Workflow Files
V1
Located in:
workflows/v1/

Contains the original rules-based lead automation and scoring workflows.
V2
Located in:
workflows/v2/

Contains:

- RapidFix AI V2 main workflow
- DLQ Retry Worker
  Screenshots
  RapidFix V2
  Workflow Overview

AI Analysis and Hybrid Decisioning

Routing and Integrations

Reliability and Error Handling

Test Scenarios
RapidFix is designed to test scenarios such as:

- Valid lead with successful AI analysis
- AI technical failure
- Invalid AI output
- Low AI confidence
- Duplicate lead
- Emergency plumbing lead
- Emergency HVAC lead
- Commercial lead
- HubSpot failure
- Gmail failure
- Slack failure
- Retry exhaustion
- DLQ creation
  Security
  This repository is a portfolio project.
  Before publishing workflow exports, sensitive information should be removed or replaced.
  Do not commit:
- API keys
- OAuth tokens
- Passwords
- Real customer PII
- Private webhook URLs
- Production credentials
- Private CRM data
  Anyone importing the workflow should create and configure their own credentials.
  Project Status
  Portfolio / production-style automation project
  RapidFix demonstrates production-oriented architecture and reliability patterns, but it is presented as a portfolio project rather than a live client deployment.
  Author
  Kareem Mehaisen
  Automation & Integration Engineer
- GitHub: https://github.com/KareemMeh
- LinkedIn: https://www.linkedin.com/in/kareem-mehaisen-46a186217
