# Database Architecture

## Core entities
organizations, users, roles, leads, lead_requirements, lead_sources, lead_activities, lead_scores, developers, projects, project_configurations, inventory, site_visits, followups, opportunities, bookings, campaigns, campaign_leads, utm_tracking, communications, calls, messages, ai_conversations, ai_qualifications, notifications, audit_logs.

## Relationship summary
- Organization owns users, leads, projects, inventory, campaigns and all operational records.
- Lead has one current requirement profile and many activities, communications, followups, visits and opportunities.
- Project belongs to a developer and has configurations and inventory units.
- Inventory belongs to a project/configuration and may be linked to opportunities/bookings.
- Campaigns generate campaign leads and UTM attribution.
- AI records attach to a lead and retain model/provider metadata and explainable outputs.

## Data rules
Use UUID primary keys, foreign keys, created_at/updated_at timestamps, explicit enums/status values where appropriate, monetary numeric fields with currency context, and indexes on organization_id plus high-frequency filters.

## Inventory fields
Project, tower, floor, unit, BHK/configuration, carpet area, view, parking, base price, floor-rise, other charges, availability, updated_at.

## Lead requirement fields
BHK, budget min/max, preferred locations, property type, carpet-area range, possession timeline, self-use/investment, new-launch/ready/resale, loan required, down-payment comfort and EMI comfort.
