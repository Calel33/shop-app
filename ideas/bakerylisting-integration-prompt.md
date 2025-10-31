# 🎯 Business Listing Detail Page Integration Prompt

## 📋 Integration Request

I want to integrate a custom Business Listing Detail Page UI design into our **project-componets** component library. Please extract and adapt this interface to work with our React + TypeScript + Tailwind CSS stack.

---

## **CURRENT PROJECT CONTEXT:**

- **Framework**: React 19 + Vite
- **Styling**: Tailwind CSS 3 (token-based design system from `design -system/`)
- **Backend**: Demo-ready components (no live backend, uses mock data)
- **Language**: TypeScript 5 (strict, no `any` types)
- **Target Directory**: `ui/components/business-listing/` (new domain)
- **Demo File**: `src/BusinessListingDemo.tsx`
- **Existing Functionality**: Component library with admin, payment, digital-health domains

---

## **UI TO INTEGRATE:**

Source: `ideas/bakerylisting.html`

### **Design Overview:**
A public-facing business detail page for a local directory, showcasing "Sunrise Bakery & Café" with comprehensive business information.

**Layout Structure:**
- Sticky header with navigation (white background)
- Breadcrumb navigation
- Two-column main layout: content (left, flexible) + sidebar (right, 400px fixed)
- Hero section with image gallery
- Business header with title, ratings, and actions
- Sidebar with multiple info cards

**Key Visual Elements:**

1. **Header Navigation**
   - Logo: "LocalConnect" (blue, 24px, bold)
   - Nav links: Directory, Categories, Add Business, Sign In
   - White background, light gray bottom border
   - Sticky positioning
   - Hover: links turn blue (#2563eb)

2. **Breadcrumb**
   - Path: Home / Restaurants / Bakeries / Sunrise Bakery & Café
   - Links in blue, separators with slashes
   - Small font (14px), gray text

3. **Hero Section (Image Gallery)**
   - 400px height
   - Main image fills container
   - Gallery navigation dots at bottom center
   - 5 dots: active (white), inactive (white 40% opacity)
   - White rounded card with shadow

4. **Business Header (within hero card)**
   - Title row: Name + Verification badge
     - H1: "Sunrise Bakery & Café" (32px, bold)
     - Category: "Bakery • Café • Breakfast" (gray)
     - Verification badge: Green gradient, shield-check icon, "Verified Business"
   - Meta row:
     - Star rating (5 gold stars) + "4.8 (127 reviews)"
     - Distance: "0.8 miles away" with map marker icon
     - Status: "Open until 7:00 PM" with clock icon (green for open)
   - Description paragraph (full width, gray text)
   - Three action buttons:
     - Primary: "Call Now" with phone icon (blue)
     - Secondary: "Get Directions" with directions icon (white with blue border)
     - Secondary: "Visit Website" with globe icon

5. **Sidebar Info Cards** (all white cards with shadow)

   **Card 1: Business Information**
   - Icon title: "Business Information" with info-circle
   - Four items with icons:
     - Address: map-marker icon + "425 Oak Street, Springfield, IL 62701"
     - Phone: phone icon + clickable "(217) 555-1234"
     - Website: globe icon + link "sunrisebakery.com"
     - Email: envelope icon + link "hello@sunrisebakery.com"
   - Items separated by light borders

   **Card 2: Hours of Operation**
   - Icon title: "Hours of Operation" with clock
   - 7 rows: day name (left) + hours (right)
   - Current day highlighted in green
   - Consistent spacing grid layout

   **Card 3: Credentials & Recognition**
   - Icon title: "Credentials & Recognition" with award
   - Four proof items with colored icon boxes:
     - Calendar icon: "Established in 2018 • 6 years in business"
     - Certificate icon: "Licensed Food Service Establishment"
     - Leaf icon: "Certified Organic Ingredients"
     - Heart icon: "Community Choice Award 2023"
   - Each item: blue icon box + text on light gray background

   **Card 4: Customer Reviews**
   - Icon title: "Customer Reviews" with star
   - Placeholder preview:
     - Dashed border, gradient background
     - Large comments icon (gray)
     - Text: "Review system coming soon! Help us build trust in our community."

   **Last Updated Badge**
   - Light gray background, small text
   - Sync icon + "Last updated by owner on March 15, 2024"

**Color Palette:**
- Primary Blue: #2563eb, #1d4ed8
- Success Green: #059669, #10b981
- Warning/Gold: #f59e0b (stars)
- Gray Scale: #f8fafc, #f1f5f9, #e2e8f0, #cbd5e1, #94a3b8, #64748b, #475569, #334155, #0f172a
- Background: #f8fafc
- Borders: #e2e8f0

**Typography:**
- Font: Inter (system-ui fallback)
- H1: 32px, 700 weight
- Card titles: 18px, 700 weight
- Body: 14-16px, 400-500 weight
- Labels: 12-14px, 600 weight

---

## **INTEGRATION REQUIREMENTS:**

### 1. 🔄 **Preserve Project Standards**
   - Follow `constitution.md` v1.0.0 principles
   - Use design tokens from `design -system/` ONLY
   - No hard-coded colors, spacing, or shadows
   - Files <500 lines each
   - Export all types from `ui/components/types/business-listing.types.ts`

### 2. 🎨 **Adapt Design Elements**
   - Convert HTML/CSS to modular React components
   - Replace inline styles with Tailwind utility classes
   - Create component hierarchy:
     - `BusinessListingLayout.tsx` (full page with header + breadcrumb)
     - `BusinessHeader.tsx` (sticky nav)
     - `Breadcrumb.tsx` (reusable navigation trail)
     - `BusinessHero.tsx` (image gallery + business info)
     - `ImageGallery.tsx` (image carousel with dots)
     - `BusinessDetails.tsx` (title, ratings, description, actions)
     - `BusinessSidebar.tsx` (sidebar container)
     - `InfoCard.tsx` (reusable card wrapper)
     - `ContactInfo.tsx` (address, phone, website, email)
     - `HoursDisplay.tsx` (operating hours grid)
     - `CredentialsDisplay.tsx` (proof items)
     - `ReviewsPlaceholder.tsx` (coming soon card)
     - `LastUpdatedBadge.tsx` (timestamp display)
   - Responsive: stack sidebar below content on mobile
   - WCAG 2.1 AA compliance

### 3. 🔧 **Technical Adaptations**
   - Create TypeScript interfaces in `ui/components/types/business-listing.types.ts`:
     - `Business` (comprehensive business data)
     - `BusinessRating` (score, count)
     - `ContactInfo` (address, phone, website, email)
     - `BusinessHours` (day schedule map)
     - `Credential` (icon, text)
     - `GalleryImage` (url, alt text)
     - `BusinessStatus` (open/closed, hours display)
   - Use React 19 best practices
   - Implement image gallery state (active index)
   - Calculate current business status from hours
   - Handle responsive layout breakpoints

### 4. 📱 **Feature Integration**
   - **Image Gallery**:
     - Display main image
     - Dots navigation (5 images)
     - Click dot to change image
     - Active dot indicator
   - **Business Status**:
     - Calculate "Open until X" or "Closed"
     - Green text for open, red for closed
     - Based on current day/time vs hours
   - **Verification Badge**:
     - Green gradient background
     - Shield-check icon
     - Conditional rendering (only if verified)
   - **Contact Actions**:
     - Call Now: `tel:` link
     - Get Directions: external maps link
     - Visit Website: external link with target="_blank"
   - **Hours Highlighting**:
     - Detect current day
     - Apply green styling to active day
   - **Breadcrumb Navigation**:
     - Dynamic path from props
     - Clickable links (except current page)
   - **Responsive Behavior**:
     - Desktop: side-by-side layout
     - Tablet: narrower sidebar
     - Mobile: stacked (sidebar below content)

### 5. 🎯 **Specific Adaptations Needed**
   - Convert Font Awesome to Lucide icons:
     - `fa-shield-check` → `ShieldCheck`
     - `fa-star` → `Star`
     - `fa-map-marker-alt` → `MapPin`
     - `fa-clock` → `Clock`
     - `fa-phone` → `Phone`
     - `fa-directions` → `Navigation`
     - `fa-globe` → `Globe`
     - `fa-info-circle` → `Info`
     - `fa-envelope` → `Mail`
     - `fa-award` → `Award`
     - `fa-calendar` → `Calendar`
     - `fa-certificate` → `Award` (or `Badge`)
     - `fa-leaf` → `Leaf`
     - `fa-heart` → `Heart`
     - `fa-comments` → `MessageSquare`
     - `fa-sync` → `RefreshCw`
   - Gradient for verification badge: `bg-gradient-to-br from-green-600 to-green-500`
   - Star rating: 5 filled stars in gold color
   - Sticky header: `sticky top-0 z-50`
   - Two-column grid: `grid grid-cols-1 lg:grid-cols-[1fr_400px] gap-12`

---

## **DELIVERABLES:**

1. ✅ Complete React component library under `ui/components/business-listing/`
2. ✅ TypeScript interfaces in `ui/components/types/business-listing.types.ts`
3. ✅ Tailwind CSS styling (100% token-based)
4. ✅ Demo implementation in `src/BusinessListingDemo.tsx` with mock data for:
   - Bakery (from HTML)
   - Restaurant
   - Coffee shop
   - Retail store
5. ✅ Barrel export in `ui/components/business-listing/index.ts`
6. ✅ README.md with usage examples and customization guide
7. ✅ Integration summary: `BUSINESS_LISTING_INTEGRATION_COMPLETE.md`
8. ✅ Responsive design tested at breakpoints (mobile, tablet, desktop)
9. ✅ Accessibility: semantic HTML, ARIA labels, keyboard nav, screen reader support

---

## **TESTING REQUIREMENTS:**

- Verify image gallery navigation works (dot clicks)
- Test business status calculation logic (open/closed)
- Validate all contact action links (tel:, mailto:, external URLs)
- Confirm current day highlighting in hours display
- Test responsive layout at 320px, 768px, 1024px, 1440px widths
- Check breadcrumb navigation rendering with varying path depths
- Verify verification badge only shows when business is verified
- Test with businesses that have:
  - No website
  - No email
  - Different hour formats
  - No credentials
  - Different rating ranges (0-5 stars)
- Validate all icons render correctly
- Check keyboard navigation (tab through all interactive elements)
- Test screen reader announcements for status, ratings, hours

---

## **DESIGN SYSTEM MAPPING:**

Map CSS values to Tailwind/design tokens:

**Colors:**
- `#2563eb` → `blue-600`
- `#1d4ed8` → `blue-700`
- `#059669` → `green-600`
- `#10b981` → `green-500`
- `#f59e0b` → `amber-500`
- `#f8fafc` → `slate-50`
- `#e2e8f0` → `slate-200`
- `#64748b` → `slate-500`
- `#0f172a` → `slate-900`

**Spacing:**
- Max width: `max-w-7xl` (1600px becomes 1280px max, or use `max-w-[1600px]`)
- Column gap: `gap-12` (48px)
- Card padding: `p-6` (24px)
- Section spacing: `mb-8`, `mb-6`

**Typography:**
- H1: `text-3xl font-bold` (32px)
- Card title: `text-lg font-bold` (18px)
- Body: `text-sm` or `text-base`
- Small: `text-xs` (12px)

**Border Radius:**
- Cards: `rounded-2xl` (16px)
- Buttons: `rounded-lg` (8px)
- Icons: `rounded-lg` (8px)
- Badges: `rounded-lg` (8px)

**Shadows:**
- Cards: `shadow-sm` or design system token
- Hover: `shadow-md`

---

## **FILE STRUCTURE:**

```
ui/components/business-listing/
├── index.ts                          # Barrel export
├── README.md                         # Documentation + examples
├── BusinessListingLayout.tsx         # Full page layout
├── BusinessHeader.tsx                # Sticky nav
├── Breadcrumb.tsx                    # Navigation trail
├── BusinessHero.tsx                  # Hero section wrapper
├── ImageGallery.tsx                  # Image carousel
├── BusinessDetails.tsx               # Title, ratings, description, CTA
├── BusinessSidebar.tsx               # Sidebar container
├── InfoCard.tsx                      # Reusable card wrapper
├── ContactInfo.tsx                   # Contact details display
├── HoursDisplay.tsx                  # Operating hours
├── CredentialsDisplay.tsx            # Proof/credentials list
├── ReviewsPlaceholder.tsx            # Reviews coming soon
└── LastUpdatedBadge.tsx              # Update timestamp

ui/components/types/
└── business-listing.types.ts         # All interfaces

src/
└── BusinessListingDemo.tsx           # Demo with 4+ businesses
```

---

## **MOCK DATA STRUCTURE:**

Demo should include:

```typescript
interface MockDataStructure {
  businesses: Business[];              // 4+ complete examples
  categories: string[];                // Bakery, Restaurant, Cafe, Retail, etc.
  breadcrumbPaths: BreadcrumbPath[];   // Various navigation paths
}

interface Business {
  id: string;
  name: string;
  category: string[];
  verified: boolean;
  rating: BusinessRating;
  distance: string;
  status: BusinessStatus;
  description: string;
  gallery: GalleryImage[];             // 5 images per business
  contact: ContactInfo;
  hours: BusinessHours;
  credentials: Credential[];
  lastUpdated: string;
}
```

**Business Examples:**
1. **Sunrise Bakery & Café** (from HTML)
   - Bakery • Café • Breakfast
   - 4.8 rating, 127 reviews
   - Verified, 0.8 miles away
   - Open 6AM-7PM daily
   
2. **Mediterranean Grill House**
   - Restaurant • Mediterranean • Healthy
   - 4.6 rating, 89 reviews
   - Verified, 1.2 miles away
   - Open 11AM-10PM
   
3. **Artisan Coffee Roasters**
   - Coffee Shop • Roastery • Café
   - 4.9 rating, 203 reviews
   - Verified, 0.3 miles away
   - Open 7AM-6PM
   
4. **Urban Outfitters Boutique**
   - Retail • Fashion • Accessories
   - 4.5 rating, 45 reviews
   - Not verified, 2.1 miles away
   - Open 10AM-8PM

---

## **STATE MANAGEMENT:**

Demo should manage:

```typescript
// Gallery state
const [activeImageIndex, setActiveImageIndex] = useState(0);

// Business data
const [currentBusiness, setCurrentBusiness] = useState<Business>(businesses[0]);

// Responsive state (optional)
const [isMobile, setIsMobile] = useState(false);

// Hours calculation
const businessStatus = calculateStatus(currentBusiness.hours);
```

---

## **BUSINESS LOGIC:**

Implement helper functions:

```typescript
// Calculate if business is currently open
function calculateStatus(hours: BusinessHours): BusinessStatus {
  const now = new Date();
  const currentDay = now.toLocaleDateString('en-US', { weekday: 'long' });
  const currentTime = now.getHours() * 60 + now.getMinutes();
  // Compare with business hours
  // Return { isOpen: boolean, closingTime?: string, opensAt?: string }
}

// Format distance
function formatDistance(miles: number): string {
  return `${miles.toFixed(1)} miles away`;
}

// Format rating display
function formatRating(rating: BusinessRating): string {
  return `${rating.score.toFixed(1)} (${rating.count} reviews)`;
}
```

---

## **INTERACTIVE BEHAVIORS:**

1. **Image Gallery**:
   - Click dot → change main image
   - Active dot has white background
   - Smooth fade transition (optional enhancement)

2. **Contact Actions**:
   - Call Now → opens phone dialer on mobile
   - Get Directions → opens Google Maps with address
   - Visit Website → opens in new tab

3. **Hours Display**:
   - Current day text color changes to green
   - "Open until X" calculates from current time
   - Shows "Closed • Opens tomorrow at X" if after hours

4. **Responsive Behavior**:
   - Desktop (>1024px): sidebar on right, 400px fixed
   - Tablet (768-1023px): sidebar on right, narrower
   - Mobile (<768px): sidebar stacks below, full width

5. **Breadcrumb**:
   - All links clickable except last item
   - Slash separators between items
   - Last item is current page (not a link)

---

## **ACCESSIBILITY REQUIREMENTS:**

- `<nav>` for header navigation
- `<main>` for primary content
- `<aside>` for sidebar
- `aria-label` for image gallery navigation
- `aria-current="page"` for active breadcrumb
- `alt` text for all images (descriptive)
- `aria-label` for icon-only buttons/links
- Focus visible states on all interactive elements
- Keyboard navigation: Tab through all controls
- Star rating: `aria-label="4.8 out of 5 stars"`
- Status: `aria-live="polite"` for dynamic open/closed updates
- Color contrast: all text meets WCAG AA (4.5:1 minimum)

---

## **CONSTITUTION ALIGNMENT:**

This integration follows:
- ✅ **Principle 1**: Vertical slice (UI + types + demo + docs + tests)
- ✅ **Principle 2**: Type-safe (strict TypeScript, validated interfaces)
- ✅ **Principle 3**: Design system fidelity (100% token-based)
- ✅ **Principle 4**: Observability (document user actions: calls, directions, website visits)
- ✅ **Principle 5**: Transparency (integration summary + session log entry)

---

## **USE CASES:**

This component serves:
- Public-facing business directory detail pages
- Local business discovery platforms
- Review and listing aggregators
- Chamber of commerce directories
- Tourism and visitor guides
- "Find a business" features in city/municipal sites

**Reusability:**
- Can be adapted for any business type (restaurants, services, retail, etc.)
- Contact info cards reusable for profile pages
- Hours display reusable for any schedule display
- Image gallery reusable for product/portfolio showcases

---

Please analyze the provided UI design from `ideas/bakerylisting.html` and implement it step-by-step, maintaining our component library standards while delivering a polished, accessible business listing detail page with all interactive features and responsive behaviors.
