## Why
Belize lacks a unified, trustworthy directory for discovering local businesses. We need a mobile-first, list-centric directory with owner submissions and admin approvals, with a dedicated map view as a supporting experience.

## What Changes
- Add public discovery flows: list-first homepage, search results list, listing detail
- Add owner submission flows: create/edit listing, submit for approval, status tracking
- Add admin approval flows: review queue, approve/reject, manage categories/tags
- Add dedicated Map View (Mapbox) with clustering and list sync (behind feature flag until UI validated)
- Mock-data-first; later toggle to Convex live data and enable Mapbox

## Impact
- Affected specs: `public-discovery`, `owner-submission`, `admin-approval`, `map-view`
- Affected code: `app/(landing)/*`, `app/dashboard/*`, `components/*` (listing cards, forms), `convex/*` (later: listings, categories, approvals), Mapbox integration in `app/*/map`
- Security & roles: Clerk-protected owner/admin routes; manual approval for data quality
