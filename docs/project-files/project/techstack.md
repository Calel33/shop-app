Technical Foundation
✅ Tech Stack Document
Frontend:

Next.js 15 (App Router), React 19, TypeScript

Tailwind CSS v4 + Custom Design System

shadcn/ui + Radix UI primitives

Framer Motion, React Bits, Magic UI for animations

Backend & Services:

Convex (Database, Serverless Functions, Real-time)

Clerk (Authentication & User Management)

Clerk Billing (Future subscriptions)

Svix (Webhook handling)

Mapbox GL JS (Mapping)

Development & Deployment:

Turbopack (Build tool)

Vercel (Hosting)

Node.js 18+ runtime

✅ Backend Structure Document (Convex)
Data Schema:

typescript
users: {
  clerkId: string,
  email: string,
  role: 'user' | 'admin'
}

businesses: {
  name: string,
  slug: string,
  category: 'restaurant' | 'service' | 'retail',
  // Contact & Location
  address: string,
  coordinates: { lat: number, lng: number },
  // Category-specific fields
  cuisineType: string[], // Restaurant
  priceRange: '$' | '$$' | '$$$', // Restaurant
  serviceArea: string, // Service
  productCategories: string[], // Retail
  // Status & Analytics
  status: 'pending' | 'verified' | 'declined',
  ownerId: Id<'users'>,
  viewCount: number
}
Key Indexes:

by_slug - For business pages

by_ownerId - For user dashboards

by_status - For admin queue

by_category_status - For category pages

✅ Frontend Guidelines Document
Project Structure:

text
app/
├── (public)/           // Public routes (no auth)
├── (dashboard)/        // Business owner routes
├── (admin)/            // Admin-only routes
├── api/               // Webhook endpoints
└── globals.css
Data Fetching:

Public content: Convex query (no auth)

Protected content: Convex queryWithAuth

Real-time updates via Convex reactive queries

Key Components:

Dynamic business form with category-specific fields

Synchronized list/map views

Role-based routing with Clerk middleware