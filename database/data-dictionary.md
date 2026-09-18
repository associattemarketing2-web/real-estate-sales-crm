# Data Dictionary and Business Rules

## Lead statuses
NEW, CONTACTED, QUALIFIED, PROJECT_MATCHED, BROCHURE_SHARED, SITE_VISIT_PLANNED, SITE_VISIT_DONE, NEGOTIATION, TOKEN, BOOKING, AGREEMENT, CLOSED, LOST, DORMANT, FUTURE_FOLLOW_UP.

## Temperature
HOT, WARM, COLD.

## Visit status
PLANNED, CONFIRMED, COMPLETED, NO_SHOW, CANCELLED, RESCHEDULED.

## Follow-up status
OPEN, COMPLETED, OVERDUE, CANCELLED.

## Opportunity stages
QUALIFIED, PROJECT_MATCHED, SITE_VISIT, NEGOTIATION, TOKEN, BOOKING, AGREEMENT, CLOSED_WON, CLOSED_LOST.

## Inventory status
AVAILABLE, BLOCKED, TOKEN, BOOKED, SOLD, HOLD, UNAVAILABLE.

## Purpose
SELF_USE, INVESTMENT, BOTH, UNKNOWN.

## Property type
APARTMENT, VILLA, PLOT, COMMERCIAL, OTHER.

## Lead-source types
META, GOOGLE, WEBSITE, WHATSAPP, CALL, REFERRAL, WALK_IN, PORTAL, OTHER.

## Qualification score
Initial deterministic score:
- Budget fit 20
- Location fit 20
- BHK/configuration fit 15
- Possession timeline fit 15
- Loan readiness 10
- Responded to outreach 5
- Brochure/price-plan engagement 5
- Site visit 10
Total 100.

Bands:
HIGH 80–100
MEDIUM 60–79
LOW 0–59

AI may add explanations, extraction and recommended actions, but the numeric score must be reproducible from stored factors and scoring_version.

## Money rules
Never use floating-point types for money. Store numeric amount and currency_code. Preserve historical transaction values even when current inventory pricing changes.

## Duplicate rules
Normalize phone/email first. Potential duplicates should be surfaced for review; never automatically merge records without an explicit business action.

## Inventory rules
Only one active booking/token should be allowed for a unit according to the organization's business policy. Database constraints/functions should prevent contradictory final states.

## Timestamps
Store UTC timestamptz. Display in organization/user timezone.
