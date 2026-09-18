# Database Relationships

organizations 1—N users
organizations 1—N developers
organizations 1—N projects
organizations 1—N leads
organizations 1—N campaigns
organizations 1—N inventory and operational records

developers 1—N projects
projects 1—N project_configurations
projects 1—N inventory
project_configurations 1—N inventory

leads 1—1 lead_requirements
leads 1—N lead_activities
leads 1—N lead_scores
leads 1—N site_visits
leads 1—N followups
leads 1—N opportunities
leads 1—N bookings
leads 1—N communications
leads 1—N calls
leads 1—N messages
leads 1—N ai_conversations
leads 1—N ai_qualifications
leads 1—N campaign_leads
leads 1—N utm_tracking

opportunities N—1 projects
opportunities N—1 inventory (nullable)
bookings N—1 opportunities
bookings N—1 inventory

users N—1 organizations
users N—1 roles
users N—1 users(manager_user_id)

campaigns N—1 lead_sources
campaign_leads N—1 campaigns
campaign_leads N—1 leads

## Ownership rules
- Every relationship must remain within the same organization.
- Foreign-key writes must be validated against the caller's tenant.
- A lead owner must be a user in the same organization.
- Project, inventory, opportunity, visit and booking links must all resolve to the same organization.
- External/channel-partner access is implemented through explicit sharing/authorization, not by weakening tenant RLS.
