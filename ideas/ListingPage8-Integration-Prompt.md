# UI Integration Prompt — Listing Page 8 (Bella Vista Bistro)

```
I want to integrate a custom UI design into our Project Components Library project. Please extract and adapt this interface to work with our React 19 + Vite + TypeScript 5 + Tailwind CSS 3 stack.

**CURRENT PROJECT CONTEXT:**
- Framework: React 19 + Vite
- Styling: Tailwind CSS 3 via project design tokens (see "design -system" directory); no hard-coded hex values
- Backend: N/A (component library; use local fixtures for demos)
- Language: TypeScript
- Current file: src/components/listing/BellaVistaBistro.tsx (compose from subcomponents under src/components/listing/)
- Existing functionality: Demos in src/*; reusable components in ui/components/*; strong typing and token usage enforced

**UI TO INTEGRATE:**
Adapt HTML/CSS from ideas/listingpage8.html. Key sections:
- Sticky header with logo and nav
- Two-column layout (content + sidebar)
- Hero image gallery: masonry-style main image + thumbnails with "+N photos" overlay
- Business header: name, verification badge, category, rating with stars, distance/price
- Description, social proof stats, action buttons (Get Directions, Call Now)
- Review preview: average rating, rating bars
- Sidebar: Contact Information (address/phone/website/email), Hours (open-now indicator), Certifications & Features badges, Last updated

**INTEGRATION REQUIREMENTS:**
1. Preserve All Existing Functionality
   - Follow library demo conventions (props-driven; no network)
   - Keep sticky header and responsive grid
   - Preserve accessibility and keyboard navigation

2. Adapt Design Elements
   - Convert HTML to React function components
   - Replace inline CSS with Tailwind utilities mapped to tokens (colors, spacing, radius, shadows)
   - Replace font-awesome with Lucide or project icon strategy
   - Ensure responsive behavior for mobile/tablet/desktop

3. Technical Adaptations
   - Define TS interfaces in ui/components/types/listing.types.ts: RestaurantBusiness, SocialProofMetric, ReviewStats, RatingBreakdownBar, ContactInfo, HourRow, CertificationBadge, GalleryImage
   - Implement state for gallery selection and optional lightbox stub
   - Provide callbacks: onGetDirections, onCall
   - Keep files <500 lines; split by responsibility

4. Feature Integration
   - Gallery with accessible thumbnails and overlay for more photos
   - Rating stars and review bars rendered from numeric data
   - Social proof numbers animated count optional (progressive enhancement)
   - Hours list with open-now highlighting
   - Certifications badges with tokens and icons

5. Specific Adaptations Needed
   - Map all colors to Tailwind token classes; remove hexes
   - Use semantic landmarks (header, main, aside) and headings
   - Focus-visible states for interactive elements; proper aria-labels
   - Avoid external image styles; use object-cover and aspect utilities

**MULTIAGENT COORDINATION:**
- @agents-agument/core/ui-configurator-agent for token mapping
- @agents-agument/universal/react-developer for implementation
- Maintain context across handoffs

**DELIVERABLES:**
1. Components under src/components/listing/:
   - ListingHeader, Breadcrumbs (if needed)
   - RestaurantGallery (main + thumbnails, overlay)
   - BusinessHeaderMeta (name, badge, category, rating)
   - SocialProofStats, ActionButtons
   - ReviewPreview, RatingBars
   - Sidebar: ContactInfoCard, HoursCard, CertificationsCard, LastUpdated
   - BellaVistaBistro (composition demo)
2. Types in ui/components/types/listing.types.ts
3. Tailwind tokenized styling only; no inline styles
4. Demo in src/BellaVistaBistroDemo.tsx with fixtures
5. Working interactions (gallery, buttons) with keyboard support
6. Responsive layout across breakpoints

**TESTING REQUIREMENTS:**
- Build passes (npm run build)
- Components render without runtime errors
- Verify gallery keyboard/mouse navigation
- Validate responsive layout at sm/md/lg
- Confirm ARIA roles/labels and focus outlines
- Ensure no hard-coded colors/sizes; only tokens

Please analyze the provided UI design and implement it step-by-step, maintaining our component-library patterns while delivering the exact visual design requested.
```
