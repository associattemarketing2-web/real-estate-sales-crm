# Testing Strategy

## Unit tests
Validation, scoring, matching rules, status transitions, permissions helpers and utility functions.

## Integration tests
Supabase queries, RLS policies, Edge Functions, webhook ingestion and idempotency.

## End-to-end tests
Login, role-based navigation, lead creation, assignment, qualification, project matching, visit creation, follow-up completion and booking workflow.

## Security tests
Cross-tenant read/write attempts, unauthorized role actions, direct API access, secret exposure checks and webhook spoof/replay cases.

## Regression rule
Each completed module must have tests covering its critical path before it is marked COMPLETE.
