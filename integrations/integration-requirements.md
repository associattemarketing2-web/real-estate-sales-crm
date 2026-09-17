# Integrations

## Meta Leads
Capture provider lead ID, form/campaign/ad identifiers, normalize fields, deduplicate, assign organization/owner and log ingestion status.

## Google Ads / UTM
Persist source, medium, campaign, content, term and click identifiers where available. Attribution must survive landing-page to lead conversion.

## WhatsApp
Use approved provider/API flows. Store message metadata and relevant message content only as required. Keep credentials server-side.

## Email
Track send/delivery/failure metadata and templates. Avoid exposing provider credentials in the browser.

## Voice AI
Voice events should map to lead/contact identity, call status, duration, transcript reference and extracted requirements where permitted. Provider-specific implementation remains replaceable.

## Integration rule
External systems feed the CRM; Supabase remains the operational system of record for CRM entities.
