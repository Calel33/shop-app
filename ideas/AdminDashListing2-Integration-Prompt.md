# UI Integration Prompt — Business Directory (admindashlisting2.html)

```
I want to integrate a custom UI design into our "Component & Landing Library" project. Please extract and adapt this interface to work with our React + TypeScript + Tailwind stack.

**CURRENT PROJECT CONTEXT:**
- Framework: React 19 + Vite
- Styling: Tailwind CSS 3 (design tokens under `design -system/`; no hard-coded styles), minimal CSS modules where necessary
- Backend: N/A (frontend component library; demo-only data)
- Language: TypeScript
- Current file: src/components/admin/BusinessDirectory.tsx (new), with demo wiring in src/AdminDirectoryDemo.tsx (new)
- Existing functionality: Library of reusable UI slices and demos; strict type safety; design tokens; accessibility-first components

**UI TO INTEGRATE:**
Source file: C:\\Users\\user1\\Desktop\\project-componets\\ideas\\admindashlisting2.html
Design summary:
- Admin dashboard “Business Directory” management screen
- Sidebar with grouped navigation
- Top bar with breadcrumb, global search, notifications
- Quick stats strip (5 tiles with trend indicators)
- Control panel with view switcher (List | Card | Map), filters (search, category, status, zone, verification), and actions (Export, Add Business)
- Business list items with meta (owner, rating, updated date, views), tags (category, verified, premium), status (active/pending/suspended), and row actions
- Bulk actions toolbar (Approve, Suspend, Delete)
- Responsive layout with large-desktop refinements

(Use the HTML file as the source of truth for structure and content; convert to TSX + Tailwind.)

**INTEGRATION REQUIREMENTS:**
1. 🔄 Preserve All Existing Functionality
   - Maintain component-library patterns; no backend dependency
   - Keep view switcher state (List/Card/Map) and filters functional
   - Preserve bulk selection and toolbar logic
   - Maintain navigation and page structure (breadcrumb/top bar)

2. 🎨 Adapt Design Elements
   - Convert HTML/CSS to React TSX components with Tailwind utility classes using project tokens
   - Replace inline styles/hard-coded colors with design tokens from `design -system/`
   - Ensure responsive behavior per original media queries; include keyboard/focus-visible states
   - Use semantic landmarks (aside, header, main, nav) and ARIA where appropriate

3. 🔧 Technical Adaptations
   - Define TypeScript types for Business, Filters, ViewMode in `ui/components/types/`
   - Use React hooks for state (filters, selection, view mode)
   - Implement accessible event handlers (Enter/Space, ESC, focus management)
   - Optimize rendering by splitting into subcomponents; no premature memoization

4. 📱 Feature Integration
   - View switching (List/Card/Map) with stateful UI
   - Keyboard shortcuts: “/” focus search, “a” toggle select all, “Esc” clear selection
   - Loading/empty states for each view
   - Form validation for filters (basic constraints)
   - Animation transitions for item hover/selection and view changes (CSS transitions)

5. 🎯 Specific Adaptations Needed
   - Replace icons with Lucide or existing icon strategy; avoid CDN Font Awesome
   - Convert gradients, colors, shadow/radius to tokens/Tailwind config
   - Ensure dark-mode readiness (respect current Tailwind theme)
   - Ensure compatibility with `ui/components/*` patterns and exports
   - Maintain state management locally; mock data via constants for demo

**MULTIAGENT COORDINATION:**
Please use appropriate agent coordination:
- @agents-agument/core/ui-configurator-agent for design analysis
- @agents-agument/universal/react-developer for implementation
- Maintain context across agent handoffs
- Document component boundaries and token mappings inline as minimal comments

**DELIVERABLES:**
1. ✅ New TSX components:
   - ui/components/admin/Sidebar.tsx
   - ui/components/admin/TopBar.tsx
   - ui/components/admin/QuickStats.tsx
   - ui/components/admin/BusinessFilters.tsx
   - ui/components/admin/BusinessListItem.tsx
   - ui/components/admin/BulkToolbar.tsx
   - ui/components/admin/BusinessDirectory.tsx (composition)
2. ✅ Updated TypeScript interfaces in ui/components/types/admin.types.ts
3. ✅ Tailwind-based styling using project tokens; no hard-coded colors
4. ✅ Demo wire-up in a src/* demo page (add AdminDirectoryDemo.tsx)
5. ✅ Working interactions: filtering, selection, bulk actions, view switching
6. ✅ Responsive design (mobile → large desktop)
7. ✅ Brief change notes in PR description (no README updates unless requested)

**TESTING REQUIREMENTS:**
- Interface loads without console errors in Vite dev
- Filter controls update list state; keyboard shortcuts work
- Bulk selection and actions reflect selection count
- Verify empty/loading states and responsive breakpoints
- Accessibility: focus-visible, ARIA labels for controls, semantic regions
- Validate color/spacing/radius via design tokens (no inline hex values)
- Snapshot or visual smoke test with test/ prototype if applicable

Please analyze the provided UI design (admindashlisting2.html) and implement it step-by-step, maintaining our component-library standards and design tokens while delivering the same visual/interaction design in React + TypeScript + Tailwind.
```
