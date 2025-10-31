# Problem Statement — Local Business Directory (Belize)

Date: 2025-10-23

## Context
Belize lacks a unified, trustworthy directory for discovering local businesses. Existing sources are fragmented, outdated, and hard to search by location and category on mobile. The homepage should prioritize list-based discovery with featured content, with maps as a supporting experience.

## Target Users
- Public (unauthenticated): Residents and tourists who need to find nearby services quickly.
- Business Owners: Local businesses seeking visibility and control over their listings.
- Admins: Team members responsible for data quality and approvals.

## Core Problem
- Users cannot reliably discover relevant businesses by proximity, category, and keywords in one place.
- Business owners lack an easy, self-serve way to publish accurate listings and keep them updated.
- Data quality suffers without clear approval and moderation.

## Proposed Solution
- A list-first homepage (hero search, featured categories, featured businesses, latest listings) with an optional map preview section and a dedicated full map view using Mapbox (with clustering and fast search).
- Owner self-serve listing creation/updates, submitted for manual admin approval.
- Admin dashboard to add/manage businesses and approve listings.
- Mock data first for all pages/components; later connect to Convex (data) and Mapbox (geospatial) once UI is validated.

## Scope (MVP)
- Geography: Belize (country-wide) with city/area filters.
- Roles: Public, Business Owner, Admin.
- Features: List-first homepage (hero search, featured categories, featured businesses, latest listings), business detail pages, category filters, optional map preview and dedicated map view, owner submission flow, admin manual approval.

## Out of Scope (MVP)
- Reviews and ratings.
- Monetization/subscriptions.
- Advanced moderation/reporting workflows.

## Constraints & Assumptions
- Tech stack is predefined: Next.js 15 (App Router), Tailwind v4, shadcn/ui, Convex, Clerk (+Billing later), Mapbox, Vercel.
- Manual approval ensures data quality; near real-time updates via Convex.
- Mock-data-first implementation for rapid UI iteration; switch to Convex/Mapbox integration after UI and flows are validated.

## Success Criteria (MVP)
- Users can discover relevant businesses in Belize via map + filters and open a detail view.
- Owners can submit and manage listings; Admins can approve/reject efficiently.
- Listings display accurate location, hours, and contact info on mobile and desktop.
