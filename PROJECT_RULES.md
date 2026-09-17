# Project Rules

## Source of truth
GitHub is the engineering and product source of truth. Specifications must be updated before implementation changes that alter behavior or architecture.

## Non-negotiable rules
- Multi-tenant data must be scoped by `organization_id` and protected by Supabase RLS.
- Never expose secrets, service-role keys, provider tokens, or private credentials to the browser.
- Do not create duplicate tables or parallel concepts for the same business entity.
- Prefer PostgreSQL constraints, indexes, functions and deterministic business rules for core CRM logic.
- AI may recommend, classify or summarize; critical business state must remain explainable and controllable.
- Do not make destructive schema changes without an explicit migration and review.
- Every feature needs acceptance criteria and a test plan.
- Do not add dependencies without a documented reason.
- Keep provider integrations behind server-side adapters/functions where practical.
- Preserve auditability for lead ownership, qualification, inventory, visits, negotiation and booking changes.
- Do not build outside the approved roadmap merely because a UI idea is attractive.

## Architecture boundaries
- Lovable: application UI and frontend implementation.
- Supabase: PostgreSQL, Auth, Storage, Realtime, RLS and Edge Functions.
- n8n: external automation and integration orchestration.
- GitHub: version control and approved specifications.
- Notion: optional operational/product collaboration mirror.
- AI providers: replaceable services accessed through controlled server-side interfaces.

## Delivery states
PLANNED → IN PROGRESS → TESTING → COMPLETE

## Definition of done
A feature is complete only when requirements, permissions, validation, loading/error/empty states, tests, audit behavior and documentation are addressed.
