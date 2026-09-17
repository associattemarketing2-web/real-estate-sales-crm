# n8n Architecture

n8n is the automation/orchestration layer, not the system of record.

## Lead ingestion
META LEAD → validate payload → normalize fields → idempotency/duplicate check → Supabase lead → assign salesperson → notification/approved communication → audit event.

## Principles
- Store provider IDs and webhook event IDs for idempotency.
- Never trust external payloads for organization ownership.
- Use signed webhooks where supported.
- Retry transient failures; do not duplicate leads/messages.
- Keep credentials in n8n credential storage, never in workflow text committed to GitHub.
- Log workflow result/status without storing unnecessary personal data.

## Planned integrations
Meta Leads, Google Ads/UTM attribution, WhatsApp, email and voice AI. Provider-specific details belong in `integrations/`.
