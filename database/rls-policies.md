# Supabase RLS Policy Specification

## Security model
RLS is mandatory before production data. Tenant access is derived from authenticated membership, never from a client-supplied organization_id.

Recommended helper functions:
- auth_user_id() from Supabase auth
- current_app_user() returns internal user row
- current_organization_id() returns authorized tenant
- has_permission(permission_key)
- is_org_admin()
- is_manager_of(target_user_id)
- can_access_lead(lead_id)

All SECURITY DEFINER functions must set a safe search_path and avoid privilege escalation paths.

## Baseline policies
For every tenant-owned table:
- SELECT: caller belongs to organization and has role scope.
- INSERT: caller belongs to organization; organization_id is forced/validated to current tenant.
- UPDATE: caller belongs to organization and has permission for the record.
- DELETE: disabled by default for core business records; use status transitions/archive semantics.
- Service-role operations are server-side only and bypass normal user RLS by design.

## Role scopes
Organization Admin: organization-wide.
Sales Manager: organization records permitted for their team; manager hierarchy validated server-side.
Sales Executive: assigned/authorized leads and their related records.
Telecaller: calling/assigned lead scope.
Marketing: campaign, attribution and permitted lead-source data.
Channel Partner/External Agent: explicitly shared records only.

## Lead-dependent tables
Access to lead_requirements, activities, scores, visits, followups, communications, calls, messages and AI records should be based on access to the parent lead plus role permission.

## Project/inventory
Project and inventory visibility may be organization-wide for internal users, but mutation is permission-controlled. Booking/token operations require explicit sales permission and server-side validation.

## Audit logs
Users must not be able to edit or delete audit records through normal application roles. Writes should occur through trusted database functions/triggers or server-side services.

## Testing
For each tenant-owned table test:
1. same-org authorized read
2. same-org unauthorized role
3. cross-org read denied
4. cross-org insert denied
5. cross-org update denied
6. unauthorized delete denied
7. manager cannot access unrelated team's restricted records
8. external agent cannot access unshared records

## Important implementation note
Do not rely on frontend route guards for security. Frontend guards improve UX; RLS is the enforcement boundary.
