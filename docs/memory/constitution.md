# Starter.diy Constitution

## Core Principles

### I. SaaS-First Architecture
Every feature is built with SaaS scalability in mind; Components must be modular, reusable, and independently maintainable; Clear separation between public marketing pages and protected application areas; Authentication and subscription gating are first-class concerns.

### II. Real-Time by Default
All data operations leverage Convex's real-time capabilities; UI components automatically reflect data changes without manual refresh; Server functions maintain consistency between client and server; Real-time updates are considered a core feature, not an add-on.

### III. Security-First Development (NON-NEGOTIABLE)
Authentication protection via middleware is mandatory; All protected routes must be properly guarded; Clerk JWT configuration for Convex is required; Webhook signatures must be verified; No secrets in client code, ever.

### IV. Design System Consistency
All UI components must use design system tokens (colors, typography, spacing, radius, shadows); No hard-coded styles allowed; Prefer existing component APIs; Extend through composition; Maintain visual consistency across the entire application.

### V. Vertical Slice Architecture
Features are implemented as complete vertical slices; Frontend components, backend functions, and data schemas are developed together; Integration testing focuses on complete user flows; No partial implementations - all related systems must be updated together.

## Technology Stack Requirements

### Core Technologies
- Next.js 15 (App Router, React 19, Turbopack) - mandatory for all web development
- Convex - required for all data storage and serverless functions
- Clerk - mandatory for authentication and user management
- Clerk Billing - required for subscription management
- Tailwind CSS v4 - mandatory for all styling
- TypeScript - required for all code

### Development Environment
- Node.js with npm scripts as defined in package.json
- Convex dev server (npx convex dev) running in parallel with Next.js dev server
- Environment variables properly configured in .env.local
- Linting and build processes must pass before deployment

## Development Workflow

### Code Structure Rules
- One responsibility per file; keep files ≤ ~500 LOC
- Modular by vertical slice; prefer composition over inheritance
- Use relative imports and maintain consistent folder patterns
- Follow KISS, YAGNI, Component-first, Performance-by-default principles

### Integration Checklist
Before submitting changes:
- Are all dependent systems updated (routing, state, types, styles, imports)?
- Would this break in production due to isolation/misalignment?
- Is end-to-end flow verified (happy path and error states)?
- Have all readers/writers/dependents of changed data or APIs been updated?

### Quality Gates
- All code must pass linting (npm run lint)
- All code must build successfully (npm run build)
- Authentication protection must be verified
- Real-time functionality must be tested
- Design system compliance must be verified

## Governance

### Constitution Supremacy
This constitution supersedes all other practices and guidelines; All development decisions must align with these principles; Amendments require documentation, team approval, and migration plan.

### Compliance Verification
- All PRs/reviews must verify constitution compliance
- Complexity must be justified with clear business value
- Use AGENTS.md for runtime development guidance
- Universal Document Rules v2.0 must be followed for all documentation

### Agent Mode System
When @agent-file is referenced, switch to that agent and follow its workflow exclusively; Auto-selection keywords guide agent choice; Multi-agent patterns must be followed for complex tasks; Protocol requires full agent identity adoption and context maintenance.

**Version**: 1.0.0 | **Ratified**: 2025-10-09 | **Last Amended**: 2025-10-09