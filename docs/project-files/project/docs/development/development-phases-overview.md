 # Development Phases Overview — Local Business Directory (Belize)
 
 Date: 2025-10-23
 
 Notes: Mock-data-first. Map is a supporting feature on homepage, with a dedicated full map view later. Only this document includes RAG recommendations.
 
 ## Phase 0 — Project Setup (Complete/Verify)
 - Ensure Next.js 15, Tailwind v4, shadcn/ui, Clerk, Convex scaffolding present.
 - Add feature flag for data source (mock | live).
 - Define env var placeholders and security headers defaults.
 - Deliverables: running app shell with dark/light theme and base tokens.
 
 ## Phase 1 — Public UI (Mock Data)
 - Build homepage sections: Hero search → Featured categories → Featured businesses → Latest listings → Map preview (below fold).
 - Build Search Results (list-first) with filters, infinite scroll (mock-paginated).
 - Build Listing Detail with all fields and states (loading/empty/error/populated).
 - Deliverables: end-to-end public flows using mock JSON.
 
 ## Phase 2 — Business Owner (Mock Data)
 - Owner dashboard (My Listings) with status chips.
 - Create/Edit Listing form (validation; ≤5 images; map pin placement mocked).
 - Submit for approval: draft → submitted → (mock) approved/rejected.
 - Deliverables: owner flows fully mocked with deterministic states.
 
 ## Phase 3 — Admin (Mock Data)
 - Review queue (filters/sort), Listing Review, Approve/Reject with reason.
 - Manage categories/tags UI.
 - Deliverables: admin flows fully mocked.
 
 ## Phase 4 — Map View Integration (Partial Live)
 - Implement dedicated Map View with Mapbox clustering; sync with list query state.
 - Keep data mock-backed; wire real Mapbox only (token, tiles, clustering).
 - Deliverables: interactive map + list sync, powered by mock listings.
 
 ## Phase 5 — Convex Integration (Live Data)
 - Define Convex schema: listings, categories, users, approvals.
 - Implement queries/mutations for public search, owner submit/edit, admin approve/reject.
 - Enforce auth/role checks (Clerk) and workflow validations.
 - Deliverables: feature flag flips to live data for core flows; map reads live data.
 
 ## Phase 6 — Hardening & Security
 - Add rate limits to sensitive mutations; logging for approvals.
 - Optimize performance (image handling, list virtualization if needed).
 - Accessibility passes; refine CSP/security headers.
 - Deliverables: production-ready staging build.
 
 ## Phase 7 — Launch & Post-Launch
 - Prepare Terms/Privacy; set env vars on Vercel; monitoring/alerts.
 - Rollout: Belize-wide soft launch; collect feedback.
 - Post-launch backlog: reviews/ratings, monetization tiers, moderation tools.
 
 ---
 
 ## RAG Recommendations (For Development Only)
 - Use retrieval-augmented snippets during development to surface:
   - Mapbox GL JS examples (clustering, sync list ↔ map interactions).
   - Convex schema and mutation patterns for role-based workflows.
   - Clerk best practices for role checks in Next.js App Router.
 - Storage: keep a small internal index of vetted docs/snippets; do not expose RAG to end users.
 - Guardrails: attribute sources in dev notes; never auto-execute untrusted code; human review required.
 
