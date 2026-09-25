# Testing

The workflow was tested across different scoring and routing scenarios.

## Test Cases

### Emergency HVAC

Expected:

- Classification: priority
- Route: hvac_emergency_queue
- Slack alert: sent

### Commercial Same-Day HVAC

Expected:

- Classification: hot
- Route: commercial_services_team
- Slack alert: sent

### Residential Maintenance Within 48 Hours

Expected:

- Classification: warm
- Route: standard_dispatch
- Slack alert: not required

### Residential Quote Request

Expected:

- Classification: standard
- Route: standard_dispatch
- Slack alert: not required

## Integration Checks

Validated:

- Website lead intake
- Google Form lead intake
- Duplicate protection
- Data-driven scoring
- Classification
- Routing
- HubSpot create/update
- Gmail acknowledgement
- Slack alerts
- Google Sheets audit logging