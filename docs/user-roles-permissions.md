# User Roles and Permissions

## Permission families
LEADS_VIEW, LEADS_CREATE, LEADS_EDIT, LEADS_ASSIGN
REQUIREMENTS_VIEW, REQUIREMENTS_EDIT
PROJECTS_VIEW, PROJECTS_EDIT
INVENTORY_VIEW, INVENTORY_EDIT, INVENTORY_RESERVE
VISITS_VIEW, VISITS_MANAGE
FOLLOWUPS_VIEW, FOLLOWUPS_MANAGE
CAMPAIGNS_VIEW, CAMPAIGNS_EDIT
REPORTS_VIEW, REPORTS_EXPORT
AI_USE, AI_CONFIGURE
USERS_MANAGE, ROLES_MANAGE
AUDIT_VIEW

## Role baseline
Organization Admin: all permissions within organization.
Sales Manager: leads/team operations, projects/inventory view, visits/followups, sales reports; no role/user administration unless granted.
Sales Executive: own/assigned leads, requirements, matches, visits, followups and sales records; project/inventory view.
Telecaller: assigned calling leads, communications, followups; limited project/inventory view.
Marketing: campaign/attribution management, marketing reports, permitted lead visibility.
Channel Partner/External Agent: explicitly shared leads/projects/inventory only; no organization-wide reporting.

Permissions should be data-driven so future custom roles do not require code changes.
