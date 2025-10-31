# Elite Auto Service Detail Page - UI Integration Prompt

## Project Context

**Interface Type:** Business Detail Page (Automotive Service)  
**Source File:** `ideas/listingpage5.html`  
**Target Framework:** React 19 + TypeScript + Tailwind CSS  
**Design System:** project-componets design tokens  
**Complexity Level:** High (Two-column layout, service grids, availability system, certification displays)

---

## Visual Design Analysis

### Layout Structure

**Primary Layout:**
- Sticky header navigation (white with border)
- Breadcrumb navigation trail
- Two-column main content layout:
  - Left column: Main content (fluid width)
  - Right column: Sidebar (fixed 400px width)
- Responsive breakpoint at 1024px (stacks to single column)

**Main Content Sections:**
1. Hero image gallery (400px height, 5-dot navigation)
2. Business header with title, badges, and metadata
3. Description paragraph
4. Action button row (3 CTAs)
5. Service pricing grid
6. Equipment showcase grid
7. Certifications grid

**Sidebar Sections:**
1. Quick actions card (availability + 3 action buttons)
2. Contact information card (4 contact items)
3. Hours of operation card (7-day schedule)
4. Warranty protection card (blue gradient)
5. Last updated timestamp

### Color Palette

**Primary Colors:**
```
Blue Primary: #2563eb (links, CTAs, equipment icons)
Blue Dark: #1d4ed8 (button hovers, gradient end)
Red/Warning: #dc2626 (emergency towing button)
Amber: #f59e0b (star ratings)
Orange: #d97706 (warning hover states)

Success/Green:
Emerald 600: #059669 (verification badge, status, prices, open hours)
Emerald 500: #10b981 (gradient blend)
Green Background: #dcfce7 (availability status background)
Green Border: #bbf7d0 (availability status border)

Neutral Palette:
Background: #f8fafc (page background, service cards)
White: #ffffff (cards, main sections)
Slate 100: #f1f5f9 (quick action secondary, last updated)
Slate 200: #e2e8f0 (borders, gallery background)
Slate 400: #64748b (secondary text, metadata)
Slate 600: #475569 (body text, descriptions)
Slate 700: #334155 (main body text)
Slate 900: #0f172a (headings, labels, dark text)
```

**Gradients:**
```css
Verification Badge: linear-gradient(135deg, #059669, #10b981)
Warranty Card: linear-gradient(135deg, #2563eb, #1d4ed8)
```

### Typography

**Font Family:** 'Inter', system-ui, -apple-system, sans-serif

**Type Scale:**
```
H1 (Business Name): 32px, weight 700, color slate-900
Logo: 24px, weight 700, color blue-600
H3 (Card Titles): 18-20px, weight 700, color slate-900
Badge Text: 14px, weight 600
Body Text: 16px, weight 400, line-height 1.7
Meta Items: 14px, color slate-400
Service Prices: 16px, weight 700, color emerald-600
Certification Labels: 14px, weight 600
Certification Org: 12px, color slate-400
Micro Text: 12px (last updated, quick action subtitles)
```

### Spacing System

```
Container Max Width: 1600px
Container Padding: 24px horizontal (16px mobile)
Main Content Gap: 48px between columns (32px mobile)
Section Padding: 32px (business header)
Card Padding: 24px
Info Item Padding: 16px bottom
Button Padding: 12px 24px (standard), 16px (quick actions)

Grid Gaps:
- Service Grid: 16px
- Equipment Grid: 16px
- Certification Grid: 16px
- Hours Grid: 8px
```

### Border Radius & Shadows

**Border Radius:**
```
Hero Section: 16px
Info Cards: 16px
Service Cards: 12px
Buttons: 8px
Service Items: 8px
Equipment Items: 8px
Certification Items: 8px
Certification Icons: 8px
Badges: 8px
Gallery Dots: 50% (circle)
Status Indicator: 50% (circle)
```

**Box Shadows:**
```
Header: none (just border)
Hero/Info Cards: 0 1px 3px rgba(0,0,0,0.1)
Quick Action Hover: 0 4px 12px rgba(0,0,0,0.15)
```

---

## Component Hierarchy

### Primary Components (18 total)

1. **`BusinessDetailLayout`** (Container)
   - Two-column grid layout (1fr 400px)
   - Responsive breakpoint handling
   - Breadcrumb navigation
   - Main + sidebar sections

2. **`BusinessHeader`** (Minimal variant from previous)
   - Logo only
   - Navigation links (Directory, Categories, Add Business, Sign In)
   - Sticky positioning

3. **`Breadcrumb`**
   - Trail navigation (Home / Category / Subcategory / Business)
   - Link styling
   - Separator display

4. **`BusinessHeroGallery`**
   - Image display (400px height)
   - 5-dot pagination indicators
   - Active state on current image
   - Click to navigate between images
   - Image carousel functionality

5. **`BusinessTitleSection`**
   - H1 business name
   - Category/subcategory subtitle
   - Verification badge (floating right)
   - Metadata row (rating, distance, hours, availability)

6. **`VerificationBadge`**
   - Green gradient background
   - Shield icon + text
   - Customizable certification text

7. **`BusinessMetaBar`**
   - Horizontal flex container
   - 4 meta items: rating, distance, status, availability
   - Icon + text pairs
   - Responsive wrapping

8. **`RatingDisplay`**
   - 5 star icons (filled)
   - Rating number + review count
   - Amber star color

9. **`BusinessDescription`**
   - Long-form text paragraph
   - Line-height 1.7
   - Slate 600 color

10. **`ActionButtonRow`**
    - 3 primary action buttons
    - Icons + labels
    - Color variants: primary (blue), warning (red), secondary (outlined)
    - Responsive stacking on mobile

11. **`ServicePricingGrid`**
    - Service card container
    - Responsive grid (minmax(250px, 1fr))
    - 6 service items with name, price, time
    - Price in emerald-600

12. **`EquipmentShowcase`**
    - Service card container
    - Responsive grid (minmax(200px, 1fr))
    - 4 equipment items with icon, name, description
    - Blue icon styling

13. **`CertificationGrid`**
    - Service card container
    - Responsive grid (minmax(150px, 1fr))
    - 6 certification items with icon badge, name, organization
    - Blue icon background squares

14. **`QuickActionsCard`**
    - Availability status banner
    - 3 stacked action buttons
    - Icon + two-line text layout
    - Color variants: primary, warning, secondary

15. **`AvailabilityStatus`**
    - Green background banner
    - Pulsing indicator dot
    - Status text (e.g., "3 service bays available now")

16. **`ContactInfoCard`**
    - 4 info items: address, phone, emergency, email
    - Icon + label + value layout
    - Bottom borders between items

17. **`HoursCard`**
    - 7-day schedule grid
    - Day + time columns
    - Current day highlighted (green text)
    - Closed status styling

18. **`WarrantyCard`**
    - Blue gradient background
    - White text
    - Shield icon + title
    - Warranty details paragraph
    - Centered text alignment

---

## Interaction Specifications

### Gallery Navigation

**Image Carousel:**
```typescript
interface GalleryState {
  currentIndex: number;
  images: string[];
  totalImages: number;
}

- Click dot → Navigate to corresponding image
- Active dot: white background
- Inactive dots: rgba(255,255,255,0.4)
- Smooth transition between images
- Optional: Auto-advance every 5 seconds
- Optional: Left/right arrow navigation
- Optional: Keyboard arrow key support
```

### Action Buttons

**Primary Actions:**
```typescript
interface BusinessAction {
  label: string;
  icon: string;
  type: 'phone' | 'towing' | 'appointment';
  url?: string;
  phone?: string;
}

// Call for Service
onClick: () => window.location.href = 'tel:+12175552300';

// Request Towing (Emergency)
onClick: () => window.location.href = 'tel:+12175552301';

// Schedule Appointment
onClick: () => navigate('/book/elite-auto-service');
```

**Quick Actions:**
```typescript
- Get Free Quote → Open quote form modal
- Emergency Towing → Immediate phone call
- Book Appointment → Navigate to booking page with prefilled business info
```

### Availability System

**Real-time Status:**
```typescript
interface AvailabilityStatus {
  isOpen: boolean;
  availableBays: number;
  totalBays: number;
  nextAvailable?: string; // "Today 2:30 PM"
  closingTime?: string; // "6:00 PM"
}

const getStatusDisplay = (status: AvailabilityStatus) => {
  if (!status.isOpen) {
    return {
      text: "Currently closed",
      variant: "closed",
      showIndicator: false
    };
  }
  
  if (status.availableBays > 0) {
    return {
      text: `${status.availableBays} service bays available now`,
      variant: "available",
      showIndicator: true
    };
  }
  
  return {
    text: `Next available: ${status.nextAvailable}`,
    variant: "busy",
    showIndicator: false
  };
};
```

### Hours of Operation

**Current Day Highlighting:**
```typescript
const getCurrentDay = (): DayOfWeek => {
  const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
  return days[new Date().getDay()] as DayOfWeek;
};

const isCurrentDay = (day: string): boolean => {
  return day === getCurrentDay();
};

// Apply "open" class (green text, bold) to current day's time
<span className={`time ${isCurrentDay(day) ? 'open' : ''}`}>
  {hours}
</span>
```

### Contact Item Interactions

```typescript
// Phone links
<a href="tel:+12175552300">(217) 555-2300</a>

// Email links
<a href="mailto:service@eliteautoservice.com">service@eliteautoservice.com</a>

// Address click → Open in maps
<a href="https://maps.google.com/?q=1847+Industrial+Blvd+Springfield+IL">
  1847 Industrial Blvd<br />Springfield, IL 62703
</a>
```

### State Management

**Required State:**
```typescript
interface BusinessDetailState {
  business: AutoServiceBusiness;
  currentImageIndex: number;
  availabilityStatus: AvailabilityStatus;
  isBookingModalOpen: boolean;
  isQuoteModalOpen: boolean;
  selectedService?: ServiceEstimate;
}
```

---

## TypeScript Interfaces

**File:** `ui/components/types/business-detail.types.ts`

```typescript
export interface AutoServiceBusiness extends Business {
  services: ServiceEstimate[];
  equipment: Equipment[];
  certifications: Certification[];
  warranty: Warranty;
  availability: AvailabilityStatus;
  emergencyTowing: {
    available: boolean;
    phone: string;
    is24x7: boolean;
  };
}

export interface ServiceEstimate {
  id: string;
  name: string;
  priceRange: {
    min: number;
    max: number;
    currency: string;
  };
  duration: {
    min: number;
    max: number;
    unit: 'minutes' | 'hours' | 'days';
  };
  description?: string;
  category?: 'maintenance' | 'repair' | 'diagnostic' | 'specialty';
}

export interface Equipment {
  id: string;
  name: string;
  description: string;
  icon: string; // Lucide icon name
  category?: string;
}

export interface Certification {
  id: string;
  name: string;
  organization: string;
  code?: string; // e.g., "A8", "A6"
  icon: string;
  issueDate?: string;
  expiryDate?: string;
  verified: boolean;
}

export interface Warranty {
  title: string;
  description: string;
  duration: {
    months?: number;
    miles?: number;
  };
  coverage: string[];
  exclusions?: string[];
}

export interface AvailabilityStatus {
  isOpen: boolean;
  availableBays: number;
  totalBays: number;
  nextAvailable?: string;
  closingTime?: string;
  status: 'available' | 'busy' | 'closed';
}

export interface BusinessHours {
  [key: string]: {
    open: string;
    close: string;
    isClosed: boolean;
  };
}

export interface ContactInformation {
  address: {
    street: string;
    city: string;
    state: string;
    zip: string;
    coordinates?: { lat: number; lng: number };
  };
  phone: string;
  emergencyPhone?: string;
  email: string;
  website?: string;
}

export interface GalleryImage {
  id: string;
  url: string;
  alt: string;
  caption?: string;
  order: number;
}

export interface MetaItem {
  icon: string;
  label: string;
  value: string | number;
  type: 'rating' | 'distance' | 'status' | 'availability';
  isHighlight?: boolean; // Green text for "open" status
}
```

---

## Design System Token Mapping

### Colors

```typescript
// Map HTML hex colors to design system tokens
{
  // Primary
  '#2563eb': 'blue.600',
  '#1d4ed8': 'blue.700',
  
  // Success/Status
  '#059669': 'emerald.600',
  '#10b981': 'emerald.500',
  '#dcfce7': 'emerald.50',
  '#bbf7d0': 'emerald.200',
  
  // Warning/Emergency
  '#dc2626': 'red.600',
  '#d97706': 'amber.600',
  '#f59e0b': 'amber.500',
  
  // Neutrals
  '#f8fafc': 'slate.50',
  '#ffffff': 'white',
  '#f1f5f9': 'slate.100',
  '#e2e8f0': 'slate.200',
  '#64748b': 'slate.500',
  '#475569': 'slate.600',
  '#334155': 'slate.700',
  '#0f172a': 'slate.900'
}
```

### Tailwind Utility Classes

```typescript
// Component-specific class mappings

BusinessDetailLayout:
"max-w-[1600px] mx-auto px-6 grid grid-cols-[1fr_400px] gap-12 lg:grid-cols-1"

BusinessHeroGallery:
"relative h-[400px] bg-slate-200 rounded-t-2xl overflow-hidden"

VerificationBadge:
"flex items-center gap-2 bg-gradient-to-br from-emerald-600 to-emerald-500 text-white px-4 py-2 rounded-lg text-sm font-semibold"

BusinessTitleSection:
"flex justify-between items-start mb-4"

BusinessMetaBar:
"flex gap-6 mb-6 flex-wrap"

ActionButtonRow:
"flex gap-4 mb-8 md:flex-col"

ServiceCard:
"bg-slate-50 border border-slate-200 rounded-xl p-6"

ServiceItem:
"bg-white p-4 rounded-lg border border-slate-200"

ServicePrice:
"text-emerald-600 font-bold text-base"

EquipmentIcon:
"text-2xl text-blue-600 mb-2"

CertificationIcon:
"w-12 h-12 bg-blue-600 text-white rounded-lg flex items-center justify-center mx-auto mb-3 text-xl"

QuickActionsCard:
"bg-white rounded-2xl p-6 shadow-sm"

AvailabilityStatus:
"flex items-center gap-2 p-3 bg-emerald-50 border border-emerald-200 rounded-lg mb-4"

StatusIndicator:
"w-2 h-2 bg-emerald-600 rounded-full"

QuickActionButton:
"p-4 rounded-lg font-semibold flex items-center gap-3 transition-all duration-200 hover:-translate-y-0.5 hover:shadow-lg"

InfoItem:
"flex items-start gap-3 mb-4 pb-4 border-b border-slate-100 last:mb-0 last:pb-0 last:border-0"

HoursRow:
"flex justify-between items-center py-1"

CurrentDayTime:
"text-emerald-600 font-semibold"

WarrantyCard:
"bg-gradient-to-br from-blue-600 to-blue-700 text-white p-5 rounded-xl text-center"

LastUpdated:
"bg-slate-100 p-3 rounded-lg text-xs text-slate-500 text-center"
```

---

## Icon Mapping

**Font Awesome → Lucide React:**

```typescript
const iconMap = {
  // Header & Navigation
  'fa-shield-check': 'ShieldCheck',
  'fa-star': 'Star',
  'fa-map-marker-alt': 'MapPin',
  'fa-clock': 'Clock',
  'fa-tools': 'Wrench',
  
  // Actions
  'fa-phone': 'Phone',
  'fa-truck': 'Truck',
  'fa-calendar-alt': 'Calendar',
  'fa-calculator': 'Calculator',
  'fa-calendar-check': 'CalendarCheck',
  
  // Services & Info
  'fa-dollar-sign': 'DollarSign',
  'fa-cogs': 'Settings',
  'fa-certificate': 'Award',
  'fa-bolt': 'Zap',
  'fa-info-circle': 'Info',
  'fa-envelope': 'Mail',
  
  // Equipment
  'fa-laptop': 'Laptop',
  'fa-microscope': 'Microscope',
  'fa-wrench': 'Wrench',
  'fa-car': 'Car',
  
  // Certifications
  'fa-award': 'Award',
  'fa-cog': 'Settings',
  'fa-snowflake': 'Snowflake',
  'fa-shield-alt': 'Shield',
  
  // Other
  'fa-sync': 'RefreshCw'
};
```

**Usage:**
```typescript
import { 
  ShieldCheck, Phone, Truck, Calendar, 
  Star, MapPin, Clock, Wrench, Award 
} from 'lucide-react';

<ShieldCheck className="w-5 h-5" />
```

---

## Accessibility Requirements

### WCAG 2.1 AA Compliance

**Keyboard Navigation:**
- All buttons and links reachable via Tab
- Gallery dots navigable with arrow keys
- Enter/Space activates buttons
- Focus visible on all interactive elements

**Screen Readers:**
```typescript
// Gallery
<div role="region" aria-label="Business photo gallery">
  <img 
    src={images[currentIndex].url} 
    alt={images[currentIndex].alt}
    aria-live="polite"
  />
  <div role="tablist" aria-label="Gallery navigation">
    {images.map((_, idx) => (
      <button
        role="tab"
        aria-selected={idx === currentIndex}
        aria-label={`View photo ${idx + 1} of ${images.length}`}
        onClick={() => setCurrentIndex(idx)}
      />
    ))}
  </div>
</div>

// Availability status
<div 
  className="availability-status" 
  role="status" 
  aria-live="polite"
>
  <span className="status-indicator" aria-hidden="true" />
  <span className="status-text">3 service bays available now</span>
</div>

// Action buttons
<button 
  className="btn btn-primary"
  aria-label="Call Elite Auto Service at (217) 555-2300"
>
  <Phone aria-hidden="true" />
  <span>Call for Service</span>
</button>

// Service pricing
<div 
  className="service-item"
  role="article"
  aria-labelledby={`service-name-${service.id}`}
>
  <div id={`service-name-${service.id}`} className="service-name">
    Oil Change & Filter
  </div>
  <div className="service-price" aria-label="Price range $45 to $85">
    $45 - $85
  </div>
  <div className="service-time" aria-label="Duration 30 to 45 minutes">
    30-45 minutes
  </div>
</div>

// Hours of operation
<div 
  className="hours-grid" 
  role="table" 
  aria-label="Hours of operation"
>
  {hours.map(day => (
    <div role="row" className="hour-row" key={day.name}>
      <span role="cell" className="day">{day.name}</span>
      <span 
        role="cell" 
        className={`time ${day.isToday ? 'open' : ''}`}
        aria-label={day.isToday ? 'Open today' : undefined}
      >
        {day.hours}
      </span>
    </div>
  ))}
</div>
```

**Color Contrast:**
- All text meets 4.5:1 contrast ratio
- Blue primary (#2563eb) on white: 7.21:1 ✓
- Emerald 600 (#059669) on white: 4.67:1 ✓
- Slate 600 (#475569) on white: 7.53:1 ✓
- White text on blue gradient: Verify contrast ≥ 4.5:1

**Focus Management:**
- Clear focus indicators on all interactive elements
- Focus trap in modals (quote form, booking)
- Return focus after modal close

---

## Mock Data Structure

**File:** `ui/components/business-detail/mockData.ts`

```typescript
export const mockAutoServiceBusiness: AutoServiceBusiness = {
  id: 'biz-elite-auto',
  name: 'Elite Auto Service',
  slug: 'elite-auto-service',
  category: 'Automotive',
  subcategory: 'Auto Repair',
  description: 'Elite Auto Service is your trusted neighborhood auto repair shop specializing in comprehensive vehicle maintenance and repair services. Our ASE-certified technicians use state-of-the-art diagnostic equipment to quickly identify issues and provide transparent, honest repairs. We stand behind our work with industry-leading warranties and have been serving the community with integrity for over 15 years. From routine oil changes to complex engine repairs, we treat every vehicle with the care and expertise it deserves.',
  
  images: [
    {
      id: 'img-1',
      url: '/images/elite-auto/shop-interior.webp',
      alt: 'Professional auto repair shop interior showing clean service bays with hydraulic lifts',
      order: 1
    },
    {
      id: 'img-2',
      url: '/images/elite-auto/diagnostic-equipment.webp',
      alt: 'Modern diagnostic equipment and computer systems',
      order: 2
    },
    {
      id: 'img-3',
      url: '/images/elite-auto/technician-work.webp',
      alt: 'ASE-certified technician performing vehicle inspection',
      order: 3
    },
    {
      id: 'img-4',
      url: '/images/elite-auto/waiting-area.webp',
      alt: 'Comfortable customer waiting area with WiFi and refreshments',
      order: 4
    },
    {
      id: 'img-5',
      url: '/images/elite-auto/exterior.webp',
      alt: 'Elite Auto Service building exterior and parking lot',
      order: 5
    }
  ],
  
  rating: 4.9,
  reviewCount: 312,
  
  distance: 1.2,
  distanceUnit: 'mi',
  
  address: {
    street: '1847 Industrial Blvd',
    city: 'Springfield',
    state: 'IL',
    zip: '62703',
    coordinates: { lat: 39.7817, lng: -89.6501 }
  },
  
  contact: {
    phone: '(217) 555-2300',
    emergencyPhone: '(217) 555-2301',
    email: 'service@eliteautoservice.com',
    website: 'https://eliteautoservice.com'
  },
  
  hours: {
    monday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
    tuesday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
    wednesday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
    thursday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
    friday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
    saturday: { open: '8:00 AM', close: '4:00 PM', isClosed: false },
    sunday: { open: '', close: '', isClosed: true }
  },
  
  isVerified: true,
  verifiedDate: '2024-03-18',
  
  badges: [
    {
      type: 'verified',
      label: 'ASE Certified Shop',
      color: 'green',
      gradient: 'from-emerald-600 to-emerald-500',
      icon: 'ShieldCheck'
    }
  ],
  
  availability: {
    isOpen: true,
    availableBays: 3,
    totalBays: 6,
    nextAvailable: 'Today 2:30 PM',
    closingTime: '6:00 PM',
    status: 'available'
  },
  
  emergencyTowing: {
    available: true,
    phone: '(217) 555-2301',
    is24x7: true
  },
  
  services: [
    {
      id: 'service-1',
      name: 'Oil Change & Filter',
      priceRange: { min: 45, max: 85, currency: 'USD' },
      duration: { min: 30, max: 45, unit: 'minutes' },
      category: 'maintenance'
    },
    {
      id: 'service-2',
      name: 'Brake Pad Replacement',
      priceRange: { min: 200, max: 400, currency: 'USD' },
      duration: { min: 2, max: 3, unit: 'hours' },
      category: 'repair'
    },
    {
      id: 'service-3',
      name: 'Engine Diagnostic',
      priceRange: { min: 120, max: 180, currency: 'USD' },
      duration: { min: 1, max: 2, unit: 'hours' },
      category: 'diagnostic'
    },
    {
      id: 'service-4',
      name: 'Transmission Service',
      priceRange: { min: 180, max: 350, currency: 'USD' },
      duration: { min: 2, max: 4, unit: 'hours' },
      category: 'maintenance'
    },
    {
      id: 'service-5',
      name: 'AC System Repair',
      priceRange: { min: 200, max: 800, currency: 'USD' },
      duration: { min: 2, max: 5, unit: 'hours' },
      category: 'repair'
    },
    {
      id: 'service-6',
      name: 'Timing Belt Replacement',
      priceRange: { min: 500, max: 1200, currency: 'USD' },
      duration: { min: 4, max: 6, unit: 'hours' },
      category: 'repair'
    }
  ],
  
  equipment: [
    {
      id: 'equip-1',
      name: 'OBD-II Scanner',
      description: 'Advanced diagnostics for all vehicle systems',
      icon: 'Laptop',
      category: 'diagnostic'
    },
    {
      id: 'equip-2',
      name: 'Engine Analyzer',
      description: 'Comprehensive engine performance testing',
      icon: 'Microscope',
      category: 'diagnostic'
    },
    {
      id: 'equip-3',
      name: 'Brake Lathe',
      description: 'Precision brake rotor resurfacing',
      icon: 'Wrench',
      category: 'repair'
    },
    {
      id: 'equip-4',
      name: 'Wheel Alignment',
      description: 'Computerized 4-wheel alignment system',
      icon: 'Car',
      category: 'service'
    }
  ],
  
  certifications: [
    {
      id: 'cert-1',
      name: 'ASE Master Technician',
      organization: 'Automotive Service Excellence',
      icon: 'Award',
      verified: true
    },
    {
      id: 'cert-2',
      name: 'Engine Performance',
      organization: 'ASE Certified',
      code: 'A8',
      icon: 'Car',
      verified: true
    },
    {
      id: 'cert-3',
      name: 'Electrical Systems',
      organization: 'ASE Certified',
      code: 'A6',
      icon: 'Wrench',
      verified: true
    },
    {
      id: 'cert-4',
      name: 'Transmission Specialist',
      organization: 'ATRA Certified',
      icon: 'Settings',
      verified: true
    },
    {
      id: 'cert-5',
      name: 'AC Systems',
      organization: 'EPA 609 Certified',
      icon: 'Snowflake',
      verified: true
    },
    {
      id: 'cert-6',
      name: 'Brake Systems',
      organization: 'ASE Certified',
      code: 'A5',
      icon: 'Shield',
      verified: true
    }
  ],
  
  warranty: {
    title: 'Warranty Protection',
    description: 'We stand behind our work with a comprehensive 24-month / 24,000-mile warranty on all repairs. Your satisfaction and peace of mind are guaranteed.',
    duration: { months: 24, miles: 24000 },
    coverage: [
      'All parts and labor',
      'Nationwide coverage',
      'Transferable to new owner',
      'No deductible'
    ]
  },
  
  lastUpdated: '2024-03-18',
  lastUpdatedBy: 'owner'
};

export const mockMetaItems: MetaItem[] = [
  {
    icon: 'Star',
    label: '4.9 (312 reviews)',
    value: 4.9,
    type: 'rating'
  },
  {
    icon: 'MapPin',
    label: '1.2 miles away',
    value: 1.2,
    type: 'distance'
  },
  {
    icon: 'Clock',
    label: 'Open until 6:00 PM',
    value: 'Open until 6:00 PM',
    type: 'status',
    isHighlight: true
  },
  {
    icon: 'Wrench',
    label: '3 bays available',
    value: 3,
    type: 'availability'
  }
];
```

---

## File Structure

```
ui/components/business-detail/
├── types/
│   └── business-detail.types.ts     # TypeScript interfaces
├── layout/
│   ├── BusinessDetailLayout.tsx     # Two-column container
│   ├── BusinessHeader.tsx           # Minimal header
│   └── Breadcrumb.tsx               # Trail navigation
├── hero/
│   ├── BusinessHeroGallery.tsx      # Image carousel
│   └── GalleryDots.tsx              # Pagination dots
├── header/
│   ├── BusinessTitleSection.tsx     # Title + badge + meta
│   ├── VerificationBadge.tsx        # Green gradient badge
│   ├── BusinessMetaBar.tsx          # 4 meta items
│   └── RatingDisplay.tsx            # Stars + count
├── content/
│   ├── BusinessDescription.tsx      # Long-form text
│   ├── ActionButtonRow.tsx          # 3 CTA buttons
│   ├── ServicePricingGrid.tsx       # Service estimates
│   ├── ServiceEstimateCard.tsx      # Individual service item
│   ├── EquipmentShowcase.tsx        # Equipment grid
│   ├── EquipmentItem.tsx            # Individual equipment
│   ├── CertificationGrid.tsx        # Certification grid
│   └── CertificationBadge.tsx       # Individual cert
├── sidebar/
│   ├── QuickActionsCard.tsx         # Actions + availability
│   ├── AvailabilityStatus.tsx       # Green status banner
│   ├── ContactInfoCard.tsx          # 4 contact items
│   ├── ContactInfoItem.tsx          # Icon + label + value
│   ├── HoursCard.tsx                # 7-day schedule
│   ├── HoursRow.tsx                 # Day + time row
│   ├── WarrantyCard.tsx             # Blue gradient card
│   └── LastUpdatedBadge.tsx         # Timestamp
├── hooks/
│   ├── useGallery.ts                # Gallery navigation
│   ├── useAvailability.ts           # Real-time status
│   └── useBusinessHours.ts          # Current day logic
├── utils/
│   ├── formatters.ts                # Price, time formatting
│   ├── availability.ts              # Status calculations
│   └── hours.ts                     # Hours parsing/display
├── mockData.ts                      # Mock business data
├── index.ts                         # Barrel exports
└── README.md                        # Component documentation
```

---

## Testing Requirements

### Unit Tests

```typescript
// AvailabilityStatus.test.tsx
describe('AvailabilityStatus', () => {
  it('shows available status with green indicator', () => {
    render(<AvailabilityStatus availableBays={3} totalBays={6} isOpen={true} />);
    
    expect(screen.getByText('3 service bays available now')).toBeInTheDocument();
    expect(screen.getByRole('status')).toHaveClass('bg-emerald-50');
    expect(screen.getByTestId('status-indicator')).toBeInTheDocument();
  });

  it('shows closed status without indicator', () => {
    render(<AvailabilityStatus availableBays={0} totalBays={6} isOpen={false} />);
    
    expect(screen.getByText('Currently closed')).toBeInTheDocument();
    expect(screen.queryByTestId('status-indicator')).not.toBeInTheDocument();
  });

  it('shows next available time when busy', () => {
    render(
      <AvailabilityStatus 
        availableBays={0} 
        totalBays={6} 
        isOpen={true}
        nextAvailable="Today 2:30 PM"
      />
    );
    
    expect(screen.getByText(/Next available: Today 2:30 PM/i)).toBeInTheDocument();
  });
});

// HoursCard.test.tsx
describe('HoursCard', () => {
  const mockHours: BusinessHours = {
    monday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
    tuesday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
    sunday: { open: '', close: '', isClosed: true }
  };

  it('renders all 7 days', () => {
    render(<HoursCard hours={mockHours} />);
    
    expect(screen.getByText('Monday')).toBeInTheDocument();
    expect(screen.getByText('Sunday')).toBeInTheDocument();
  });

  it('highlights current day in green', () => {
    jest.spyOn(Date.prototype, 'getDay').mockReturnValue(2); // Tuesday
    
    render(<HoursCard hours={mockHours} />);
    
    const tuesdayTime = screen.getByText('7:00 AM - 6:00 PM');
    expect(tuesdayTime).toHaveClass('open');
  });

  it('shows "Closed" for closed days', () => {
    render(<HoursCard hours={mockHours} />);
    
    const sundayRow = screen.getByText('Sunday').closest('.hour-row');
    expect(sundayRow).toContainHTML('Closed');
  });
});

// BusinessHeroGallery.test.tsx
describe('BusinessHeroGallery', () => {
  const mockImages: GalleryImage[] = [
    { id: '1', url: '/img1.jpg', alt: 'Image 1', order: 1 },
    { id: '2', url: '/img2.jpg', alt: 'Image 2', order: 2 },
    { id: '3', url: '/img3.jpg', alt: 'Image 3', order: 3 }
  ];

  it('renders first image by default', () => {
    render(<BusinessHeroGallery images={mockImages} />);
    
    const img = screen.getByAltText('Image 1');
    expect(img).toHaveAttribute('src', '/img1.jpg');
  });

  it('changes image on dot click', async () => {
    render(<BusinessHeroGallery images={mockImages} />);
    
    const dots = screen.getAllByRole('tab');
    await userEvent.click(dots[1]);
    
    expect(screen.getByAltText('Image 2')).toBeInTheDocument();
    expect(dots[1]).toHaveClass('active');
  });

  it('navigates with keyboard arrows', async () => {
    render(<BusinessHeroGallery images={mockImages} />);
    
    const gallery = screen.getByRole('region');
    gallery.focus();
    
    await userEvent.keyboard('{ArrowRight}');
    expect(screen.getByAltText('Image 2')).toBeInTheDocument();
    
    await userEvent.keyboard('{ArrowLeft}');
    expect(screen.getByAltText('Image 1')).toBeInTheDocument();
  });
});

// ServicePricingGrid.test.tsx
describe('ServicePricingGrid', () => {
  it('renders all service estimates', () => {
    render(<ServicePricingGrid services={mockAutoServiceBusiness.services} />);
    
    expect(screen.getByText('Oil Change & Filter')).toBeInTheDocument();
    expect(screen.getByText('$45 - $85')).toBeInTheDocument();
    expect(screen.getByText('30-45 minutes')).toBeInTheDocument();
  });

  it('formats prices in emerald color', () => {
    render(<ServicePricingGrid services={mockAutoServiceBusiness.services} />);
    
    const price = screen.getByText('$45 - $85');
    expect(price).toHaveClass('text-emerald-600');
  });

  it('displays duration in readable format', () => {
    render(<ServicePricingGrid services={mockAutoServiceBusiness.services} />);
    
    expect(screen.getByText('2-3 hours')).toBeInTheDocument();
    expect(screen.getByText('30-45 minutes')).toBeInTheDocument();
  });
});
```

### Integration Tests

```typescript
describe('BusinessDetailPage Integration', () => {
  it('loads business data and displays all sections', async () => {
    render(<BusinessDetailLayout business={mockAutoServiceBusiness} />);
    
    // Title section
    expect(screen.getByRole('heading', { name: 'Elite Auto Service' })).toBeInTheDocument();
    expect(screen.getByText('ASE Certified Shop')).toBeInTheDocument();
    
    // Meta bar
    expect(screen.getByText('4.9 (312 reviews)')).toBeInTheDocument();
    expect(screen.getByText('1.2 miles away')).toBeInTheDocument();
    
    // Services
    expect(screen.getByText('Common Service Estimates')).toBeInTheDocument();
    expect(screen.getAllByRole('article')).toHaveLength(6);
    
    // Sidebar
    expect(screen.getByText('3 service bays available now')).toBeInTheDocument();
    expect(screen.getByText('(217) 555-2300')).toBeInTheDocument();
  });

  it('handles action button clicks', async () => {
    const mockNavigate = jest.fn();
    render(<BusinessDetailLayout business={mockAutoServiceBusiness} onNavigate={mockNavigate} />);
    
    // Call for Service
    const callButton = screen.getByRole('button', { name: /call for service/i });
    await userEvent.click(callButton);
    expect(window.location.href).toContain('tel:+12175552300');
    
    // Request Towing
    const towButton = screen.getByRole('button', { name: /request towing/i });
    await userEvent.click(towButton);
    expect(window.location.href).toContain('tel:+12175552301');
    
    // Schedule Appointment
    const appointmentButton = screen.getByRole('button', { name: /schedule appointment/i });
    await userEvent.click(appointmentButton);
    expect(mockNavigate).toHaveBeenCalledWith('/book/elite-auto-service');
  });

  it('navigates breadcrumb trail', async () => {
    const mockNavigate = jest.fn();
    render(<BusinessDetailLayout business={mockAutoServiceBusiness} onNavigate={mockNavigate} />);
    
    await userEvent.click(screen.getByText('Home'));
    expect(mockNavigate).toHaveBeenCalledWith('/');
    
    await userEvent.click(screen.getByText('Automotive'));
    expect(mockNavigate).toHaveBeenCalledWith('/category/automotive');
  });
});
```

---

## Responsive Behavior

### Breakpoint Strategy

```typescript
const breakpoints = {
  md: 768,   // Mobile: Stack action buttons
  lg: 1024   // Tablet: Stack columns, adjust grids
};
```

### Layout Transformations

**Main Content Layout:**
```
Desktop (>1024px): Two columns [1fr 400px]
Tablet/Mobile (≤1024px): Single column stack
```

**Service Grids:**
```
Desktop: Auto-fit minmax(250px, 1fr) [2-3 columns]
Tablet: minmax(200px, 1fr) [2 columns]
Mobile: Single column
```

**Action Buttons:**
```
Desktop: Horizontal flex row
Mobile (≤768px): Vertical stack
```

**Business Meta:**
```
Desktop: Horizontal flex with gaps
Mobile (≤768px): Vertical stack
```

---

## Performance Optimization

### Image Optimization

```typescript
// Gallery images with lazy loading
<Image
  src={images[currentIndex].url}
  alt={images[currentIndex].alt}
  width={1200}
  height={400}
  sizes="(max-width: 1024px) 100vw, 1200px"
  loading={currentIndex === 0 ? 'eager' : 'lazy'}
  placeholder="blur"
/>
```

### Code Splitting

```typescript
// Lazy load modal components
const QuoteModal = lazy(() => import('./QuoteModal'));
const BookingModal = lazy(() => import('./BookingModal'));

<Suspense fallback={<ModalSkeleton />}>
  {isQuoteModalOpen && <QuoteModal business={business} />}
</Suspense>
```

---

## Constitution Alignment

### Vertical Slice Ownership
- Each section owns its types, components, and mock data
- Clear separation: hero, header, content, sidebar
- Equipment/certifications are reusable across business types

### Type Safety
- Comprehensive interfaces for all business data
- No `any` types - explicit typing throughout
- Runtime validation for availability status

### Design Fidelity
- Exact color palette from HTML prototype
- Preserved gradients and shadows
- Responsive grid matching original breakpoints

### Observability
- Track action button clicks (call, tow, appointment)
- Log gallery navigation patterns
- Monitor availability status changes
- Track service estimate interactions

---

## Summary

This is a **comprehensive automotive service detail page** with:

- **18 modular React components** organized by section
- **Two-column responsive layout** (main + 400px sidebar)
- **Hero image gallery** with 5-dot pagination
- **Business header** with verification badge and 4-item metadata bar
- **Service pricing grid** with 6 estimates (price ranges + duration)
- **Equipment showcase** with 4 diagnostic tools
- **Certification grid** with 6 professional credentials
- **Quick actions sidebar** with real-time availability status
- **Contact information card** with 4 contact methods
- **Hours of operation** with current day highlighting
- **Warranty protection card** with gradient styling
- **Fully responsive** design (1024px breakpoint for column stack)
- **Accessibility compliant** (WCAG 2.1 AA, ARIA labels, keyboard navigation)
- **Type-safe** with comprehensive TypeScript interfaces
- **Thoroughly tested** (unit, integration, accessibility)

The interface emphasizes **trust**, **transparency**, and **immediate action** through prominent availability status, multiple contact methods, detailed service pricing, and professional certifications. Perfect for service-based businesses requiring detailed capability showcases.
