# UI Integration Prompt — Business Listing Page (listing7.html)

```
I want to integrate a custom UI design into our "Component & Landing Library" project. Please extract and adapt this interface to work with our React + TypeScript + Tailwind stack.

**CURRENT PROJECT CONTEXT:**
- Framework: React 19 + Vite
- Styling: Tailwind CSS 3 (design tokens under `design -system/`; no hard-coded styles), minimal CSS modules where necessary
- Backend: N/A (frontend component library; demo-only data)
- Language: TypeScript
- Current file: src/components/business/BusinessListing.tsx (new), demo wiring in src/BusinessListingDemo.tsx (new)
- Existing functionality: Reusable UI slices and demos; strict type safety; design tokens; accessibility-first components

**UI TO INTEGRATE:**
Source file: C:\\Users\\user1\\Desktop\\project-componets\\ideas\\listing7.html
Design summary:
- Public business listing page for "Green Bowl Co." (consumer-facing)
- Sticky header with logo and navigation + primary CTA (Order Online)
- Main layout: content area + right sidebar
- Hero with image banner, title, tagline, verification badge, description, key feature cards
- Loyalty promo section (benefits grid)
- Menu section with tabs (Build Your Bowl, Signature Bowls, Smoothies, Sides), categories, items, calories, allergen tags, and action buttons
- Nutrition legend with badges
- Sidebar cards: quick actions, contact information, hours, features, health & safety
- Responsive layout across breakpoints

(Use the HTML as source of truth for structure/content; convert to TSX + Tailwind.)

**INTEGRATION REQUIREMENTS:**
1. 🔄 Preserve All Existing Functionality
   - Maintain tab switching state for menu sections
   - Keep CTA actions wired as handlers (no real network)
   - Preserve layout structure: header, main, sidebar

2. 🎨 Adapt Design Elements
   - Convert HTML/CSS to React TSX with Tailwind utilities using project tokens
   - Replace inline colors/gradients/shadows with tokens or Tailwind theme
   - Implement sticky header and responsive grid using Tailwind
   - Accessibility: semantic landmarks, ARIA for tabs, focus-visible, keyboard nav

3. 🔧 Technical Adaptations
   - Define TypeScript types for MenuItem, MenuCategory, MenuTab, Feature, Hours, Contact in `ui/components/types/`
   - Componentize: HeaderNav, BusinessHero, LoyaltyBanner, MenuTabs, MenuCategoryList, NutritionLegend, SidebarCard(s), BusinessListing (composition)
   - Use React hooks for tab state and simple interactions
   - Replace Font Awesome with Lucide (or existing icon abstraction)

4. 📱 Feature Integration
   - Tabs: keyboard accessible (ArrowLeft/Right, Home/End), ARIA roles
   - Buttons: hover/active states per tokens; disabled/loading variants for demo
   - Optional: Smooth scroll to sections; minor CSS transitions on hover
   - Empty/loading states for menu categories (mocked)

5. 🎯 Specific Adaptations Needed
   - Tokenize brand greens/yellows and gradients into Tailwind theme or use existing tokens
   - Convert hero image to prop; provide alt text and object-cover styling
   - Support dark mode styles if theme enabled
   - Ensure compatibility with `ui/components/*` export patterns

**MULTIAGENT COORDINATION:**
Please use appropriate agent coordination:
- @agents-agument/core/ui-configurator-agent for design analysis
- @agents-agument/universal/react-developer for implementation
- Maintain context across handoffs; keep comments minimal

**DELIVERABLES:**
1. ✅ New TSX components:
   - ui/components/business/HeaderNav.tsx
   - ui/components/business/BusinessHero.tsx
   - ui/components/business/LoyaltyBanner.tsx
   - ui/components/business/MenuTabs.tsx
   - ui/components/business/MenuCategoryList.tsx
   - ui/components/business/NutritionLegend.tsx
   - ui/components/business/Sidebar/QuickActions.tsx
   - ui/components/business/Sidebar/ContactInfo.tsx
   - ui/components/business/Sidebar/Hours.tsx
   - ui/components/business/Sidebar/Features.tsx
   - ui/components/business/Sidebar/HealthSafety.tsx
   - ui/components/business/BusinessListing.tsx (composition)
2. ✅ Types in ui/components/types/business.types.ts
3. ✅ Tailwind styling via tokens; no hard-coded hex values
4. ✅ Demo page wiring in src/BusinessListingDemo.tsx
5. ✅ Functioning tabs and CTA handlers; accessible nav and controls
6. ✅ Responsive design from mobile to wide desktop
7. ✅ Brief PR change notes (no README edits unless requested)

**TESTING REQUIREMENTS:**
- Runs cleanly in `npm run dev` with no console errors
- Tabs are keyboard-accessible with correct ARIA and roving tabindex
- Hero image alt text present; focus-visible styles apparent
- Sidebar info cards render and collapse acceptably on small screens
- Validate all colors/spacing/radius are from tokens/theme
- Visual smoke test in test/ prototype if applicable

Please analyze the provided UI design (listing7.html) and implement it step-by-step, maintaining our component-library standards and design tokens while delivering the same visual/interaction design in React + TypeScript + Tailwind.
```
