 # App Flow — Local Business Directory (Belize)
 
 Date: 2025-10-23
 
 Assumptions: Infinite scroll on results; homepage map preview below the fold; owner photos limit 5; mock-data-first for all states.
 
 ## Public Flows
 
 ### 1) Homepage (List-first)
 - Sections (top→bottom):
   1. Hero search (keyword + category + location)
   2. Featured categories
   3. Featured businesses
   4. Latest listings
   5. Map preview (optional) with link to full map view
 - States (mock): loading, empty (no featured), populated, error
 
 ### 2) Search Results (List View)
 - Inputs: keyword, category, location
 - Filters: category, location (city/area), tags
 - Results: infinite scroll; sort by relevance (nearest if location set)
 - Actions: open listing detail; switch to Map View (sync query)
 - States (mock): loading, empty, populated, error
 
 ### 3) Listing Detail
 - Content: photos (up to 5), name, category, short description, hours, phone, website, address, directions link, map pin (static/preview)
 - States (mock): loading, not-found, populated, error
 
 ### 4) Map View (Dedicated)
 - Mapbox with clustering; synchronized result list/pane sharing the same query as list view
 - Interactions: click pin → highlight list item; list hover → focus pin; filters persist
 - States (mock): loading, empty, populated, error
 
 ## Business Owner Flows
 
 ### 5) Owner Dashboard
 - Sections: My Listings (table/cards), Create Listing CTA, Status badges (draft/submitted/approved/rejected)
 - States (mock): empty (no listings), populated, error
 
 ### 6) Create/Edit Listing
 - Fields: name, category, address, map pin placement, phone, website, hours, images (≤5), short description, tags
 - Actions: Save Draft, Submit for Approval
 - Validation: required fields (name, category, address, location)
 - States (mock): initial, validation error, saved, error
 
 ### 7) Submission & Status
 - Flow: draft → submitted → approved/rejected
 - User sees status timeline and rejection reason (if any); can edit and resubmit
 - States (mock): pending approval, approved, rejected
 
 ## Admin Flows
 
 ### 8) Review Queue
 - Filters: category, submission date, owner
 - Actions: open listing detail, approve/reject, edit fields
 - States (mock): empty queue, populated, error
 
 ### 9) Listing Review
 - View submitted data, map pin, images; edit if needed
 - Actions: Approve → status=approved; Reject → status=rejected with reason
 - States (mock): loading, populated, error
 
 ### 10) Manage Categories/Tags
 - Add/edit/remove categories and tags (admin-managed taxonomy)
 - States (mock): empty, populated, error
 
 ## Data Strategy
 - Phase 1: All pages/components powered by mock JSON fixtures and deterministic UI states.
 - Phase 2: Integrate Convex collections & serverless fns (listings, categories, users); wire Mapbox on Map View and owner pin placement.
 - Feature flag to toggle between mock data and live data.
 
