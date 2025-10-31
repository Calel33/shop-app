# Belize Directory MVP - Stack Diffs Plan (Graphite Workflow)

**Goal:** Ship Belize Directory MVP end-to-end with list-first discovery, owner submissions, admin approvals, and Map View. Start mock-data-first, then integrate Convex/Mapbox via feature flags.

**Stack Strategy:** Break the MVP into 8 focused, stacked PRs (using Graphite) on a feature branch. Stacks are reviewed and merged sequentially to the feature branch, with parallel work on stacks 3-5. Final merge to main after all stacks are complete.

---

## Stack Architecture & Workflow

```
main (trunk)
  ↓
feature/belize-directory (feature branch)
  ↓
  Stack 1: mock-data-fixtures (mock data + types)
    ↓
    Stack 2: public-ui-list-discovery (homepage, list view)
      ├─ Stack 3: public-ui-detail-search (parallel work) ┐
      ├─ Stack 4: owner-ui-dashboard (parallel work)       ├─ Merged sequentially
      └─ Stack 5: admin-ui-approval (parallel work)        ┘
    ↓
    Stack 6: map-view-integration (Map View with clustering)
      ↓
      Stack 7: convex-schema-integration (backend + feature flags)
        ↓
        Stack 8: security-and-qa (validation, a11y, rate limits)
          ↓
          feature/belize-directory → main (Final merge)
```

**Key Points:**
- All stacks created on `feature/belize-directory` branch
- Stacks 1 & 2 are sequential (dependent)
- Stacks 3, 4, 5 can be worked on in **parallel** after Stack 2 ships
- Stacks 6, 7, 8 are sequential again (dependent on prior work)
- Each stack is a PR reviewed against `feature/belize-directory`
- Final PR: `feature/belize-directory` → `main`

---

## Stack Details

### Stack 1: Mock Data Fixtures & Types
**Task:** 1.1, 1.2, 1.3, 1.4 foundation  
**Goal:** Establish reusable mock data and TypeScript types for all flows  
**Files:**
- `lib/mock-data/listings.ts` - Mock listing fixtures (10-20 deterministic listings with categories, images, locations)
- `lib/mock-data/categories.ts` - Category/tag fixtures
- `lib/mock-data/users.ts` - Mock owner and admin users
- `lib/types/directory.ts` - TypeScript types: Listing, Category, Approval, Review, Location
- `lib/types/index.ts` - Export all types

**Key Changes:**
- Define stable, reusable mock fixtures for all UI states (loading, empty, populated, error)
- Export all types for consistent usage across components
- No UI components, no routes—just data and types

**Success Criteria:**
- Types compile and are importable
- Mock data covers all UI states and variations
- Fixtures are deterministic (same data on every import)

---

### Stack 2: Public UI - List Discovery (Homepage & List View)
**Task:** 1.1 + foundation for 1.2  
**Goal:** Validate list-first discovery layout on mobile  
**Files:**
- `app/(landing)/directory/page.tsx` - Public homepage (hero, featured categories, latest listings)
- `components/directory/hero-section.tsx` - Hero with search CTA
- `components/directory/featured-categories.tsx` - Grid of featured categories (clickable to filter)
- `components/directory/listings-grid.tsx` - Responsive grid of listing cards
- `components/directory/listing-card.tsx` - Individual listing card (image, title, category, rating, distance)
- `components/directory/map-preview-cta.tsx` - CTA link to Map View
- `lib/mock-data/index.ts` - Export all fixtures

**Key Changes:**
- Server component for page, client components for interactive sections
- Use design system tokens (colors, spacing, shadows)
- Mobile-first responsive design (Tailwind grid: col-1 mobile → col-4 desktop)
- Link to search results page (not yet built, use placeholder)
- Link to Map View CTA (route not yet created)

**Success Criteria:**
- Homepage renders with mock data
- Featured categories are clickable stubs
- Responsive on mobile/tablet/desktop
- `npm run lint` passes
- `npm run build` succeeds

---

### Stack 3: Public UI - Search & Detail
**Task:** 1.2  
**Goal:** Prove search UX and detail page coverage on mobile  
**Files:**
- `app/(landing)/directory/search/page.tsx` - Search results page with filters
- `app/(landing)/directory/listings/[id]/page.tsx` - Listing detail page
- `components/directory/search-header.tsx` - Search input with filters (category, distance, rating)
- `components/directory/infinite-scroll-list.tsx` - Infinite scroll container with pagination state
- `components/directory/search-filters.tsx` - Filter sidebar (category, sort, distance)
- `components/directory/listing-detail.tsx` - Detail page content (images, description, contact, map embed placeholder)
- `lib/utils/search.ts` - Mock search/filter logic (client-side array filtering)

**Key Changes:**
- Implement client-side search and filtering on mock data
- Infinite scroll UX (load 10 items per scroll, mock pagination)
- Detail page shows: gallery, category, location, description, owner contact, map placeholder
- All interactive logic uses mock data (Convex integration happens later)
- Use shadcn components (Card, Button, Input, Select)

**Success Criteria:**
- Search filters work on mock data (client-side)
- Infinite scroll loads items progressively
- Detail page displays all listing info
- Mobile experience validated
- No console errors or warnings

---

### Stack 4: Owner UI - Submissions & Dashboard
**Task:** 1.3  
**Goal:** Confirm owner workflow without backend integration  
**Files:**
- `app/dashboard/listings/page.tsx` - Owner's listing dashboard
- `app/dashboard/listings/create/page.tsx` - Create listing form
- `app/dashboard/listings/[id]/edit/page.tsx` - Edit listing form
- `components/owner/listings-table.tsx` - Table of owner's listings with status chips
- `components/owner/listing-form.tsx` - Reusable form (create/edit) with validation
- `components/owner/status-badge.tsx` - Status indicator (draft, pending, approved, rejected)
- `lib/validations/listing.ts` - Client-side validation schema (Zod)
- `lib/hooks/use-owner-listings.ts` - Mock hook to get/submit listings (localStorage or state)

**Key Changes:**
- Protected routes (Clerk middleware already in place, dashboard/* routes)
- Form includes: title, description, category, images (max 5), location (lat/lng), contact info
- Client-side validation (Zod schema)
- Status tracking (draft → pending → approved/rejected)
- Submit for approval button (no backend yet—store in mock state/localStorage)
- List shows owner's own listings with status badges

**Success Criteria:**
- Form validation works (client-side)
- Listings persist in mock state during session
- Status flow is clear (draft → pending → approved)
- Mobile-friendly form inputs
- Accessibility: keyboard navigation, focus states

---

### Stack 5: Admin UI - Approval Queue & Taxonomy
**Task:** 1.4  
**Goal:** Validate manual approval process and taxonomy management  
**Files:**
- `app/dashboard/admin/approvals/page.tsx` - Review queue
- `app/dashboard/admin/categories/page.tsx` - Category/tag management
- `components/admin/approval-queue.tsx` - Sortable/filterable table of pending listings
- `components/admin/approval-card.tsx` - Expandable card with listing preview, approve/reject buttons, reason input
- `components/admin/category-manager.tsx` - Add/edit/delete categories
- `lib/hooks/use-admin-approvals.ts` - Mock hook for approval actions
- `lib/hooks/use-categories.ts` - Mock hook for category management

**Key Changes:**
- Admin-protected routes (use Clerk roles or hardcoded mock admin check for now)
- Approval queue shows pending listings with preview
- Inline approve/reject with optional reason (stored in mock state)
- Category manager: CRUD for categories/tags
- Status updates reflected in mock state (no Convex yet)

**Success Criteria:**
- Approval workflow is clear and intuitive
- Reject reason is captured
- Category CRUD works in mock state
- Admin UI is protected (only admin users can access)
- Status changes reflected in mock listings

---

### Stack 6: Map View - List↔Map Sync
**Task:** 1.5 (mock phase)  
**Goal:** Ensure list↔map synchronization and performance before live Mapbox integration  
**Files:**
- `app/(landing)/directory/map/page.tsx` - Dedicated Map View page
- `components/directory/map-container.tsx` - Map wrapper with Mapbox lazy-load placeholder
- `components/directory/map-list-panel.tsx` - Synchronized list panel next to map
- `components/directory/map-marker.tsx` - Individual marker component
- `lib/hooks/use-map-sync.ts` - Sync selected listing between map and list
- `lib/utils/mapbox-utils.ts` - Placeholder utils (lat/lng bounds, clustering logic)

**Key Changes:**
- Route: `app/(landing)/directory/map`
- Left panel: map placeholder (no Mapbox token yet)
- Right panel: list of listings synced with map selection
- Click listing in list → highlight marker; click marker → scroll list and show detail
- Show mock clustering (visual only, no Mapbox)
- Lazy-load Mapbox only if token is present (feature flag check)

**Success Criteria:**
- List↔map selection sync works
- Mobile-first responsive layout (list stacked on mobile, side-by-side on desktop)
- Map placeholder renders without Mapbox token
- No performance regressions on mock data

---

### Stack 7: Feature Flags & Convex Integration
**Task:** 1.6, 2.1, 2.2, 2.3, 2.4  
**Goal:** Define backend schema, queries/mutations, and toggle mock → Convex via feature flags  
**Files:**
- `convex/schema.ts` - Add tables: listings, categories, approvals, owner_roles
- `convex/listings.ts` - Query: search listings, detail; Mutation: create/update/delete (owner-gated)
- `convex/approvals.ts` - Mutation: approve/reject; Query: pending queue (admin-gated)
- `convex/categories.ts` - Query: list categories; Mutation: CRUD (admin-gated)
- `convex/auth.ts` - Helper: verify owner, verify admin
- `lib/hooks/use-listings-live.ts` - Hook to switch between mock and Convex via feature flag
- `lib/hooks/use-approvals-live.ts` - Admin hook with live data
- `lib/config/feature-flags.ts` - Feature flag: `BELIZE_USE_LIVE_DATA` (default: false)
- `.env.local` (example) - Add feature flag config

**Key Changes:**
- Convex schema enforces roles via `useUser()` helper and `ctx.viewer` checks
- Owners can only edit their own listings
- Admins can approve/reject and manage categories
- Server-side validation (field lengths, lat/lng bounds, image count)
- Rate limiting: implement with simple in-memory counter (log + reject if threshold exceeded)
- Feature flag in `lib/config` allows safe toggle between mock and live data
- All UI hooks accept mock data as fallback; check feature flag to switch source
- Logging: basic console logs for approval actions and rate limit hits (later: structured logging)

**Success Criteria:**
- Convex schema compiles and syncs
- Owner mutations enforce ownership
- Admin mutations enforce admin role
- Feature flag correctly toggles data source
- No UI changes needed to switch backends
- Rate limiting prevents abuse

---

### Stack 8: Security, Validation & QA Hardening
**Task:** 3.1, 3.2, 3.3, 4.1, 4.2, 4.3  
**Goal:** Enforce validation, accessibility, rate limits, and pass all checks  
**Files:**
- `convex/validators.ts` - Centralized validation functions (field lengths, bounds, counts)
- `lib/validations/listing.ts` - Enhanced Zod schema with server-side rules
- `lib/utils/rate-limit.ts` - Rate limiter implementation (per-user, per-IP tracking)
- `lib/a11y/focus-management.ts` - Focus trap, focus restoration utilities
- `components/directory/*.tsx` - Add keyboard navigation, ARIA labels, focus states
- `app/globals.css` - Ensure color contrast, focus outlines

**Key Changes:**
- Server-side validation on all Convex mutations (field length, lat/lng bounds, image count ≤5)
- Rate limiting: 5 submissions per user per hour; logged with timestamp
- Accessibility audit: keyboard nav (Tab, Enter, Escape), ARIA labels, focus states, color contrast (WCAG AA)
- Run `npm run lint` and fix all issues
- Run `npm run build` successfully
- Create deterministic demo fixtures covering: loading, empty, populated, error, approved, rejected states

**Success Criteria:**
- All validation passes (no bad data can be submitted)
- Rate limit prevents spam (logs violations)
- Keyboard-only navigation works through all flows
- Color contrast ≥4.5:1 (WCAG AA)
- `npm run lint` and `npm run build` pass with no errors
- Demo fixtures are reproducible and cover all states

---

## Implementation Order & Dependencies

### Sequential Flow
1. **Stack 1** provides types and mock data for all downstream stacks
2. **Stack 2** demonstrates public discovery without backend integration
3. **Stacks 3–5** depend on Stacks 1–2, worked in **parallel** after Stack 2 is approved
4. **Stack 6** depends on Stacks 2–5 (list-view, detail, and other UIs complete)
5. **Stack 7** depends on Stacks 1–6 (adds Convex backend)
6. **Stack 8** final pass: validation, a11y, rate limits (depends on all prior stacks)

### Parallel Development Window
**After Stack 2 is merged to feature branch:**
- Developer A: Works on Stack 3 (Search & Detail)
- Developer B: Works on Stack 4 (Owner Dashboard)
- Developer C: Works on Stack 5 (Admin Approvals)
- All 3 stacks can progress independently; merge sequentially as they're approved

---

## Graphite Setup & Submission Workflow

### Initial Setup

1. **Create and checkout feature branch:**
   ```bash
   git checkout main
   git pull origin main
   git checkout -b feature/belize-directory
   ```

2. **Initialize Graphite on this branch:**
   ```bash
   gt init
   # Select main as trunk branch when prompted
   ```

3. **Verify setup:**
   ```bash
   gt log short
   # Should show: feature/belize-directory (current) as child of main
   ```

### Creating Stacks (Sequential Phase)

**Developer creating Stacks 1–2:**

```bash
# Stack 1: Mock Data & Types
gt create -am "feat(belize): Add mock data fixtures and types"

# Stack 2: Public Homepage
gt create -am "feat(belize): Public UI - list discovery homepage"

# Submit both stacks for review
gt submit --stack --reviewers @team
```

After Stack 2 is approved and merged to `feature/belize-directory`:

```bash
# Sync to pull Stack 2 into feature/belize-directory
gt sync
```

### Creating Stacks (Parallel Phase)

**Developer A - Stack 3:**
```bash
gt checkout feature/belize-directory
gt pull  # Ensure Stack 2 is merged
gt create -am "feat(belize): Public UI - search and detail pages"
gt submit
```

**Developer B - Stack 4:**
```bash
gt checkout feature/belize-directory
gt pull  # Ensure Stack 2 is merged
gt create -am "feat(belize): Owner UI - submissions and dashboard"
gt submit
```

**Developer C - Stack 5:**
```bash
gt checkout feature/belize-directory
gt pull  # Ensure Stack 2 is merged
gt create -am "feat(belize): Admin UI - approval queue and categories"
gt submit
```

**Merging stacks 3–5 sequentially:**
```bash
# After Stack 3 is approved:
gt checkout feature/belize-directory
gt merge <stack-3-branch>  # or use GitHub to merge PR

# After Stack 4 is approved:
gt checkout feature/belize-directory
gt merge <stack-4-branch>

# After Stack 5 is approved:
gt checkout feature/belize-directory
gt merge <stack-5-branch>

# Sync all stacks to keep everyone up-to-date
gt sync
```

### Creating Stacks (Final Phase)

**After all Stacks 1–5 are merged to feature/belize-directory:**

```bash
# Stack 6: Map View
gt checkout feature/belize-directory
gt sync
gt create -am "feat(belize): Map View - list↔map sync integration"
gt submit

# (After approved)
gt checkout feature/belize-directory
gt sync

# Stack 7: Convex Integration
gt create -am "feat(belize): Feature flags and Convex integration"
gt submit

# (After approved)
gt checkout feature/belize-directory
gt sync

# Stack 8: Security & Hardening
gt create -am "feat(belize): Security, validation, and accessibility hardening"
gt submit
```

### Final Merge to Main

Once all 8 stacks are approved and merged to `feature/belize-directory`:

```bash
# Option 1: GitHub UI (Recommended)
# Go to GitHub, create PR: feature/belize-directory → main
# Review + Merge

# Option 2: Git + Graphite
gt checkout main
git pull origin main
git merge feature/belize-directory
git push origin main
```

---

## Key Design Decisions

1. **Mock-Data-First:** All UI built against mock data first; Convex integration happens in Stack 7 behind a feature flag.
2. **Component Isolation:** Each stack introduces focused components with minimal cross-dependencies.
3. **Type Safety:** Stack 1 establishes shared types used by all downstream stacks.
4. **Feature Flags:** Stack 7 adds toggles to swap data sources without UI refactors.
5. **Lazy-Load Mapbox:** Map View loads Mapbox token lazily; falls back gracefully if not available.
6. **Role-Based Access:** Owner/Admin routes protected via Clerk; Convex mutations enforce server-side checks.

---

## Testing & Validation Checklist

- [ ] Stack 1: Types compile, mock data is reusable and deterministic
- [ ] Stack 2: Homepage renders, responsive on mobile, `npm run lint` + `npm run build` pass
- [ ] Stack 3: Search/filter works, infinite scroll functional, detail page complete
- [ ] Stack 4: Form validation client-side, status flow clear, localStorage persistence works
- [ ] Stack 5: Approval workflow intuitive, category CRUD works, admin role enforced
- [ ] Stack 6: List↔map sync works, no Mapbox required, responsive layout
- [ ] Stack 7: Convex mutations enforce roles, feature flag toggles backends, rate limiting active
- [ ] Stack 8: All validation passes, a11y audit complete, no console errors, `npm run lint` + `npm run build` pass

---

## Open Questions (Resolved During Implementation)

1. **City/Area Taxonomy:** Source and canonical list?
   - *Resolve in Stack 5 when building category manager*

2. **Image Storage:** Post-mock approach (limits, EXIF removal, CDN)?
   - *Resolve in Stack 7 when integrating Convex; consider Vercel Blob or Cloudinary*

3. **Re-Approval Policy:** Which edits trigger re-approval?
   - *Resolve in Stack 7: Define field-level triggers (e.g., location, category changes require re-approval)*

4. **Mapbox Token Management:** How to handle token in production?
   - *Resolve in Stack 6: Store in Convex env; feature flag gates rendering; fall back gracefully if missing*

---

## Rollout Timeline (Estimated)

- **Stack 1–2:** 2–3 days (foundation + homepage)
- **Stacks 3–5:** 3–4 days (parallel work on search, owner, admin UIs)
- **Stack 6:** 1–2 days (map sync)
- **Stack 7:** 2–3 days (Convex integration + feature flag)
- **Stack 8:** 1–2 days (hardening + a11y)

**Total:** ~2–3 weeks for end-to-end MVP

---

## Notes

- This plan assumes `main` is stable and ready for stack merges.
- Each stack is self-contained; review time should be ~1–2 hours per PR.
- After each stack merges, run `gt sync` to keep dependent stacks up-to-date.
- If conflicts arise during merge, resolve and run `gt continue` to sync downstack branches.
