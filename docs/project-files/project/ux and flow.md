UX & Flow
✅ User Stories
For Sam the Shopper (Unauthenticated):

As a shopper, I want to immediately search and browse all verified businesses without creating an account

As a shopper, I want to filter businesses by category and location on a map

As a shopper, I want to view detailed business pages with category-specific information

As a shopper, I want to see which businesses are verified by the platform

For Bailey the Business Owner:
5. As a business owner, I want to sign up and create a business profile
6. As a business owner, I want to edit my business information and photos
7. As a business owner, I want to preview my public listing
8. As a business owner, I want to see basic profile view analytics

For Alex the Admin:
9. As an admin, I want to see a queue of all submitted businesses
10. As an admin, I want to approve or decline submissions efficiently

✅ User Scenarios
Scenario A: Sam Finds Brunch Spot
Sam opens Local Nexus, taps "Restaurants," uses map view to find "The Sunny Cafe" with high rating, views menu, and gets directions - all without logging in.

Scenario B: Bailey Lists Landscaping Service
Bailey signs up via Google OAuth, fills out service business form with service area details, submits for verification, and gets approved notification.

Scenario C: Alex Verifies Business
Alex logs into admin dashboard, reviews pending submissions, approves "Bailey's Landscaping" with one click, making it live instantly.

✅ App Flow Document
App Flow Document
1. Public Site Access
User: Sam (Unauthenticated)

Entry: Landing page (/) with immediate access to search and browse

UI: Hero section with search, featured businesses, category navigation

Transitions: Direct access to all public content without authentication

2. Authentication & Role Routing
Clerk Integration: Handles auth UI and JWT creation

Webhook: Svix sends user data to Convex on sign-up

Role Routing: Business owners → dashboard, Admins → admin panel

3. Business Dashboard
Path: /dashboard

UI: Welcome, "Add Business" button, business list with edit/preview

States: Empty state for new users, list view for existing businesses

4. Business Submission Flow
Path: /dashboard/business/new

UI: Dynamic form with category selection

Logic: Form fields change based on category (Restaurant/Service/Retail)

Backend: Convex mutation creates business with status: "pending"

5. Admin Verification
Path: /admin (Role-protected)

UI: Table of pending businesses with approve/decline actions

Backend: Mutations update business status to "verified" or "declined"

6. Search & Browse
Path: /search & /categories/[category]

UI: Sidebar filters, result list, synchronized Mapbox map

Backend: Convex queries for verified businesses with reactive filtering

7. Business Listing Page
Path: /business/[slug]

UI: Dynamic template based on business category

Features: Category-specific sections, embedded map, view counting