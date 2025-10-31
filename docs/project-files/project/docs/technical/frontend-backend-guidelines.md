 # Frontend & Backend Guidelines — Local Business Directory (Belize)
 
 Date: 2025-10-23
 
 ## Frontend Guidelines
 - Routing: App Router with segments for (public) home/search/detail, (owner) dashboard/listing-edit, (admin) review/taxonomy.
 - Styling: Tailwind v4 + shadcn/ui; token-only; dark/light via data-theme.
 - State/Data: Start with mock fixtures; feature flag to switch to Convex.
 - Loading/Error: Provide skeletons and error boundaries for all list/detail views.
 - Accessibility: Keyboard nav, focus rings via tokens, color contrast.
 - Map: Dedicated map view with synchronized list; lazy-load Mapbox.
 
 ## Backend Guidelines (Convex)
 - Schema (later): listings, categories, users, approvals (status: draft/submitted/approved/rejected).
 - Validation: server-side validation for required fields; fail-fast.
 - AuthZ: Clerk role checks on mutations (owner can edit own listings; admin can approve/manage).
 - Workflow: admin approval mutates status; rejection stores reason; edits may require re-approval.
 - Rate Limits/Abuse: basic per-user limits on submissions; audit logs on admin actions (later).
 
 ## Integration & Testing
 - Feature Flags: mock vs live data toggle.
 - Sync: list↔map query params unified; filters persist across views.
 - Testing: component tests for states (loading/empty/error/populated) using mock data; minimal e2e for critical flows later.
 
