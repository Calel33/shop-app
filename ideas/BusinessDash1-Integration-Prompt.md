# UI Integration Prompt — Business Dashboard (businessdash1.html)

```
I want to integrate a custom UI design into our "Component & Landing Library" project. Please extract and adapt this interface to work with our React + TypeScript + Tailwind stack.

**CURRENT PROJECT CONTEXT:**
- Framework: React 19 + Vite
- Styling: Tailwind CSS 3 (design tokens under `design -system/`; no hard-coded styles), minimal CSS modules where necessary
- Backend: N/A (frontend component library; demo-only data)
- Language: TypeScript
- Current file: src/components/admin/BusinessDashboard.tsx (new), with demo wiring in src/AdminBusinessDashboardDemo.tsx (new)
- Existing functionality: Library of reusable UI slices and demos; strict type safety; design tokens; accessibility-first components

**UI TO INTEGRATE:**
Source file: C:\\Users\\user1\\Desktop\\project-componets\\ideas\\businessdash1.html
Design summary:
- Admin dashboard view focused on directory management
- Sidebar with grouped navigation and user profile capsule
- Top bar with breadcrumb, global search, notifications
- Quick stats tiles (KPIs with trend indicators)
- Control panel with view switcher (List | Card | Map), filters (search, category, status, zone, verification), and actions (Export, Add Business)
- Business list with rich metadata, tags (category/verified/premium), and row actions
- Bulk actions toolbar (Approve, Suspend, Delete)
- Responsive layout optimizations for large desktops

(Use the HTML file as the source of truth for structure and content; convert to TSX + Tailwind.)

**INTEGRATION REQUIREMENTS:**
1. 🔄 Preserve All Existing Functionality
   - Maintain component-library patterns; no backend dependency
   - Keep view switcher and filters functional
   - Preserve bulk selection state and toolbar logic
   - Maintain navigation structure (breadcrumb/top bar)

2. 🎨 Adapt Design Elements
   - Convert HTML/CSS to React TSX components with Tailwind using project tokens
   - Replace inline styles/hard-coded colors with tokens from `design -system/`
   - Ensure responsive behavior per original media queries; add focus-visible states
   - Use semantic landmarks and ARIA attributes where appropriate

3. 🔧 Technical Adaptations
   - Define TypeScript types (Business, Filters, ViewMode) in `ui/components/types/`
   - Use React hooks for filters, selection, and view mode state
   - Implement accessible event handlers (Enter/Space activation, ESC clear)
   - Split into subcomponents; avoid premature memoization

4. 📱 Feature Integration
   - View switching (List/Card/Map)
   - Keyboard shortcuts: `/` focus search, `a` toggle select all, `Esc` clear selection
   - Loading and empty states
   - Basic validation for filter inputs
   - CSS transition animations for hover/selection and view transitions

5. 🎯 Specific Adaptations Needed
   - Replace Font Awesome CDN with Lucide (or existing icon strategy)
   - Map gradients, colors, shadows, radii to Tailwind config/tokens
   - Dark-mode readiness with current Tailwind theme
   - Ensure compatibility with existing `ui/components/*` patterns and barrel exports
   - Use local mock data for demo; no network calls

**MULTIAGENT COORDINATION:**
Please use appropriate agent coordination:
- @agents-agument/core/ui-configurator-agent for design analysis
- @agents-agument/universal/react-developer for implementation
- Maintain context across agent handoffs
- Keep comments minimal; note token mappings where non-obvious

**DELIVERABLES:**
1. ✅ New TSX components:
   - ui/components/admin/Sidebar.tsx
   - ui/components/admin/TopBar.tsx
   - ui/components/admin/QuickStats.tsx
   - ui/components/admin/BusinessFilters.tsx
   - ui/components/admin/BusinessListItem.tsx
   - ui/components/admin/BulkToolbar.tsx
   - ui/components/admin/BusinessDashboard.tsx (composition)
2. ✅ Updated TypeScript interfaces in ui/components/types/admin.types.ts
3. ✅ Tailwind styling via tokens; no hard-coded colors
4. ✅ Demo page wiring in src/AdminBusinessDashboardDemo.tsx
5. ✅ Interactions: filtering, selection, bulk actions, view switching
6. ✅ Responsive design across breakpoints
7. ✅ Brief PR change notes (no README edits unless requested)

**TESTING REQUIREMENTS:**
- Loads without console errors in `npm run dev`
- Filters update list; shortcuts operate as specified
- Bulk selection updates toolbar count and actions
- Validate empty/loading states and responsive layout
- Accessibility: semantic regions, ARIA, focus-visible, keyboard operability
- Verify all colors/spacing/radius come from tokens; no inline hex values
- Optional visual smoke test via test/ prototype

Please analyze the provided UI design (businessdash1.html) and implement it step-by-step, maintaining our component-library standards and design tokens while delivering the same visual/interaction design in React + TypeScript + Tailwind.
```
