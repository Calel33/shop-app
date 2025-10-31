## Context
Multi-role Belize local directory with list-first discovery, owner submissions, admin approvals, and a dedicated Map View. Start with mock data to validate UX, then integrate Convex and Mapbox.

## Goals / Non-Goals
- Goals: Fast list-first discovery; simple owner submission; clear admin approval; map view with clustering; minimal complexity initially
- Non-Goals (MVP): Reviews/ratings, monetization, advanced moderation

## Decisions
- App Router (Next.js 15) with server/client components as needed; Tailwind v4 + shadcn/ui
- Mock-data-first via fixtures; feature flag to switch to Convex live data
- Clerk for auth/roles (public, owner, admin); protect owner/admin routes via middleware
- Convex schema later: listings, categories, users/owners, approvals (status workflow)
- Mapbox for dedicated Map View with clustering; lazy-load on that route only

## Risks / Trade-offs
- Manual approvals add friction → improves data quality; SLA target 48h
- Mapbox token handling and quota → restrict token; lazy-load; fall back gracefully
- Data model evolution risk → start minimal; add fields post-MVP as MODIFIED deltas

## Migration Plan
1) Phases: Public UI → Owner → Admin → Map View → Convex integration → Hardening
2) Flip feature flag to move from mock data to Convex; gate Mapbox behind flag until ready
3) Add rate limits and logging during hardening

## Open Questions
- City/area taxonomy source and canonical list?
- Image storage approach post-mock (limits, EXIF removal, hosting)?
- Re-approval policy for sensitive edits (which fields trigger re-approval)?
