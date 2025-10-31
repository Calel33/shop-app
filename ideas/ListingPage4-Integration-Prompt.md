# UI Integration Prompt — Listing Page 4 (Oakwood Veterinary Clinic)

```
I want to integrate a custom UI design into our Project Components Library project. Please extract and adapt this interface to work with our React 19 + Vite + TypeScript 5 + Tailwind CSS 3 stack.

**CURRENT PROJECT CONTEXT:**
- Framework: React 19 + Vite
- Styling: Tailwind CSS 3 using project design tokens (see "design -system" directory); no hard-coded colors/sizes
- Backend: N/A (frontend component library; demo data via local fixtures)
- Language: TypeScript
- Current file: src/components/listing/OakwoodVeterinaryClinic.tsx (compose from subcomponents under src/components/listing/)
- Existing functionality: Component demos under src/* and reusable UI under ui/components/* with strict types and tokens

**UI TO INTEGRATE:**
Adapt the HTML/CSS from ideas/listingpage4.html. Key sections:
- Sticky header with logo and nav; breadcrumb trail
- Two-column layout (content + sidebar)
- Hero image gallery with dot navigation
- Business header: title, categories, verification badge, meta (rating, distance, hours, emergency availability)
- Action buttons (Book Appointment, Emergency Line, Call Clinic, Get Directions)
- Specializations grid (cards with icon, name, description)
- Veterinarians section (cards with photo, name, title, credentials, experience)
- Pet care tips list (info cards)
- Sidebar: Emergency Contact card, Appointment Booking CTA, Clinic Information, Hours of Operation with emergency note, Credentials & Certifications, Last Updated

**INTEGRATION REQUIREMENTS:**
1. Preserve All Existing Functionality
   - Follow component-library demo pattern (no network calls; use props/fixtures)
   - Keep responsive behavior and sticky header
   - Preserve accessibility, routing-friendly anchors (convert plain anchors to Link/button stubs as appropriate)

2. Adapt Design Elements
   - Convert to React function components
   - Replace inline CSS with Tailwind utilities mapped to our tokens (colors, spacing, radius, shadows)
   - Use Lucide icons (or the project’s existing icon approach) in place of font-awesome
   - Ensure responsive design for mobile, tablet, desktop breakpoints

3. Technical Adaptations
   - Define TypeScript interfaces in ui/components/types/listing.types.ts (e.g., VetClinicBusiness, Specialization, Veterinarian, PetTip, EmergencyContact, HourRow)
   - Implement state for gallery active index with keyboard navigation
   - Provide callbacks for key actions: onBookAppointment, onEmergency, onCallClinic, onGetDirections
   - Keep each component <500 lines and split responsibilities

4. Feature Integration
   - Gallery with clickable/keyboard-accessible dots
   - SpecializationCard hover elevation
   - Veterinarian cards with images (alt text from props)
   - Pet Tips info items with emphasis styles
   - Sidebar emergency card with distinct styling and 24/7 note
   - Hours list highlighting the open day/state; emergency banner

5. Specific Adaptations Needed
   - Replace all color hexes with tokenized Tailwind classes
   - Use semantic markup and ARIA where needed (nav, main, aside, section headings)
   - Optional subtle transitions via CSS only; avoid heavy animation libs unless already present
   - Ensure compatibility with existing product primitives where applicable

**MULTIAGENT COORDINATION:**
- @agents-agument/core/ui-configurator-agent for design-token mapping
- @agents-agument/universal/react-developer for implementation
- Maintain context across handoffs

**DELIVERABLES:**
1. React components under src/components/listing/:
   - ListingHeader, Breadcrumbs
   - ImageGallery (with dots), BusinessHeaderMeta
   - ActionButtons (with Emergency variant)
   - SpecializationsSection, SpecializationCard
   - VeterinariansSection, VeterinarianCard
   - PetTipsSection, PetTipItem
   - Sidebar: EmergencyContactCard, AppointmentBookingCard, ClinicInfoCard, HoursCard, CredentialsCard, LastUpdated
   - OakwoodVeterinaryClinic (composition demo)
2. Updated TypeScript types in ui/components/types/listing.types.ts
3. Tailwind tokenized styling; no inline styles
4. Demo usage in src/OakwoodVeterinaryClinicDemo.tsx with fixture data
5. Working interactions (gallery, buttons) and keyboard support
6. Responsive behavior across breakpoints

**TESTING REQUIREMENTS:**
- Build passes (npm run build)
- Components render without runtime errors
- Verify gallery navigation via mouse and keyboard
- Validate responsive behavior at sm/md/lg breakpoints
- Check ARIA roles/labels and focus-visible states
- Ensure no hard-coded colors/sizes; only token-based utilities

Please analyze the provided UI design and implement it step-by-step, maintaining our component-library patterns while delivering the exact visual design requested.
```
