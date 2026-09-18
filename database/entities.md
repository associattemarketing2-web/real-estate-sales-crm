# Entity Definitions

## Organization and access
Organization is the tenant boundary. Users belong to one organization in the initial SaaS model. Roles define permissions; manager_user_id enables team hierarchy.

## Lead
Lead is the primary sales prospect record. Requirements are separated so changing requirements does not overwrite identity/source history. Activities are append-oriented. Ownership is explicit.

## Requirement
One current requirement profile per lead. Keep structured fields for matching and JSON only for genuinely variable multi-value preferences.

## Project
Project is the sellable real-estate development. Developer is a separate entity because one developer owns multiple projects.

## Configuration
Configuration represents a sellable product type within a project, such as 2 BHK or 3 BHK, and provides aggregate ranges.

## Inventory
Inventory is the atomic unit that can be shown, negotiated and booked. Availability and pricing must be timestamped.

## Opportunity
Opportunity represents a qualified sales opportunity associated with a lead and optionally a specific inventory unit.

## Site visit
A scheduled or completed physical/virtual visit connected to a lead and project.

## Follow-up
A salesperson action with an owner, due time and outcome. It is not the same as a communication record.

## Booking
Booking is a business transaction record and must preserve the booked inventory/value at booking time. Cancellation must not erase history.

## Attribution
Campaigns, campaign_leads and UTM tracking preserve acquisition context without making attribution dependent on a single channel.

## Communication
Communications provide channel-agnostic timeline entries. Calls and messages contain channel-specific details.

## AI records
AI conversations and qualifications are advisory records with provider/model metadata. AI must not silently mutate booking, inventory availability or ownership state.

## Audit
Audit logs preserve material changes to ownership, qualification, inventory, visits, negotiation/opportunity and booking state.
