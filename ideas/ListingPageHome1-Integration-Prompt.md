# UI Integration Prompt — Listing Page Home 1 (Neighborhood Landing)

```
I want to integrate a custom UI design into our Project Components Library project. Please extract and adapt this interface to work with our React 19 + Vite + TypeScript 5 + Tailwind CSS 3 stack.

**CURRENT PROJECT CONTEXT:**
- Framework: React 19 + Vite
- Styling: Tailwind CSS 3 via project design tokens (see "design -system" directory); avoid hard-coded hex values
- Backend: N/A (component library; demos powered by local fixtures only)
- Language: TypeScript
- Current file: src/components/listing/NeighborhoodHome.tsx (compose from subcomponents under src/components/listing/)
- Existing functionality: Demos in src/*; reusable UI in ui/components/*; strict typing and token usage

**UI TO INTEGRATE:**
Adapt HTML/CSS from ideas/listingpagehome1.html. Key sections:
- Sticky, blurred header with logo, nav menu, and auth actions (Login, Join Now)
- Hero with badge, headline with gradient text, description, dual-input search (query + location) and CTA buttons
- Community stats strip with metrics and "Trusted Community" badge
- Categories grid including a featured split tile (Food & Dining) plus additional category tiles
- Discovery section: two-column layout with features list and map visual with indicator
- Full footer with brand block, social links, three link columns, and legal footer

**INTEGRATION REQUIREMENTS:**
1. Preserve All Existing Functionality
   - Follow library demo approach (props-driven; no network)
   - Keep sticky header behavior and responsive layouts
   - Maintain accessibility (semantic landmarks, ARIA, focus-visible)

2. Adapt Design Elements
   - Convert HTML to React function components
   - Replace inline CSS with Tailwind utilities mapped to tokens (colors, spacing, radius, shadows)
   - Replace font-awesome with Lucide or existing icon abstraction
   - Implement responsive breakpoints for mobile/tablet/desktop

3. Technical Adaptations
   - Define TS interfaces in ui/components/types/listing.types.ts: NavLink, HeaderActions, SearchFormValues, StatMetric, CategoryTile, CategoryFeatured, DiscoveryFeature, MapIndicator, FooterLinkGroup
   - Search form emits onSearch({ query, location })
   - Buttons emit callbacks: onBrowseBusinesses, onAddBusiness, onLaunchExplorer
   - Keep files <500 lines, split responsibilities per component

4. Feature Integration
   - Accessible search inputs with labels/aria and keyboard submission
   - Gradient text and badges using tokenized Tailwind classes
   - Categories grid with hover elevation and featured split layout
   - Discovery features list with icon bullets; map card with indicator pill
   - Footer with keyboard-navigable links and visible focus states

5. Specific Adaptations Needed
   - Tokenize all color usage; no hex literals
   - Semantic structure: header/nav/main/section/footer with headings hierarchy
   - Focus-visible rings and adequate contrast per WCAG AA
   - Avoid external font-awesome dependency; align with project icon system

**MULTIAGENT COORDINATION:**
- @agents-agument/core/ui-configurator-agent for design-token mapping
- @agents-agument/universal/react-developer for implementation
- Maintain context across handoffs

**DELIVERABLES:**
1. Components under src/components/listing/:
   - SiteHeader (logo, nav, actions)
   - HeroSection (Badge, Headline, SearchBar, HeroCTAs)
   - CommunityStats (StatsRow, CommunityBadge)
   - CategoriesSection (FeaturedCategoryTile, CategoryTile)
   - DiscoverySection (DiscoveryContent, DiscoveryMapCard)
   - SiteFooter (Brand, SocialLinks, LinkColumns, Legal)
   - NeighborhoodHome (composition demo)
2. Types in ui/components/types/listing.types.ts
3. Tailwind tokenized styling only; no inline styles
4. Demo in src/NeighborhoodHomeDemo.tsx with fixture content
5. Working interactions (search submit, CTAs) with keyboard support
6. Responsive design across breakpoints

**TESTING REQUIREMENTS:**
- Build passes (npm run build)
- Components render without runtime errors
- Verify search form a11y and keyboard submission
- Validate responsive behavior at sm/md/lg
- Confirm ARIA roles/labels and focus outlines
- Ensure no hard-coded colors/sizes; only token-based utilities

Please analyze the provided UI design and implement it step-by-step, maintaining our component-library patterns while delivering the exact visual design requested.
```
