# UI Integration Prompt — Listing Page 3 (Iron Will CrossFit)

```
I want to integrate a custom UI design into our Project Components Library project. Please extract and adapt this interface to work with our React 19 + Vite + TypeScript 5 + Tailwind CSS 3 stack.

**CURRENT PROJECT CONTEXT:**
- Framework: React 19 + Vite
- Styling: Tailwind CSS 3 using project design tokens (see "design -system" directory); no hard-coded colors/sizes
- Backend: N/A (frontend component library; demo data via local fixtures)
- Language: TypeScript
- Current file: src/components/listing/IronWillCrossFit.tsx (compose from subcomponents under src/components/listing/)
- Existing functionality: Component demos under src/* and reusable UI under ui/components/* with strict types and tokens

**UI TO INTEGRATE:**
Paste/adapt the HTML/CSS from ideas/listingpage3.html. Key sections:
- Sticky header with logo and nav
- Breadcrumb trail
- Main two-column layout (content + sidebar)
- Hero with image gallery (dots navigation)
- Business header: title, category, verification badge, meta (rating, distance, hours, spots)
- Highlights grid (3 cards)
- Action buttons (Book Free Trial, Call Now, Get Directions)
- Trainers section (grid of cards)
- Membership section with pricing cards (one featured)
- Sidebar: today’s classes, gym information, hours, equipment, last updated

**INTEGRATION REQUIREMENTS:**
1. Preserve All Existing Functionality
   - Maintain component-library demo pattern (no network calls; mock data props)
   - Keep responsive behavior and sticky header
   - Preserve routing-friendly anchors (replace raw <a href="#"> with button/Link stubs)
   - Maintain accessibility (semantic roles, aria, focus-visible)

2. Adapt Design Elements
   - Convert HTML/CSS to React function components
   - Replace inline CSS with Tailwind utilities mapped to our design tokens (colors, spacing, radius, shadows)
   - Ensure responsive behavior for mobile, tablet, desktop breakpoints as in source
   - Replace font-awesome icons with Lucide (already used in project) or fallback to existing icon strategy

3. Technical Adaptations
   - Define TypeScript props/interfaces in ui/components/types (e.g., ListingBusiness, Trainer, PricingPlan, ClassSchedule)
   - Use React patterns (state hooks for gallery index, keyboard handlers)
   - Add minimal error boundaries for gallery image loading
   - Optimize images via loading attributes; keep components <500 lines and split by responsibility

4. Feature Integration
   - Image gallery with dots navigation (click/keyboard to change active index)
   - Action buttons emit callbacks: onBookTrial, onCall, onGetDirections
   - Trainers grid renders from props; maintain tab/focus order
   - Pricing cards support featured variant
   - Sidebar schedule with capacity labels; hours grid highlighting "open" state

5. Specific Adaptations Needed
   - Replace hard-coded color hexes with tokenized Tailwind classes (from design -system)
   - Use CSS transitions or Framer Motion (optional) for subtle hover/active states
   - Ensure compatibility with existing ui/components/product primitives where relevant
   - Keep state localized; accept all content via props with sensible defaults

**MULTIAGENT COORDINATION:**
- @agents-agument/core/ui-configurator-agent for design analysis and token mapping
- @agents-agument/universal/react-developer for implementation
- Maintain context across handoffs

**DELIVERABLES:**
1. React components under src/components/listing/:
   - ListingHeader, Breadcrumbs
   - ImageGallery (with dots), BusinessHeaderMeta
   - HighlightCard, HighlightsGrid, ActionButtons
   - TrainersSection, TrainerCard
   - MembershipSection, PricingCard
   - Sidebar: TodayClasses, GymInfo, HoursList, EquipmentGrid, LastUpdated
   - IronWillCrossFit (composition demo)
2. Updated TypeScript types in ui/components/types/listing.types.ts
3. Tailwind-based styling mapped to tokens; no inline styles
4. Demo usage in src/IronWillCrossFitDemo.tsx with fixture data
5. Working interactions (gallery, buttons) with accessible keyboard support
6. Responsive behavior across breakpoints

**TESTING REQUIREMENTS:**
- Build succeeds (npm run build)
- Components render without errors in a demo page
- Verify gallery navigation via mouse and keyboard
- Validate responsive layout at sm/md/lg breakpoints
- Check ARIA roles/labels and focus-visible states
- Ensure no hard-coded colors/sizes; only tokenized utilities

Please analyze the provided UI design and implement it step-by-step, maintaining our component-library patterns while delivering the exact visual design requested.
```
