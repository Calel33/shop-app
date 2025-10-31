 # Security & Compliance Guidelines — Local Business Directory (Belize)
 
 Date: 2025-10-23
 
 ## Scope & Principles
 - Minimal data (no sensitive PII); role-based access (Public, Owner, Admin).
 - Mock-data-first: avoid real data during initial UI development.
 - Defense-in-depth: authn, authz, validation, transport, storage, logging.
 
 ## Authentication & Authorization (Clerk)
 - Enforce session validation server-side for protected routes (Owner/Admin).
 - Role checks on actions: Owners can CRUD only their listings; Admin has elevated rights.
 - Email verification required for Owners before submission; session timeout reasonable.
 - CSRF: rely on Clerk-provided protections for forms/actions; avoid exposing session tokens client-side.
 
 ## Data Validation & Integrity (Convex)
 - Validate all mutations (required fields, types, bounds: lat/lng range, image count ≤5).
 - Normalize inputs (trim, canonicalize URLs, phone formats); reject malicious payloads.
 - Status workflow enforced in backend: draft → submitted → approved/rejected; store rejection reason.
 - Rate-limit owner submissions and edits (per user/IP) to reduce abuse.
 
 ## Frontend Security
 - Output encoding for user content; avoid dangerouslySetInnerHTML.
 - CSP (baseline): default-src 'self'; img-src 'self' data: https:; script-src 'self' 'unsafe-inline' 'unsafe-eval' vercel-insights domains as needed; connect-src Mapbox/Convex/Clerk; style-src 'self' 'unsafe-inline'. Tighten in production.
 - XSS/Clickjacking: X-Frame-Options DENY; set Referrer-Policy strict-origin-when-cross-origin.
 - Forms: client-side validation mirrors server; do not leak validation details.
 
 ## Secrets & Configuration
 - Store secrets only in environment variables on Vercel; never commit.
 - Mapbox token: use NEXT_PUBLIC_MAPBOX_TOKEN with least privilege (restrict URL origins if possible).
 - Webhooks (later): verify Svix signatures server-side; rotate secrets periodically.
 
 ## Transport & Storage
 - Enforce HTTPS everywhere; HSTS in production.
 - Images: on integration, accept only allowed MIME types; size limits; strip EXIF; store via signed URLs.
 - Backups/retention (later): define retention for listings and audit logs; enable soft-delete if needed.
 
 ## Logging & Monitoring
 - Log auth events (login, role changes), approvals/rejections (with actor/user IDs), and errors (without sensitive payloads).
 - Centralize logs (Vercel/Convex); set alerts for abnormal approval spikes or submission floods.
 
 ## Privacy & Compliance
 - Provide Terms/Privacy links; describe data use and retention; allow owner account deletion requests.
 - Cookie banner not required if only essential cookies are used by Clerk; reassess when adding analytics/ads.
 
 ## Third-Party Services
 - Clerk: follow best practices for JWT/session handling; least-privileged API keys.
 - Mapbox: restrict token scope; monitor usage quotas.
 - Convex: secure functions; validate inputs; restrict indexes to needed fields.
 
 ## Deployment Checklist (Prod)
 - [ ] All env vars set in Vercel; no secrets in repo or logs
 - [ ] CSP and security headers configured
 - [ ] Clerk roles and email verification enabled
 - [ ] Rate limits active on sensitive endpoints
 - [ ] Error boundaries and fallbacks present
 - [ ] Backups/retention plan documented (if enabled)
 
