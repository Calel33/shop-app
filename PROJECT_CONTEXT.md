# PROJECT_CONTEXT.md - Complete Project Understanding

> **Purpose:** This document is the single source of truth for the project. Reference this when onboarding AI agents or when you need a quick refresh on project goals, architecture, and current status. Update this whenever major decisions or milestones change.

---

## 1. Executive Summary

**Project Name:** Starter.diy (Elite Next.js SaaS Starter Kit) + **Belize Directory MVP**

**Status:** In development; adding Belize Directory feature to existing SaaS starter

**What We're Building:**
- A production-ready SaaS starter template with authentication, real-time database, and payments
- **NEW:** Belize Directory MVP — a mobile-first local business directory with public discovery, owner submissions, and admin approvals

**Core Value Proposition:**
- Eliminate weeks of integration work with a complete, production-ready SaaS template
- Add a trustworthy, unified directory for discovering local Belize businesses
- Focus on list-first UX, manual approval for data quality, and lazy-loaded map view

---

## 2. Project Structure & Key Files

### Root-Level Organization
```
shop-app/
├── CLAUDE.md                          # Development guidelines & code rules
├── AGENTS.md                          # AI agent behavior rules
├── PRIME_CONTEXT.md                   # Quick reference for new sessions
├── PROJECT_CONTEXT.md                 # THIS FILE - comprehensive project understanding
├── STACK_PLAN.md                      # 8-stack Graphite plan for Belize MVP
├── package.json                       # Dependencies (Next.js 15, Convex, Clerk, etc.)
├── tsconfig.json                      # TypeScript configuration
├── next.config.ts                     # Next.js configuration
├── middleware.ts                      # Auth protection (Clerk)
├── app/                               # Next.js 15 App Router
├── components/                        # React components (UI, forms, custom)
├── convex/                            # Convex backend (schema, queries, mutations, webhooks)
├── lib/                               # Utilities, hooks, constants
├── public/                            # Static assets
├── docs/                              # Documentation (design system, architecture, etc.)
├── openspec/                          # OpenSpec proposals (Belize MVP specs)
└── .env.example                       # Environment variables template
```

### Critical Files
| File | Purpose |
|------|---------|
| `CLAUDE.md` | **MUST READ.** Coding rules, patterns, token-only design, file size limits, etc. |
| `app/layout.tsx` | Root layout with Clerk + Convex providers |
| `middleware.ts` | Route protection via Clerk authentication |
| `convex/schema.ts` | Database schema (users, paymentAttempts, + future listings/approvals) |
| `convex/http.ts` | Webhook router for Clerk events |
| `.env.example` | Template for environment setup |
| `docs/core/APP_ARCHITECTURE.md` | System architecture, auth flow, webhooks |
| `docs/core/DATA_MODEL.md` | Entity relationships, indexes, service layer mapping |
| `openspec/changes/add-belize-directory-mvp/` | Belize MVP proposal, design, and tasks |

---

## 3. Tech Stack (Current + MVP)

### Frontend
- **Next.js 15** - React framework with App Router, Turbopack
- **React 19** - Latest React with compiler optimizations
- **TailwindCSS v4** - Utility-first CSS framework
- **shadcn/ui** - Modern, accessible component library (uses Radix UI primitives)
- **TypeScript** - Type safety throughout
- **Framer Motion** - Smooth animations and transitions
- **Lucide React & Tabler Icons** - Icon libraries
- **Recharts** - Data visualization components
- **next-themes** - Dark/light theme support

### Backend & Data
- **Convex** - Real-time database, serverless functions, WebSocket sync
- **Clerk** - Authentication, user management, billing integration
- **Clerk Billing** - Subscription payments and plans
- **Svix** - Webhook verification and delivery

### Development Tools
- **TypeScript** - Type system
- **ESLint** - Code linting
- **Turbopack** - Fast build tool
- **Vercel** - Deployment platform

### Newly Added (Belize MVP)
- **Mapbox** (future) - Map view with clustering and markers (lazy-loaded)
- **Zod** (if needed) - Schema validation for forms

---

## 4. Authentication & Authorization

### Current System (Starter Kit)
1. **Clerk** manages all authentication (sign-in, sign-up, social logins)
2. **Middleware** (`middleware.ts`) protects routes:
   - Public: `app/(landing)/*`
   - Protected: `app/dashboard/*` (requires sign-in)
   - Subscription-gated: `app/dashboard/payment-gated/*` (requires active subscription)
3. **JWT Token** - Clerk generates JWT with "convex" template for Convex auth
4. **User Sync** - Webhooks (`convex/http.ts`) sync Clerk users to Convex `users` table

### Belize MVP Additions (Stack 7 onwards)
- **Owner Role** - Users who can submit and edit listings
- **Admin Role** - Users who can approve/reject listings and manage categories
- **Authorization Checks:**
  - Owners can only edit their own listings
  - Admins can only access `/dashboard/admin/*` routes
  - Server-side mutations enforce role checks in Convex

---

## 5. Database Schema & Data Model

### Current Tables (Starter Kit)

**users**
```typescript
{
  _id: Id<"users">,           // Primary key
  name: string,
  externalId: string,         // Clerk user ID (unique)
}
```
- **Index:** `byExternalId(externalId)` - Fast lookup from Clerk ID

**paymentAttempts**
```typescript
{
  _id: Id<"paymentAttempts">,
  payment_id: string,         // Unique
  statement_id: string,
  status: string,             // e.g., "succeeded", "failed"
  userId?: Id<"users">,       // Foreign key to users
  payer: {                    // Payer info from Clerk
    user_id: string,
    email: string,
    first_name: string,
    last_name: string
  },
  payment_source: {
    card_type: string,
    last4: string
  },
  subscription_items: Array<{
    amount: number,
    plan: string,
    status: string,
    period_start: number,
    period_end: number
  }>,
  totals: {
    grand_total: number,
    subtotal: number,
    tax_total: number
  },
  billing_date: number,       // Timestamp
  created_at: number,
  updated_at: number,
  paid_at?: number,
  failed_at?: number
}
```
- **Indexes:** `byPaymentId`, `byUserId`, `byPayerUserId` - Fast lookups for billing queries

### Future Tables (Belize MVP - Stack 7)

**listings** (new)
```typescript
{
  _id: Id<"listings">,
  title: string,
  description: string,
  ownerId: Id<"users">,       // FK to users
  categoryId: Id<"categories">,
  images: Array<{ url: string, alt: string }>,  // Max 5
  location: {
    lat: number,
    lng: number,
    address: string,
    city: string,
    area?: string
  },
  contact: {
    email?: string,
    phone?: string,
    website?: string
  },
  status: "draft" | "pending" | "approved" | "rejected",
  tags: Array<string>,
  createdAt: number,
  updatedAt: number,
  approvedAt?: number,
  rejectionReason?: string
}
```
- **Indexes:** `byOwnerId`, `byStatus`, `byCategory`

**categories** (new)
```typescript
{
  _id: Id<"categories">,
  name: string,              // e.g., "Restaurant", "Retail"
  slug: string,
  description?: string,
  icon?: string,
  createdAt: number
}
```

**approvals** (new)
```typescript
{
  _id: Id<"approvals">,
  listingId: Id<"listings">,
  adminId: Id<"users">,
  action: "approved" | "rejected",
  reason?: string,
  previousStatus: string,
  newStatus: string,
  approvedAt: number
}
```

---

## 6. Belize Directory MVP - Feature Overview

### What It Does
A mobile-first local business directory for Belize with three core flows:

1. **Public Discovery**
   - Homepage: Featured categories, latest listings, map preview
   - Search: Filter by category, distance, rating; infinite scroll
   - Detail: Full listing info, contact, location, owner info

2. **Owner Submissions**
   - Dashboard: View own listings with status
   - Create/Edit: Form with validation (title, description, category, images ≤5, location, contact)
   - Submit for Approval: Owner submits, admin reviews

3. **Admin Approvals**
   - Review Queue: Pending listings with preview
   - Approve/Reject: With optional reason
   - Category Management: Create/edit/delete categories and tags

4. **Map View**
   - Dedicated route with list sync
   - Click listing → highlight marker; click marker → scroll list
   - Lazy-load Mapbox; fall back gracefully if token missing
   - Show clustering on map

### Implementation Phases

**Phase 1: Mock Data (Stacks 1–6)**
- All UIs built against mock, deterministic data
- No Convex backend yet
- No Mapbox token needed
- Feature flag: `BELIZE_USE_LIVE_DATA=false` (default)

**Phase 2: Convex Integration (Stack 7)**
- Define schema; implement queries/mutations
- Owner/admin authorization checks
- Feature flag: `BELIZE_USE_LIVE_DATA=true` (toggle to enable)

**Phase 3: Hardening (Stack 8)**
- Server-side validation (field lengths, bounds, image count)
- Rate limiting (5 submissions/user/hour)
- Accessibility audit (keyboard nav, ARIA labels, color contrast)

### Stacked PR Plan (See STACK_PLAN.md for Details)

```
Stack 1: Mock Data & Types
  ↓
Stack 2: Public Homepage
  ├─ Stack 3: Search & Detail (parallel)
  ├─ Stack 4: Owner Dashboard (parallel)
  └─ Stack 5: Admin Approvals (parallel)
  ↓
Stack 6: Map View
  ↓
Stack 7: Convex Integration & Feature Flags
  ↓
Stack 8: Security & Accessibility Hardening
```

---

## 7. Webhook Integration & Real-Time Sync

### Current (Starter Kit)
**Endpoint:** `POST /api/clerk-users-webhook` (handled by Convex HTTP router at `convex/http.ts`)

**Events Handled:**
| Event | Action |
|-------|--------|
| `user.created` | Call `users.upsertFromClerk()` → sync new user to Convex |
| `user.updated` | Call `users.upsertFromClerk()` → update user data |
| `user.deleted` | Call `users.deleteFromClerk()` → remove user |
| `paymentAttempt.updated` | Call `paymentAttempts.savePaymentAttempt()` → track payment |

**Webhook Security:** Svix verifies signature using `CLERK_WEBHOOK_SECRET`

### Future (Belize MVP)
- No additional webhooks needed for MVP (all data driven by UI interactions)
- Later: Could add image processing webhooks (EXIF removal, CDN optimization)

---

## 8. Environment Variables

### Required for Local Development

**.env.local** (copy from `.env.example`):
```bash
# Clerk Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
CLERK_SECRET_KEY=sk_test_...
NEXT_PUBLIC_CLERK_FRONTEND_API_URL=https://...clerk.accounts.dev

# Clerk Redirects
NEXT_PUBLIC_CLERK_SIGN_IN_FORCE_REDIRECT_URL=/dashboard
NEXT_PUBLIC_CLERK_SIGN_UP_FORCE_REDIRECT_URL=/dashboard
NEXT_PUBLIC_CLERK_SIGN_IN_FALLBACK_REDIRECT_URL=/dashboard
NEXT_PUBLIC_CLERK_SIGN_UP_FALLBACK_REDIRECT_URL=/dashboard

# Convex Database
CONVEX_DEPLOYMENT=prod:...
NEXT_PUBLIC_CONVEX_URL=https://....convex.cloud/

# Belize MVP Feature Flag (Stack 7+)
NEXT_PUBLIC_BELIZE_USE_LIVE_DATA=false    # false = mock, true = Convex

# Mapbox (Stack 6+, optional)
NEXT_PUBLIC_MAPBOX_TOKEN=pk_...          # Optional; lazy-loaded in map view
```

### In Convex Dashboard (Environment Variables)
```bash
CLERK_WEBHOOK_SECRET=whsec_...
NEXT_PUBLIC_CLERK_FRONTEND_API_URL=https://...clerk.accounts.dev
NEXT_PUBLIC_BELIZE_USE_LIVE_DATA=false   # Mirror from .env.local
```

---

## 9. Development Workflow

### Starting Development

1. **Install Dependencies:**
   ```bash
   npm install
   # or: bun install (if using Bun)
   ```

2. **Set Environment Variables:**
   ```bash
   cp .env.example .env.local
   # Fill in your Clerk and Convex credentials
   ```

3. **Start Convex (Required):**
   ```bash
   npx convex dev
   # or: bunx convex dev
   # Runs on http://localhost:3210 by default
   ```

4. **Start Next.js (In Another Terminal):**
   ```bash
   npm run dev
   # Runs on http://localhost:3000
   ```

### Key Commands

| Command | Purpose |
|---------|---------|
| `npm run dev` | Start Next.js dev server with Turbopack |
| `npx convex dev` | Start Convex backend and dashboard |
| `npm run build` | Build for production |
| `npm start` | Start production server |
| `npm run lint` | Run ESLint; fix issues |
| `npm run format` | Format code (if configured) |

### Feature Branch Workflow (Belize MVP)

All Belize Directory work happens on `feature/belize-directory` branch using Graphite stacked PRs:

```bash
# Create feature branch
git checkout main
git pull origin main
git checkout -b feature/belize-directory

# Initialize Graphite (if not already done)
gt init  # Select main as trunk

# Create Stack 1
gt create -am "feat(belize): Add mock data fixtures and types"

# Create Stack 2 (and submit both for review)
gt create -am "feat(belize): Public UI - list discovery homepage"
gt submit --stack --reviewers @team
```

See `STACK_PLAN.md` for complete stack submission workflow, parallel work instructions, and final merge to main.

### Installing shadcn/ui Components (From CLAUDE.md)
```bash
# ALWAYS use bunx (not npx)
bunx --bun shadcn@latest add button card drawer
# If dependency fails, manually install:
bun install <dependency-name>
```

---

## 10. Code Quality & Guidelines

### Design System (Token-Only Rule)
- **NEVER** use hard-coded style values
- **ALWAYS** use design system tokens for: colors, typography, spacing, shadows, borders
- Token location: `docs/Design-system/design.md`
- CSS variables defined in `app/globals.css`

**Example:**
```typescript
// ✅ GOOD - Use design tokens
<button className="bg-primary text-primary-foreground p-md rounded-lg">
  
// ❌ BAD - Hard-coded values
<button className="bg-#3b82f6 text-white p-4 rounded-8px">
```

### File Organization
- **Max file length:** 500 lines (strictly enforced)
- **One responsibility per file**
- **Modular design:** Break large files into smaller modules
- **Relative imports:** Use relative paths within domains

**Example Structure:**
```
components/
├── directory/
│   ├── listing-card.tsx        # Single component
│   ├── listings-grid.tsx       # Composite
│   └── index.ts                # Barrel export
├── ui/                         # shadcn/ui
└── index.ts
```

### Code Patterns
- **Composition over inheritance**
- **Fail-fast validation** - Validate early, fail explicitly
- **Vertical slice architecture** - Complete features in isolated slices
- **React 19 compiler** - Trust compiler for optimizations; only memoize if profiling shows issues

### TypeScript & Type Safety
- **Full TypeScript throughout** - No `any` types unless absolutely necessary
- **Define types at domain level** - E.g., `lib/types/directory.ts`
- **Export from `index.ts`** for clean imports

---

## 11. Project Conventions & Patterns

### File Naming
- **Components:** PascalCase (`ListingCard.tsx`, `SearchHeader.tsx`)
- **Hooks:** camelCase with `use` prefix (`useListings.ts`, `useMapSync.ts`)
- **Utilities:** camelCase (`searchUtils.ts`, `formatters.ts`)
- **Types:** Export from `types/domain.ts` (e.g., `types/directory.ts`)

### Component Structure
```typescript
// Server component (default)
export default async function Page() {
  const data = await fetchData();
  return <ClientComponent data={data} />;
}

// Client component (when needed)
"use client";

export function ClientComponent({ data }: Props) {
  return ...;
}
```

### Hooks with Mock/Live Data Toggle
```typescript
// lib/hooks/useListings.ts
export function useListings(query?: string) {
  const useLiveData = useFeatureFlag("BELIZE_USE_LIVE_DATA");
  
  if (useLiveData) {
    return useLiveListings(query);    // Convex hook
  }
  return useMockListings(query);       // Mock fixture
}
```

### Authorization Pattern (Stack 7+)
```typescript
// convex/listings.ts - Mutation
export const createListing = mutation({
  handler: async (ctx, args) => {
    const user = await ctx.auth.getUserIdentity();
    if (!user) throw new Error("Not authenticated");
    
    // Server-side validation
    validateListingFields(args);
    
    // Create listing
    return db.insert("listings", {
      ...args,
      ownerId: user._id,
      status: "pending"
    });
  }
});
```

---

## 12. Current Status & Next Steps

### What's Done (Starter Kit)
- ✅ Next.js 15 + App Router setup
- ✅ Clerk authentication + webhook sync
- ✅ Convex database + real-time queries
- ✅ Clerk Billing integration
- ✅ Landing page with pricing
- ✅ Protected dashboard
- ✅ Payment-gated content area
- ✅ TailwindCSS v4 + shadcn/ui

### What's Pending (Belize MVP)

**Stack 1–2:** Mock data, public homepage, search (ETA: 2–3 days)

**Stacks 3–5:** Owner UI, admin UI, detail page (ETA: 3–4 days, parallel work)

**Stack 6:** Map view integration (ETA: 1–2 days)

**Stack 7:** Convex schema, live data, feature flags (ETA: 2–3 days)

**Stack 8:** Validation, rate limits, accessibility (ETA: 1–2 days)

**Total MVP Timeline:** ~2–3 weeks

### Git Workflow
- **Branch Strategy:** Feature branch (`feature/belize-directory`) with Graphite stacked PRs
  - All stacks created on feature branch
  - Sequential and parallel work tracked with Graphite
  - Final merge: `feature/belize-directory` → `main`
- **Default Branch:** `main` (trunk)
- **Commit Style:** `feat(belize): ...`, `fix(belize): ...`, `refactor(...): ...`
- **PR Review:** Each stack is a PR reviewed against `feature/belize-directory`
- **Merge Strategy:** PRs merged to feature branch; parallel work sequenced as approved

---

## 13. Key Decision Points & Rationale

### Why Mock-Data-First?
- Decouples UI development from backend
- Allows parallel work (frontend can build while backend schema is designed)
- Easier to test edge cases with deterministic mock data
- Feature flag allows safe toggle to live data

### Why Feature Flags?
- MVP can ship with mock data; toggle to Convex when ready
- Safe rollback if Convex integration has issues
- Team can test both paths before committing to live data

### Why Mapbox Lazy-Load?
- Reduces bundle size and improves initial load
- Graceful fallback if token is missing or quota exceeded
- Map is secondary experience; list is primary

### Why Manual Approvals (Not Auto)?
- Ensures data quality for new directory
- Builds trust with users
- SLA target: 48 hours

---

## 14. Known Risks & Mitigations

| Risk | Mitigation |
|------|-----------|
| **Mapbox token quota exceeded** | Lazy-load; fall back to static map; implement cost controls |
| **Data model evolution** | Start minimal in MVP; add fields as MODIFIED deltas post-launch |
| **Image storage not defined** | Resolve in Stack 7; consider Vercel Blob or Cloudinary |
| **Re-approval policy unclear** | Define in Stack 7 which field edits trigger re-approval |
| **Rate limiting insufficient** | Stack 8 hardening; monitor abuse patterns |

---

## 15. How to Use This Document

**For AI Agents:**
- Start here when asked to work on the project
- Reference CLAUDE.md for coding rules
- Check STACK_PLAN.md for current task breakdown
- When in doubt, ask for clarification—don't assume

**For Team:**
- Update this doc when major decisions change
- Link to this in PR descriptions and issue templates
- Keep PRIME_CONTEXT.md as a quick ~100-line summary

**For New Developers:**
- Read this first
- Then read CLAUDE.md
- Then clone the repo and follow the "Starting Development" section above
- Reference `docs/core/APP_ARCHITECTURE.md` and `docs/core/DATA_MODEL.md` for deep dives

---

## 16. Quick Reference Links

| Document | Purpose |
|----------|---------|
| `CLAUDE.md` | Coding rules & patterns |
| `AGENTS.md` | AI agent behavior rules |
| `PRIME_CONTEXT.md` | Quick ~100-line summary |
| `STACK_PLAN.md` | 8-stack PR plan for Belize MVP |
| `README.md` | Public project overview |
| `docs/core/APP_ARCHITECTURE.md` | System architecture & auth flow |
| `docs/core/DATA_MODEL.md` | Database schema & relationships |
| `.env.example` | Environment variable template |
| `openspec/changes/add-belize-directory-mvp/` | MVP proposal & specs |

---

## 17. Contact & Questions

**If you're unclear about:**
- **Architecture:** Check `docs/core/APP_ARCHITECTURE.md`
- **Data model:** Check `docs/core/DATA_MODEL.md`
- **Coding style:** Check `CLAUDE.md`
- **Belize MVP scope:** Check `STACK_PLAN.md` or `openspec/changes/add-belize-directory-mvp/`
- **Project decisions:** Ask in this doc or refer to linked specs

---

**Last Updated:** 2025-10-31  
**Status:** MVP Planning Phase  
**Next Milestone:** Stack 1 (Mock Data & Types) - Ready to begin
