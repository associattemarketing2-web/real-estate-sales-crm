# Acceptance Criteria

## Global
- Every tenant-owned query is RLS-protected.
- Cross-tenant access is denied even when IDs are manually supplied.
- Role permissions are enforced server-side.
- Forms validate required fields and business constraints.
- Loading, empty, error and success states exist.
- Important mutations create audit history.
- No secret/provider token is exposed in browser code.

## Leads
- Create, edit, search and filter leads.
- Phone/email normalization and duplicate warning work.
- Assignment respects role scope.
- Requirement profile is visible from Lead 360.
- Next action and overdue state are explicit.

## Qualification
- Score is deterministic and reproducible.
- Score factors are displayed.
- Score history is retained.
- AI output cannot silently change critical business state.

## Projects/inventory
- Projects can be filtered by location/status.
- Inventory supports BHK, price, carpet, tower/floor and availability filters.
- Inventory freshness is visible.
- Booking/reservation cannot create contradictory inventory state.

## Matching
- Matching uses structured lead requirements.
- Every returned match includes fit reasons.
- Match results identify stale/unavailable inventory.
- Shared shortlists are recorded against the lead.

## Followups/visits
- Due/overdue followups are queryable.
- Visit schedule prevents invalid status transitions.
- Completion captures outcome.

## Booking
- Booking records preserve historical value and inventory identity.
- Server-side authorization is required.
- Audit records capture status/value/inventory changes.

## Testing
Before marking a module complete:
- happy path
- validation failures
- permission failures
- cross-tenant negative tests
- empty/loading/error states
- concurrency-sensitive business rules
- mobile/responsive check
