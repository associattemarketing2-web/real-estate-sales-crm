# Database Schema Specification

## Principles
- PostgreSQL/Supabase.
- UUID primary keys; timestamptz for timestamps.
- Every tenant-owned operational table has organization_id and RLS.
- Foreign keys use explicit ON DELETE behavior; avoid accidental cascades for business records.
- Monetary values use numeric(14,2) plus currency_code.
- Use CHECK constraints/enums only for stable business states; prefer lookup/config tables when values are expected to change.
- created_at, updated_at on mutable entities; immutable business events retain occurred_at.

## Tables

### organizations
id, name, slug, status, default_currency, timezone, created_at, updated_at.

### roles
id, organization_id nullable for system roles, name, permissions_json, created_at.

### users
id, organization_id, auth_user_id, role_id, full_name, phone, email, status, manager_user_id nullable, created_at, updated_at.

### developers
id, organization_id, name, contact details, website, status, created_at, updated_at.

### projects
id, organization_id, developer_id, name, slug, location_text, city, locality, rera_number, property_type, land_area, tower_count, possession_date, status, description, created_at, updated_at.

### project_configurations
id, organization_id, project_id, name, bhk, property_type, carpet_min, carpet_max, price_min, price_max, possession_date, created_at, updated_at.

### inventory
id, organization_id, project_id, configuration_id, tower, floor, unit_number, bhk, carpet_area, facing, view, parking_count, base_price, floor_rise, other_charges, total_price, currency_code, status, available_from, last_verified_at, created_at, updated_at.

### lead_sources
id, organization_id, name, source_type, provider, active, created_at, updated_at.

### campaigns
id, organization_id, lead_source_id, name, platform, campaign_external_id, start_date, end_date, spend, currency_code, created_at, updated_at.

### leads
id, organization_id, owner_user_id, created_by_user_id, first_name, last_name, phone, email, city, language, source_id, campaign_id, status, temperature, next_action_at, last_contacted_at, last_activity_at, duplicate_of_lead_id nullable, created_at, updated_at.

### lead_requirements
id, organization_id, lead_id unique, bhk_min, bhk_max, budget_min, budget_max, currency_code, preferred_locations_json, property_types_json, carpet_area_min, carpet_area_max, possession_deadline, purpose, launch_preference, loan_required, down_payment_comfort, emi_comfort, notes, created_at, updated_at.

### lead_activities
id, organization_id, lead_id, user_id, activity_type, activity_at, outcome, notes, metadata_json, created_at.

### lead_scores
id, organization_id, lead_id, score, band, factors_json, scoring_version, calculated_at, created_at.

### site_visits
id, organization_id, lead_id, project_id, assigned_user_id, scheduled_at, status, attendees_count, outcome, notes, created_at, updated_at.

### followups
id, organization_id, lead_id, owner_user_id, due_at, followup_type, priority, status, outcome, notes, completed_at, created_at, updated_at.

### opportunities
id, organization_id, lead_id, project_id, inventory_id nullable, stage, expected_value, probability, expected_close_date, owner_user_id, created_at, updated_at.

### bookings
id, organization_id, opportunity_id, lead_id, project_id, inventory_id, booking_amount, total_value, currency_code, booking_date, status, cancellation_reason, created_at, updated_at.

### campaign_leads
id, organization_id, campaign_id, lead_id, attributed_at, attribution_type, created_at.

### utm_tracking
id, organization_id, lead_id, source, medium, campaign, term, content, landing_page, captured_at, created_at.

### communications
id, organization_id, lead_id, user_id nullable, channel, direction, provider, external_id, sent_at, status, content_summary, created_at.

### calls
id, organization_id, lead_id, user_id, provider, external_call_id, direction, started_at, ended_at, duration_seconds, disposition, recording_reference nullable, transcript_reference nullable, created_at.

### messages
id, organization_id, lead_id, user_id nullable, channel, provider, external_message_id, direction, sent_at, status, body_reference nullable, created_at.

### ai_conversations
id, organization_id, lead_id, channel, provider, model, session_id, started_at, ended_at, summary, created_at.

### ai_qualifications
id, organization_id, lead_id, ai_conversation_id nullable, model, qualification_json, confidence, recommended_next_action, created_at.

### notifications
id, organization_id, user_id, lead_id nullable, type, title, body, priority, due_at, read_at, created_at.

### audit_logs
id, organization_id, actor_user_id nullable, entity_type, entity_id, action, before_json, after_json, metadata_json, occurred_at.

## Required indexes
For tenant tables, index organization_id. Add composite indexes for:
- leads(organization_id, owner_user_id, status)
- leads(organization_id, next_action_at)
- leads(organization_id, phone)
- lead_activities(organization_id, lead_id, activity_at desc)
- followups(organization_id, owner_user_id, status, due_at)
- site_visits(organization_id, scheduled_at, status)
- projects(organization_id, city, status)
- inventory(organization_id, project_id, status)
- inventory(organization_id, bhk, total_price, status)
- audit_logs(organization_id, entity_type, entity_id, occurred_at desc)

## Uniqueness
Use organization-scoped unique constraints for project slug, campaign external IDs where applicable, and inventory identity (project,tower,unit_number). Phone normalization should be handled before duplicate checks.

## Derived vs stored data
Store source-of-truth business values. Calculate match percentages, funnel metrics and dashboard aggregates from source data or controlled views/functions. Do not duplicate mutable values without a defined synchronization rule.
