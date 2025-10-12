# 🏗️ System Architecture

## 📐 Overview

Starter.diy is a full-stack SaaS template built on Next.js 15 (App Router) with Clerk for authentication, Clerk Billing for subscriptions, and Convex for a real-time, serverless backend. It enforces protected routes via middleware, syncs users and payment attempts by webhook into Convex, and ships a modern UI using TailwindCSS v4 and shadcn/ui.

Project file tree (key paths):

```
Starter-app-template/
├── app/
│   ├── (landing)/
│   │   ├── animated-list-custom.tsx
│   │   ├── call-to-action.tsx
│   │   ├── cpu-architecture.tsx
│   │   ├── faqs.tsx
│   │   ├── features-one.tsx
│   │   ├── footer.tsx
│   │   ├── header.tsx
│   │   ├── hero-section.tsx
│   │   ├── page.tsx
│   │   ├── table.tsx
│   │   └── testimonials.tsx
│   ├── dashboard/
│   │   ├── payment-gated/
│   │   │   └── page.tsx
│   │   ├── app-sidebar.tsx
│   │   ├── chart-area-interactive.tsx
│   │   ├── data-table.tsx
│   │   ├── data.json
│   │   ├── layout.tsx
│   │   ├── loading-bar.tsx
│   │   ├── nav-documents.tsx
│   │   ├── nav-main.tsx
│   │   ├── nav-secondary.tsx
│   │   ├── nav-user.tsx
│   │   ├── page.tsx
│   │   ├── section-cards.tsx
│   │   └── site-header.tsx
│   ├── favicon.ico
│   ├── globals.css
│   ├── layout.tsx
│   └── not-found.tsx
├── components/
│   ├── ui/
│   ├── ConvexClientProvider.tsx
│   ├── custom-clerk-pricing.tsx
│   ├── logo.tsx
│   ├── mode-toggle.tsx
│   └── theme-provider.tsx
├── convex/
│   ├── _generated/
│   ├── auth.config.ts
│   ├── http.ts
│   ├── paymentAttempts.ts
│   ├── paymentAttemptTypes.ts
│   ├── schema.ts
│   └── users.ts
├── lib/
│   └── utils.ts
├── middleware.ts
├── next.config.ts
├── public/
├── README.md
├── package.json
├── tsconfig.json
├── .env.example
├── components.json
└── docs/
    └── core/
```

## 🏛️ Technology Stack

### Frontend
- Next.js 15 (App Router, React 19)
- TailwindCSS v4
- shadcn/ui + Radix UI
- Framer Motion / Motion primitives
- Recharts, Lucide, Tabler Icons
- next-themes (dark/light)

### Backend
- Convex (queries, mutations, real-time DB)
- Clerk (auth)
- Clerk Billing (subscriptions/payments)
- Svix (webhook verification)

### Database
- Convex managed data store
  - Tables: `users`, `paymentAttempts`

### Infrastructure
- Vercel for deployment
- Convex cloud for backend functions and data
- Environment variables via `.env.local` (Next) and Convex dashboard

## 🔄 System Components

### Component 1: Frontend App (Next.js)
- Description: App Router-based UI with landing, dashboard, and payment-gated areas.
- Responsibilities:
  - Public landing and pricing
  - Protected dashboard (`/dashboard(.*)`)
  - Theme, UI components, animations
- Dependencies:
  - Clerk (session/UI)
  - Convex client
  - Tailwind/shadcn/ui

### Component 2: Backend & Integrations (Convex + Clerk)
- Description: Convex handles data and server-side logic; Clerk manages auth; Svix verifies webhooks.
- Responsibilities:
  - HTTP webhook endpoint `/clerk-users-webhook` (convex/http.ts)
  - User sync (convex/users.ts)
  - Payment attempts persistence (convex/paymentAttempts.ts)
  - Schema definition (convex/schema.ts)
- Dependencies:
  - `CLERK_WEBHOOK_SECRET` for signature verification
  - Clerk JWT template “convex”
  - Convex environment variables

## 📊 Data Flow

1) Auth flow
- User signs in via Clerk → Clerk session cookie set.
- Next middleware (`middleware.ts`) protects `/dashboard(.*)` using `auth.protect()`.
- Client components call Convex queries with Clerk-authenticated identity.

2) User sync
- Clerk emits `user.created | user.updated | user.deleted`.
- Webhook hits `/clerk-users-webhook` → Svix verification.
- Convex internal mutation upserts or deletes user in `users` table (indexed by `externalId` = Clerk ID).

3) Billing flow
- Clerk emits `paymentAttempt.updated`.
- Webhook transforms payload (`transformWebhookData`) and upserts into `paymentAttempts` (indexed by `payment_id`) and links to `users.userId` if present.

## 🔐 Security Architecture

- Clerk session-based auth with route protection via middleware.
- JWT template “convex” in Clerk ensures server-side identity for Convex.
- Webhook signature verification with Svix using `CLERK_WEBHOOK_SECRET`.
- Internal Convex mutations are not exposed to clients.
- Least-privilege environment variable usage; no secrets in client code.

## 🚀 Deployment Architecture

- Strategy: Deploy Next.js app to Vercel; Convex functions/data run on Convex cloud.
- Environment setup:
  - Next.js: `.env.local` with Clerk and Convex client vars
  - Convex dashboard: `CLERK_WEBHOOK_SECRET`, `NEXT_PUBLIC_CLERK_FRONTEND_API_URL`
- Scaling:
  - Vercel auto-scales stateless frontend
  - Convex scales queries/mutations and real-time sync automatically
  - Webhooks are idempotently handled to avoid duplicates

---

*Last updated: 2025-10-08*
