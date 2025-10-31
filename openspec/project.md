# Project Context

## Purpose
Production-ready SaaS starter built with Next.js 15, integrating Clerk for authentication and billing, and Convex for a real-time backend. Provides a polished landing, protected dashboard, and payment-gated content with minimal setup.

## Tech Stack
- Frontend: Next.js 15 (App Router, React 19), TypeScript, TailwindCSS v4, shadcn/ui (Radix), Framer Motion/Motion, Recharts
- Backend/Services: Convex (DB + functions), Clerk (Auth), Clerk Billing (Payments), Svix (webhooks)
- Tooling: Turbopack, ESLint (next lint), TypeScript

## Project Conventions

### Code Style
- TypeScript-first, strict types where practical
- Utility classes via Tailwind v4; prefer design tokens over hard-coded values
- Components are small, composable, and colocate logic by vertical slice
- Follow existing import/order patterns and naming as in codebase

### Architecture Patterns
- App Router with server and client components as appropriate
- Route protection via `middleware.ts` and Clerk
- Real-time data with Convex hooks (`useQuery`, `useMutation`)
- Webhook-driven sync for Clerk users and billing events (handled in Convex `http.ts`)

### Testing Strategy
- Unit/integration where applicable for Convex functions and critical UI logic
- Linting via `npm run lint`; CI should at minimum run build + lint
- Add tests alongside features (vertical slice) when adding non-trivial logic

### Git Workflow
- Default branch: `main`
- Feature branches from `main`; open PRs with concise scope
- Commit messages: imperative, focus on why; avoid committing secrets

## Domain Context
- Authentication and user provisioning handled by Clerk; Clerk user ID maps to `users.externalId` in Convex
- Subscription access controlled via Clerk Billing; payment-gated routes live under `app/dashboard/payment-gated`
- Pricing UI in `components/custom-clerk-pricing.tsx`

## Important Constraints
- Do not hard-code secrets; use env vars
- Keep files focused (≤500 lines, single responsibility)
- Maintain backwards compatibility of public routes and Convex schema
- Use design tokens/utilities; avoid inline arbitrary styles

## External Dependencies
- Clerk (auth, billing): requires `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`, `CLERK_SECRET_KEY`, redirect URLs, `NEXT_PUBLIC_CLERK_FRONTEND_API_URL`
- Convex: `CONVEX_DEPLOYMENT`, `NEXT_PUBLIC_CONVEX_URL`; webhook secret `CLERK_WEBHOOK_SECRET` in Convex dashboard
- Webhooks: Configure Clerk events (`user.*`, `paymentAttempt.updated`) to `/api/clerk-users-webhook`
