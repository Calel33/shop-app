<!-- OPENSPEC:START -->
# OpenSpec Instructions

These instructions are for AI assistants working in this project.

Always open `@/openspec/AGENTS.md` when the request:
- Mentions planning or proposals (words like proposal, spec, change, plan)
- Introduces new capabilities, breaking changes, architecture shifts, or big performance/security work
- Sounds ambiguous and you need the authoritative spec before coding

Use `@/openspec/AGENTS.md` to learn:
- How to create and apply change proposals
- Spec format and conventions
- Project structure and guidelines

Keep this managed block so 'openspec update' can refresh the instructions.

<!-- OPENSPEC:END -->

 # AGENTS.md
 
 A field guide for AI agents working on the Starter.diy project — an elite Next.js 15 SaaS starter kit combining Next.js, Convex, Clerk, and Clerk Billing. Follow this playbook to work safely, consistently, and productively.
 
 ## 1) Project Overview
 
 - Stack
   - Next.js 15 (App Router, React 19, Turbopack)
   - Convex (real-time DB + serverless functions)
   - Clerk (auth) + Clerk Billing (subscriptions)
   - Tailwind CSS v4 with custom UI components (shadcn-like in `components/ui/` and curated libraries)
   - TypeScript throughout
 - Core flows
   - Auth protection via `middleware.ts` and Clerk JWT config for Convex
   - Users synced to Convex via webhook handler in `convex/http.ts`
   - Subscription-gated features in `app/dashboard/payment-gated/` using pricing in `components/custom-clerk-pricing.tsx`
 - Key directories
   - `app/(landing)/*` public marketing pages
   - `app/dashboard/*` protected application shell and modules
   - `components/*` UI primitives and composition
   - `convex/*` schema, functions, webhooks, and auth config
   - `middleware.ts` route protection
 
 ## 2) Environment & Repo Basics
 
 - Node scripts (from `package.json`)
   - `npm run dev` — Next dev with Turbopack
   - `npm run build` — production build
   - `npm start` — production server
   - `npm run lint` — Next lint
 - Convex dev server (run in a second terminal)
   - `npx convex dev`
 - Required environment variables (set in `.env.local`)
   - `CONVEX_DEPLOYMENT`, `NEXT_PUBLIC_CONVEX_URL`
   - `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`, `CLERK_SECRET_KEY`
   - `NEXT_PUBLIC_CLERK_FRONTEND_API_URL` (from Clerk JWT template)
   - `CLERK_WEBHOOK_SECRET` (configured in Convex)
 - Default protection
   - `middleware.ts` protects `/dashboard(.*)`; update this when adding new protected areas
   - API routes under `/api` always run through middleware
 
 ## 3) Dev Rules & Code Conventions
 
 Authoritative rules synthesized from `.cursor/rules/system.md` and `.cursor/rules/designsystem.md`. Apply them rigorously.
 
 - Editing discipline
   - Read surrounding code before editing; double-check line numbers and paths
   - Preserve existing functionality and backwards compatibility
   - After edits, re-check impacted modules and run linters/tests
 - Code structure
   - One responsibility per file; keep files ≤ ~500 LOC
   - Modular by vertical slice; prefer composition over inheritance
   - Use relative imports and maintain consistent folder patterns
 - Principles
   - KISS, YAGNI, Component-first, Performance-by-default (let React 19 compiler work)
   - Fail-fast validation; break tasks into small units; validate design before build
 - UI & styling
   - Always implement UI using the design system tokens (colors, typography, spacing, radius, shadows)
   - No hard-coded styles; leverage existing tokens/components under `components/ui/` and curated libs
   
 - Behavior & safety
   - No assumptions or hallucinated functions; confirm paths and modules
   - Do not delete or modify core frameworks without explicit instruction
   - Avoid adding dependencies without checking existing ones
 - Integration checklist (run mentally before submitting changes)
   - Are all dependent systems updated (routing, state, types, styles, imports)?
   - Would this break in production due to isolation/misalignment?
   - Is end-to-end flow verified (happy path and error states)?
 - Workflow rule: never leave a system half-updated
   - Identify all readers/writers/dependents of changed data or APIs
   - Update all linked systems in the same change set; test end-to-end
 
 Concrete examples
 - Changing user roles? Update: Convex schema/types, middleware guards, UI conditions, and sync logic
 - Modifying an API response in Convex? Update: callers in React, Zod types, error handling, and any derived selectors
 - Adding a new dashboard section? Update: `middleware.ts` matcher if needed, nav components, route, data hooks


 
 ### System Rule: Pre-Task Research & RAG Tool Protocol
Before beginning any user coding task, you MUST first assess the situation using the following protocol:

Assess Task Complexity & Knowledge Gaps:
Ask yourself:

Complexity: "Is this a simple, well-defined task, or a complex one involving multiple components, scalability, or performance?"

Patterns & Examples: "Do I know the established, best-practice code patterns and have proven examples for this specific context?"

Specificity & Accuracy: "Is my knowledge of the required libraries, versions, and techniques specific and up-to-date?"

Make a Decision & Communicate Clearly:
Based on your assessment, follow one of these paths:

Path A: Simple Task & Confident Knowledge

Trigger: The task is straightforward and you have specific, best-practice knowledge.

Your Response: "This is a straightforward task. I can proceed with a standard implementation using established patterns. I will begin now."

Path B: Complex Task or Knowledge Gaps

Trigger: The task is complex, performance-sensitive, or you lack specific patterns/examples.

Your Response: "Given the complexity of this task, finding the optimal code patterns and proven examples is crucial for a robust implementation. I recommend we use the research tools to investigate:

'Best-practice architecture/patterns for [Specific Complex Aspect, e.g., managing state in a long-running process]'

'Code examples for [Specific Library/Task] that demonstrate scalability and error handling'
Should I proceed with this research?

Path C: Uncertain or Potentially Outdated

Trigger: You can complete the task, but suspect there may be a significantly better modern approach.

Your Response: "I can implement this with a standard approach. However, to ensure we use the most modern and efficient patterns, I suggest a quick research on:

'Current best-practice alternatives to [Older Library/Method] for [Task]'
Would you like me to investigate this first?

Act:

For Path A, proceed immediately.

For Paths B & C, you MUST await explicit user permission before using any RAG tools.


 
 ## 4) Agent Mode System
 
 Codified from `.cursor/rules/AGENT-MODE.md`.
 
 - Core rule: when the user references `@[agent-file]`, switch to that agent and follow its workflow exclusively
   1) Declare: “AGENT-NAME MODE ACTIVATED”
   2) Become: follow only that agent’s behaviors/tools
   3) No mixing: do not blend workflows across agents
 - Auto-selection keywords (shortcut guidance)
   - Vague → clarity-agent; review/security → code-reviewer; backend/API → backend-developer; frontend/UI → frontend-developer; performance → performance-optimizer; docs → documentation-specialist; planning → project-researcher-agent
 - Quick commands (conceptual)
   - `/agent` auto-selects an agent; `/multiagent` coordinates multiple; `/deeptask` runs a 5-phase parallel workflow
 - Multi-agent patterns
   - Vague → clarity-agent → implementation-agent → code-reviewer
   - Complex → prompt-assistant → implementation-agent → code-reviewer
   - Performance → code-archaeologist → performance-optimizer → code-reviewer
 - Protocol
   - Adopt identity fully; use that agent’s tools only; maintain project security context; handoff with a summary; track interactions for audit
 
 ## 5) Build / Run / Lint / Dev Servers
 
 Commands
 
 ```bash
 # App server
 npm run dev
 
 # Convex (required for DB, run in separate terminal)
 npx convex dev
 
 # Lint/build
 npm run lint
 npm run build
 
 # Production
 npm start
 ```
 
 Local auth protection
 
 ```ts
 // middleware.ts
 import { clerkMiddleware, createRouteMatcher } from '@clerk/nextjs/server'
 const isProtectedRoute = createRouteMatcher(['/dashboard(.*)'])
 export default clerkMiddleware(async (auth, req) => {
   if (isProtectedRoute(req)) await auth.protect()
 })
 ```
 
 ## 6) Data & APIs
 
 - Convex schema and functions
   - Schema: `convex/schema.ts`
   - User sync and CRUD: `convex/users.ts`
   - Payment tracking: `convex/paymentAttempts.ts`, `convex/paymentAttemptTypes.ts`
   - Webhooks: `convex/http.ts` (handles Clerk events, including `paymentAttempt.updated`)
   - Auth config for JWT: `convex/auth.config.ts`
 - Frontend data access
   - Use Convex client/provider in `components/ConvexClientProvider.tsx`
   - Access via Convex hooks in client components (e.g., `useQuery`, `useMutation`) and ensure types align with server functions
 - Authentication & billing
   - Clerk is the source of truth for sessions; protect pages via `middleware.ts`
   - Subscription gating implemented under `app/dashboard/payment-gated/`
   - Pricing UI at `components/custom-clerk-pricing.tsx`
 - Example: adding a new Convex query
 
 ```ts
 // convex/items.ts
 import { query } from 'convex/server'
 export const list = query(async (ctx) => {
   return await ctx.db.query('items').collect()
 })
 
 // app/dashboard/items/page.tsx (client component)
 import { useQuery } from 'convex/react'
 import { api } from '@/convex/_generated/api'
 
 export default function ItemsPage() {
   const items = useQuery(api.items.list) || []
   return <div>{items.map(i => <div key={i._id}>{i.name}</div>)}</div>
 }
 ```
 
 Security considerations
 - Validate and narrow types with Zod where user input crosses boundaries
 - Never expose secrets in client code, logs, or diffs
 - Verify webhook signatures (Clerk) via `convex/http.ts`; keep secrets in environment variables
 
 ## 7) Git & Safety
 
 - Before committing
   - Run `git status` and `git diff` to inspect all changes
   - Review diffs for secrets, credentials, or sensitive data; do not commit `.env*` or build outputs
   - Ensure all dependent systems for your change are updated (see checklist above)
 - Branching
   - Base branch is `main`; current working branch may vary (e.g., `Template`)
 - Do not push unless explicitly requested; follow repository conventions for commit messages
 
 ## 8) Quick References
 
 - File paths
   - Protected app: `app/dashboard/*` (see `app/dashboard/page.tsx`, nav, charts, tables)
   - Landing pages: `app/(landing)/*`
   - UI primitives: `components/ui/*`
   - Theming/toggle: `components/theme-provider.tsx`, `components/mode-toggle.tsx`
   - Clerk pricing: `components/custom-clerk-pricing.tsx`
   - Convex server: `convex/*`
 - Tokens & styling
   - Use design system tokens only; avoid inline hard-coded values
   - Prefer existing component APIs; extend via composition
 - Commands
   - Dev: `npm run dev` + `npx convex dev`
   - Lint/build/start: `npm run lint` / `npm run build` / `npm start`
 - Common pitfalls to avoid
   - Duplicated functionality, overwriting tests, modifying core frameworks, or adding deps without checking
   - Partially-updated features (routes/types/UI not aligned)
 
 ---
 
 If any instruction conflicts, defer to the rules in `.cursor/rules/` and the actual code in this repository. Always confirm file paths and existing patterns before implementation.
