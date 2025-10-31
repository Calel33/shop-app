## Main Goal
Ship the Belize Directory MVP end-to-end: list-first discovery, owner submissions, admin approvals, and a dedicated Map View. Start mock-data-first, then flip to Convex/Mapbox via feature flags while maintaining mobile performance and data quality.

## 1. Implementation
- [ ] 1.1 Public UI (mock): homepage (hero, featured categories/businesses, latest listings, map preview link) — Goal: Validate list-first discovery layout and content hierarchy.
- [ ] 1.2 Public UI (mock): search results list with filters, infinite scroll, detail page — Goal: Prove search UX and detail coverage on mobile.
- [ ] 1.3 Owner (mock): dashboard list + create/edit listing form; submit for approval; status chips — Goal: Confirm owner workflow and validation without backend.
- [ ] 1.4 Admin (mock): review queue; approve/reject with reason; manage categories/tags — Goal: Validate manual approval process and taxonomy management.
- [ ] 1.5 Map View (mock→live): dedicated route with list sync; lazy-load Mapbox; clustering when token present — Goal: Ensure list↔map synchronization and performance with lazy-loaded map.
- [ ] 1.6 Feature flag: toggle mock vs Convex; gate Mapbox — Goal: Enable safe, incremental rollout from mock to live data.

## 2. Integration (Live Data)
- [ ] 2.1 Define Convex schema: listings, categories, users/owners, approvals (status) — Goal: Establish minimal, stable data model for MVP.
- [ ] 2.2 Implement Convex queries/mutations for search, owner submit/edit, admin approve/reject — Goal: Power core flows with real data and enforce workflow.
- [ ] 2.3 AuthZ: Clerk role checks on mutations; owners only edit own listings — Goal: Protect data integrity and enforce roles.
- [ ] 2.4 Wire frontend hooks to Convex behind feature flag — Goal: Swap data source without UI refactors.

## 3. Security & Quality
- [ ] 3.1 Validation: server-side field validation; image count ≤5; lat/lng bounds — Goal: Prevent bad data and abuse.
- [ ] 3.2 Rate limits on submissions/edits; basic logging for approvals — Goal: Deter spam and provide auditability.
- [ ] 3.3 Accessibility: keyboard navigation; focus states; color contrast — Goal: Meet baseline a11y for mobile and desktop.

## 4. Validation & Tooling
- [ ] 4.1 OpenSpec: `openspec validate add-belize-directory-mvp --strict` (fix any spec issues) — Goal: Keep proposal structurally sound.
- [ ] 4.2 Lint/build: `npm run lint` and `npm run build` (ensure no errors) — Goal: Maintain build health.
- [ ] 4.3 Demo data: ensure deterministic mock fixtures for all states (loading/empty/error/populated) — Goal: Reproducible demos and tests.
