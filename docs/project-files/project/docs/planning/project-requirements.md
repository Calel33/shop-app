 # Project Requirements Document (PRD) — Local Business Directory (Belize)
 
 Date: 2025-10-23
 
 ## 1. Scope & Goals
 - Region: Belize, country-wide.
 - Roles: Public (Visitor), Business Owner, Admin.
 - Approach: Mock-data-first; connect to Convex and Mapbox after UI validation.
 - Approvals: Manual admin approval for all owner submissions.
 - Non-goals (MVP): Reviews/ratings, monetization, advanced moderation.
 
 ## 2. Homepage (List-first)
 Order: Hero search → Featured categories → Featured businesses → Latest listings → Map preview (optional, below fold) → Link to full map view.
 
 ## 3. Listing Model (MVP)
 Fields:
 - name (string)
 - category (enum; admin-managed)
 - address (string)
 - location: { latitude (number), longitude (number) }
 - phone (string)
 - website (string | null)
 - hours (per-day open/close; optional)
 - images (array, up to 5)
 - shortDescription (<= 240 chars)
 - tags (array<string>)
 - status (draft | submitted | approved | rejected)
 
 ## 4. Search & Discovery
 - Inputs: keyword, category, location.
 - Filters: category, location (city/area), optional tag filters.
 - Results: infinite scroll; default sort relevance; if location is set, favor nearest.
 - Map View: dedicated page with Mapbox clustering and synchronized result list.
 
 ## 5. Owner Flow
 - Create/edit listing with precise map pin placement.
 - Submit for approval; track status: draft → submitted → approved/rejected.
 - Edit after rejection; resubmit.
 
 ## 6. Admin Flow
 - Review queue with filters.
 - Listing detail review; approve/reject; edit fields.
 - Manage categories/tags.
 
 ## 7. SLA & Validation
 - Approval target: within 48 hours.
 - Owner identity: Clerk-authenticated email verified.
 
 ## 8. Data & Integration Plan
 - Phase 1: Mock JSON fixtures powering all UI states.
 - Phase 2: Convex collections for listings, categories, users; serverless functions for submission/approval.
 - Mapbox: enabled on map view and owner pin placement after UI stabilizes.
 
 ## 9. Accessibility & Performance
 - Mobile-first layouts; keyboard navigation basics.
 - Image optimization; list virtualization if needed.
 
 ## 10. Legal
 - Terms of Service and Privacy Policy placeholders (links in footer).
 
