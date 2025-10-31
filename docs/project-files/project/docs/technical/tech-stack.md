 # Tech Stack — Local Business Directory (Belize)
 
 Date: 2025-10-23
 
 ## Frontend
 - Next.js 15 (App Router, RSC), Turbopack, TypeScript
 - TailwindCSS v4 (token-only), shadcn/ui (Radix), Framer Motion
 - Mapbox GL JS (enabled on dedicated map view post‑MVP hookup)
 
 ## Backend & Services
 - Convex (real-time DB + serverless functions)
   - Collections (later): listings, categories, users/owners, approvals
 - Clerk (auth + roles: public, owner, admin); Clerk Billing deferred
 - Svix (webhooks) for Clerk/Convex sync (later)
 
 ## Infrastructure
 - Vercel (deploy, env mgmt), Feature flags (mock vs live data)
 - Logging/Monitoring (basic app-level to start)
 
 ## Environment Variables (placeholders)
 - NEXT_PUBLIC_MAPBOX_TOKEN=
 - CLERK_PUBLISHABLE_KEY=
 - CLERK_SECRET_KEY=
 - CONVEX_DEPLOYMENT=
 - CONVEX_SITE_URL=
 - WEBHOOK_SECRET_SVIX= (later)
 
 ## Integration Notes
 - Phase 1: mock JSON fixtures power all UI states
 - Phase 2: wire Convex queries/mutations; enable Mapbox on map view + owner pin placement
 - Protected routes with Clerk; owner/admin dashboards behind auth
 
