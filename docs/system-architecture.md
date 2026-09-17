# System Architecture

## High-level
Browser app (React/TypeScript) → Supabase Auth/PostgreSQL/Storage/Realtime → Edge Functions for privileged/server-side logic → n8n and external providers for automation.

## Layers
1. Presentation: responsive CRM UI, role-aware navigation and action-oriented dashboards.
2. Application: validation, workflows, permissions-aware service functions and UI state.
3. Data: PostgreSQL relational model with foreign keys, constraints, indexes and RLS.
4. Integration: n8n workflows, webhooks and provider adapters.
5. Intelligence: deterministic scoring/matching plus AI enrichment and recommendations.

## Event concepts
`lead.created`, `lead.assigned`, `lead.qualified`, `lead.score.updated`, `project.created`, `inventory.updated`, `site_visit.created`, `site_visit.completed`, `followup.due`, `booking.created`.

## Scalability principles
Use indexed relational queries first. Avoid premature Redis/queues/microservices. Introduce background infrastructure only when measured workload requires it.

## Reliability
Idempotent webhook processing, unique external IDs where available, retry-safe automation, audit logs, timestamps in UTC, explicit status transitions and soft deletion/archive where business history must remain intact.
