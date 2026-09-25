# n8n Data Tables

## processed_submissions

Used for idempotency and duplicate submission protection.

| Column | Type | Purpose |
|---|---|---|
| submissionId | String | Unique submission ID from the lead source |
| source | String | website / google_form / meta |
| correlationId | String | n8n execution correlation ID |
| processedAt | Date & Time | Processing timestamp |
| status | String | processing / completed / failed |

## scoring_rules

| Column | Type |
|---|---|
| factor | String |
| value | String |
| score | Number |
| is_active | Boolean |
| version | String |