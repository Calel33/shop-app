# 🛠️ Development Guide

## 🚀 Getting Started

### Prerequisites

- Node.js 18+
- Clerk account (auth + billing)
- Convex account
- Vercel account (recommended for deployment)

### Installation

1. Install dependencies
   ```bash
   npm install
   ```
2. Copy environment template
   ```bash
   cp .env.example .env.local
   ```
3. Initialize Convex (prompts and config)
   ```bash
   npx convex dev
   ```

### Environment Setup

1. Set Clerk keys in `.env.local`:
   - `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`
   - `CLERK_SECRET_KEY`
   - `NEXT_PUBLIC_CLERK_FRONTEND_API_URL` (from Clerk JWT template “convex”)
   - Optional redirect URLs for sign-in/up fallbacks/force
2. Configure Convex dashboard environment:
   - `CLERK_WEBHOOK_SECRET` (from Clerk webhooks page)
   - `NEXT_PUBLIC_CLERK_FRONTEND_API_URL`
3. Create Clerk webhook endpoint:
   - URL: `<your-app-origin>/clerk-users-webhook`
   - Events: `user.created`, `user.updated`, `user.deleted`, `paymentAttempt.updated`

## 🏗️ Project Structure

```
app/
  (landing)/         # Public landing, pricing
  dashboard/         # Protected dashboard
    payment-gated/   # Subscription-only content
  layout.tsx
  not-found.tsx
components/
  ui/                # shadcn/ui components
  custom-clerk-pricing.tsx
convex/
  schema.ts
  http.ts            # /clerk-users-webhook
  users.ts
  paymentAttempts.ts
  paymentAttemptTypes.ts
middleware.ts        # Clerk route protection
```

## 🔧 Development Workflow

### 1. Run backends locally
- Start Convex dev server:
  ```bash
  npx convex dev
  ```

### 2. Run Next.js app
- Start the app with Turbopack:
  ```bash
  npm run dev
  ```

### 3. Implement and verify
- Add UI in `app/` and `components/`
- Add data logic in `convex/`
- Verify auth on `/dashboard` and subscription gating on `/dashboard/payment-gated`

## 🧪 Testing

### Running Tests

```bash
# No tests configured yet; add your preferred test runner.
```

### Test Structure

- Recommended: unit tests for Convex functions, integration tests for webhook handling, and E2E tests for auth + gated routes.

## 📦 Building & Deployment

### Local Development

```bash
npm run dev
```

### Production Build

```bash
npm run build
npm start
```

### Deployment

- Deploy to Vercel; set environment variables in Vercel dashboard.
- Ensure Convex project is configured and webhook URL is reachable.

## 📋 Coding Standards

- TypeScript-first; keep types strict and explicit
- Lint with Next.js ESLint:
  ```bash
  npm run lint
  ```
- Keep secrets out of client code; use env variables properly
- Match existing component patterns and Tailwind utility conventions

## 🔍 Debugging

- Next.js console/server logs during `npm run dev`
- Convex function logs via Convex dashboard or terminal where `npx convex dev` runs
- Verify webhook signature issues by checking 400 responses and Svix header presence

## 📚 Resources

- Next.js: https://nextjs.org/docs
- Clerk: https://clerk.com/docs
- Convex: https://docs.convex.dev
- Svix: https://docs.svix.com

---

*Last updated: 2025-10-08*
