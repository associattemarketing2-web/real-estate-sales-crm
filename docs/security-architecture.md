# Security Architecture

## Tenant isolation
Every organization-owned table contains `organization_id`. RLS policies must derive the current organization from authenticated user membership rather than trusting a client-supplied organization ID.

## Roles
Super Admin, Organization Admin, Sales Manager, Sales Executive, Telecaller, Marketing, Channel Partner/External Agent.

## Access model
Organization Admin: organization-wide access. Sales Manager: team-scoped access. Sales Executive: assigned/authorized leads and opportunities. Telecaller: calling scope. Marketing: attribution/campaign scope. External agents: explicitly shared records only.

## Security requirements
- Supabase RLS enabled on all tenant tables before production data is introduced.
- Least-privilege policies and tested negative cases.
- Service-role key only in trusted server environments.
- Secrets stored in Supabase/n8n secret management, never committed.
- Audit important permission, ownership, inventory, qualification and booking changes.
- Validate webhook signatures where providers support them.
- Rate-limit public ingestion endpoints.
- Minimize personal data, define retention rules and support data export/deletion workflows subject to business/legal requirements.
