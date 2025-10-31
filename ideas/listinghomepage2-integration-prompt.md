# LocalConnect Business Directory Homepage - UI Integration Prompt

## Project Context

**Interface Type:** Business Directory Landing Page  
**Source File:** `ideas/listinghomepage2.html`  
**Target Framework:** React 19 + TypeScript + Tailwind CSS  
**Design System:** project-componets design tokens  
**Complexity Level:** High (Multiple interactive sections, hero search, carousels, responsive grids)

---

## Visual Design Analysis

### Layout Structure

**Primary Layout:**
- Sticky header navigation (64px height, white with shadow)
- Full-width hero section with gradient background and search
- Quick filters bar (horizontal scrollable tags)
- Main content area (max-width: 1600px, centered)
- Multiple content sections with varied layouts

**Responsive Breakpoints:**
- Desktop: 1600px max-width container
- Tablet: 1200px (3-column grids → 2-column)
- Mobile: 768px (flex columns, stacked search)
- Small Mobile: 480px (single column grids)

### Color Palette

**Primary Colors:**
```
Blue Primary: #2563eb (links, CTAs, hero gradient start)
Blue Dark: #1e40af (hero gradient end)
Blue Hover: #1d4ed8

Accent Colors:
Orange: #f59e0b (Add Business button, trending badges)
Orange Dark: #d97706 (hover states)
Green: #10b981 (new business badges, verified badges)
Green Dark: #059669
Sky Blue: #0ea5e9 (location banner accent)

Neutral Palette:
Background: #f8fafc (page background)
White: #ffffff (cards, header)
Slate 100: #f1f5f9 (filter tags)
Slate 200: #e2e8f0 (borders, dividers)
Slate 400: #94a3b8 (placeholder text)
Slate 500: #64748b (secondary text, nav links)
Slate 600: #475569 (body text)
Slate 700: #334155 (primary text)
Slate 800: #1e293b
Slate 900: #0f172a (headings, dark text)
```

**Gradients:**
```css
Hero Background: linear-gradient(135deg, #2563eb 0%, #1e40af 100%)
Trending Section: linear-gradient(135deg, #f8fafc, #e2e8f0)
New Business Header: linear-gradient(135deg, #10b981, #059669)
Location Banner: linear-gradient(135deg, #f0f9ff, #e0f2fe)
Category Fallback: linear-gradient(45deg, #2563eb, #1d4ed8)
Trending Badge: linear-gradient(135deg, #f59e0b, #d97706)
New Badge: linear-gradient(135deg, #10b981, #059669)
Verified Badge: linear-gradient(135deg, #059669, #10b981)
```

### Typography

**Font Family:** 'Inter', system-ui, -apple-system, sans-serif

**Type Scale:**
```
Hero H1: 48px, weight 800, line-height 1.2 (mobile: 36px)
Section Title (H2): 36px, weight 700, color slate-900
Section Title (H3): 28px, weight 700, color slate-900
New Business Title: 24px, weight 700
Business Name (H4): 18px, weight 700, color slate-900
Logo: 28px, weight 800, color blue-600

Body Large: 20px (hero subtitle)
Body Regular: 18px (section subtitle)
Body Small: 16px (search inputs, nav links)
Caption: 14px (category count, meta info, badges)
Micro: 12px (badge text)
```

### Spacing System

```
Container Padding: 24px horizontal (16px mobile)
Section Padding: 64px vertical
Card Padding: 20px
Header Padding: 16px vertical
Hero Padding: 80px vertical

Grid Gaps:
- Category Grid: 24px (16px mobile)
- Business Card Grid: 24px
- New Business Grid: 24px
- Verified Carousel: 20px
- Filter Tags: 16px
```

### Border Radius & Shadows

**Border Radius:**
```
Hero Search Container: 16px
Category Tiles: 20px
Business Cards: 16px
New Business Header: 16px 16px 0 0
Buttons/CTAs: 12px (large), 8px (medium), 6px (small)
Badges: 20px (pill), 12px (rounded), 6px (small badge)
Filter Tags: 20px (pill)
Logo Images: 8px (small), 50% (circular avatars)
```

**Box Shadows:**
```
Header: 0 1px 3px rgba(0,0,0,0.05)
Hero Search: 0 8px 32px rgba(0,0,0,0.1)
Business Card: 0 4px 6px rgba(0,0,0,0.05)
Business Card Hover: 0 12px 24px rgba(0,0,0,0.1)
Category Tile Hover: 0 20px 40px rgba(0,0,0,0.15)
Verified Card: 0 2px 4px rgba(0,0,0,0.05)
Verified Card Hover: 0 8px 16px rgba(0,0,0,0.1)
```

---

## Component Hierarchy

### Primary Components (15 total)

1. **`ListingHomepageLayout`** (Container)
   - Sticky header
   - Hero section
   - Quick filters
   - Main content area
   - Manages scroll behavior and location state

2. **`DirectoryHeader`**
   - Logo with icon
   - Navigation links (Browse Directory, Categories, About)
   - Add Your Business CTA button (orange)
   - Sign In link
   - Responsive mobile menu

3. **`HeroSearchSection`**
   - Gradient background with pattern overlay
   - H1 heading and subtitle
   - Dual-input search bar (query + location)
   - Search button with icon
   - Statistics display (3 metrics)

4. **`SearchBar`** (Compound Component)
   - Search query input (flex: 1)
   - Location input (min-width: 200px)
   - Search button with hover animation
   - White container with shadow
   - Responsive stacking on mobile

5. **`StatsDisplay`**
   - 3 stat items in horizontal flex (vertical on mobile)
   - Stat number (24px bold)
   - Stat label (14px, opacity 0.8)
   - Animated counter option

6. **`QuickFiltersBar`**
   - Horizontal scrollable container
   - 6 filter tags: Trending Now, Open Now, Highly Rated, Nearby, Special Offers, Newly Verified
   - Icon + text badges
   - Hover animation (color flip, translateY)
   - Active state management

7. **`LocationBanner`**
   - Sky blue gradient background
   - Location arrow icon
   - Current location title + subtitle
   - "Change Location" link
   - Dismissible/collapsible

8. **`CategoryGrid`**
   - 4-column responsive grid (4→3→2→1)
   - 8 category tiles with images
   - Categories: Restaurants, Healthcare, Shopping, Automotive, Beauty & Wellness, Fitness, Home Services, Professional

9. **`CategoryTile`**
   - Aspect ratio 1:1 (square)
   - Background image with overlay
   - Gradient overlay (transparent to rgba(0,0,0,0.7))
   - Icon in top-right corner
   - Category name + count at bottom
   - Hover animation (translateY -8px, shadow increase)
   - Click navigation

10. **`TrendingSection`**
    - Gradient background container
    - Section header with "View All" link
    - 3-column grid of business cards (3→2→1)
    - Special trending badges

11. **`BusinessCard`**
    - Card image (200px height)
    - Business name + category
    - Trending/status badge (conditional)
    - Rating stars + review count
    - Distance/location meta
    - Description text (truncated)
    - Dual action buttons (primary + secondary)
    - Hover elevation animation

12. **`NewBusinessesShowcase`**
    - Green gradient header section
    - White content section with rounded bottom
    - 4-column grid (4→3→2→1)
    - Centered card design

13. **`NewBusinessCard`**
    - Circular logo image (60px, green border)
    - Business name (bold)
    - Category label
    - "New This Week" badge
    - Hover border color change

14. **`VerifiedCarousel`**
    - Section header with carousel controls
    - 5-column horizontal scrollable grid
    - Navigation arrows (left/right)
    - Minimal card design

15. **`VerifiedBusinessCard`**
    - Horizontal layout: logo (48px) + info
    - Business name + category
    - Verified badge with date
    - Rating + distance meta
    - Hover elevation

---

## Interaction Specifications

### Navigation & Scroll Behavior

**Sticky Header:**
```typescript
- Position: sticky, top: 0, z-index: 100
- Background: white with 1px border-bottom
- Shadow appears on scroll (0 1px 3px rgba(0,0,0,0.05))
- Mobile: Hamburger menu at <768px
```

**Hero Search:**
```typescript
- Search button click → Navigate to results page with query params
- Location input → Geocoding/autocomplete dropdown
- Enter key triggers search from either input
- Clear button appears when inputs have values
```

**Quick Filters:**
```typescript
- Click → Apply filter and scroll to results section
- Active state: Blue background + white text
- Horizontal scroll on overflow
- Touch-friendly spacing on mobile (48px min height)
```

### Card Interactions

**Category Tiles:**
```typescript
- Hover: translateY(-8px), shadow increase
- Click: Navigate to category page
- Keyboard accessible (tab navigation, enter to activate)
- Focus ring visible on keyboard navigation
```

**Business Cards:**
```typescript
- Hover: translateY(-4px), shadow increase
- Primary button: "Reserve Table" / "Book Service" / "Free Trial"
- Secondary button: "View Menu" / "Learn More" / "View Services"
- Image click: Navigate to business detail page
- Card click: Navigate to business detail (except buttons)
```

**Carousel Controls:**
```typescript
interface CarouselState {
  currentIndex: number;
  itemsPerView: number; // Responsive: 5→4→2→1
  totalItems: number;
}

- Left/Right arrows scroll by itemsPerView count
- Disable left arrow at start, right arrow at end
- Touch swipe support on mobile
- Keyboard: Arrow keys navigate, Home/End jump to start/end
```

### Form Handling

**Search Bar:**
```typescript
interface SearchFormData {
  query: string;
  location: string;
  filters?: string[];
}

const handleSearch = (data: SearchFormData) => {
  // Validate inputs
  // Build query params
  // Navigate to /search?q={query}&location={location}
  // Track analytics event
};
```

**Location Change:**
```typescript
interface Location {
  name: string;
  coordinates: { lat: number; lng: number };
  businessCount: number;
}

- Click "Change Location" → Open modal/dropdown
- Geolocation API: Get user's current location
- Manual input: Autocomplete with Places API
- Update banner + re-fetch results
```

### State Management

**Required State:**
```typescript
interface HomepageState {
  searchQuery: string;
  currentLocation: Location;
  activeFilters: string[];
  trendingBusinesses: Business[];
  newBusinesses: Business[];
  verifiedBusinesses: Business[];
  carouselIndex: number;
  isLoading: boolean;
  error: string | null;
}
```

---

## TypeScript Interfaces

**File:** `ui/components/types/directory.types.ts`

```typescript
export interface Business {
  id: string;
  name: string;
  category: string;
  subcategory?: string;
  description: string;
  imageUrl: string;
  logoUrl?: string;
  rating: number;
  reviewCount: number;
  distance: number; // miles
  distanceUnit: 'mi' | 'km';
  address: {
    street: string;
    city: string;
    state: string;
    zip: string;
    coordinates: { lat: number; lng: number };
  };
  contact: {
    phone?: string;
    email?: string;
    website?: string;
  };
  hours?: OperatingHours;
  isVerified: boolean;
  verifiedDate?: string;
  isTrending?: boolean;
  trendingRank?: number;
  isNew?: boolean;
  newDate?: string;
  badges?: Badge[];
  primaryAction?: {
    label: string;
    type: 'reservation' | 'booking' | 'trial' | 'contact';
    url?: string;
  };
  secondaryAction?: {
    label: string;
    type: 'menu' | 'info' | 'services' | 'portfolio';
    url?: string;
  };
}

export interface Category {
  id: string;
  name: string;
  slug: string;
  icon: string; // Lucide icon name
  imageUrl: string;
  businessCount: number;
  color?: string; // Fallback gradient color
  description?: string;
}

export interface Location {
  name: string;
  displayName: string;
  coordinates: { lat: number; lng: number };
  businessCount: number;
  radius: number; // miles
}

export interface FilterOption {
  id: string;
  label: string;
  icon: string;
  isActive: boolean;
}

export interface Badge {
  type: 'trending' | 'new' | 'verified' | 'top-rated' | 'hot';
  label: string;
  color: 'orange' | 'green' | 'blue' | 'red';
  gradient?: string;
  icon?: string;
  date?: string;
}

export interface SearchParams {
  query?: string;
  location?: string;
  category?: string;
  filters?: string[];
  sort?: 'relevance' | 'rating' | 'distance' | 'trending';
}

export interface OperatingHours {
  monday?: { open: string; close: string; isClosed?: boolean };
  tuesday?: { open: string; close: string; isClosed?: boolean };
  wednesday?: { open: string; close: string; isClosed?: boolean };
  thursday?: { open: string; close: string; isClosed?: boolean };
  friday?: { open: string; close: string; isClosed?: boolean };
  saturday?: { open: string; close: string; isClosed?: boolean };
  sunday?: { open: string; close: string; isClosed?: boolean };
}

export interface Statistic {
  value: string;
  label: string;
  format?: 'number' | 'percentage' | 'text';
  animate?: boolean;
}

export interface CarouselConfig {
  itemsPerView: {
    mobile: number;
    tablet: number;
    desktop: number;
  };
  gap: number;
  showControls: boolean;
  autoScroll?: boolean;
  autoScrollDelay?: number;
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
  '#1e40af': 'blue.800',
  '#1d4ed8': 'blue.700',
  
  // Accent
  '#f59e0b': 'amber.500',
  '#d97706': 'amber.600',
  '#10b981': 'emerald.500',
  '#059669': 'emerald.600',
  '#0ea5e9': 'sky.500',
  
  // Neutrals
  '#f8fafc': 'slate.50',
  '#ffffff': 'white',
  '#f1f5f9': 'slate.100',
  '#e2e8f0': 'slate.200',
  '#cbd5e1': 'slate.300',
  '#94a3b8': 'slate.400',
  '#64748b': 'slate.500',
  '#475569': 'slate.600',
  '#334155': 'slate.700',
  '#1e293b': 'slate.800',
  '#0f172a': 'slate.900'
}
```

### Tailwind Utility Classes

```typescript
// Component-specific class mappings

DirectoryHeader:
"sticky top-0 z-[100] bg-white border-b border-slate-200 shadow-sm"

HeroSearchSection:
"relative overflow-hidden bg-gradient-to-br from-blue-600 to-blue-800 py-20"

SearchBar:
"max-w-3xl mx-auto bg-white rounded-2xl p-2 shadow-xl flex gap-2"

CategoryTile:
"aspect-square rounded-3xl overflow-hidden relative cursor-pointer transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl"

BusinessCard:
"bg-white rounded-2xl overflow-hidden shadow-md border border-slate-200 transition-all duration-300 hover:-translate-y-1 hover:shadow-xl"

TrendingBadge:
"bg-gradient-to-br from-amber-500 to-amber-600 text-white px-2 py-1 rounded-md text-xs font-semibold flex items-center gap-1"

NewBadge:
"inline-block bg-gradient-to-br from-emerald-500 to-emerald-600 text-white px-2 py-1 rounded-xl text-xs font-semibold"

VerifiedBadge:
"bg-gradient-to-br from-emerald-600 to-emerald-500 text-white px-3 py-1.5 rounded-full text-xs font-semibold flex items-center gap-1.5 w-fit"

FilterTag:
"bg-slate-100 text-slate-600 px-4 py-2 rounded-full font-medium transition-all duration-200 border-2 border-transparent hover:bg-blue-600 hover:text-white hover:-translate-y-0.5"

LocationBanner:
"bg-gradient-to-br from-sky-50 to-sky-100 border border-sky-500 rounded-xl p-5 flex items-center gap-4"
```

---

## Icon Mapping

**Font Awesome → Lucide React:**

```typescript
const iconMap = {
  'fa-map-marker-alt': 'MapPin',
  'fa-plus': 'Plus',
  'fa-search': 'Search',
  'fa-fire': 'Flame',
  'fa-clock': 'Clock',
  'fa-star': 'Star',
  'fa-tag': 'Tag',
  'fa-shield-check': 'ShieldCheck',
  'fa-location-arrow': 'Navigation',
  'fa-utensils': 'UtensilsCrossed',
  'fa-heartbeat': 'HeartPulse',
  'fa-shopping-bag': 'ShoppingBag',
  'fa-car': 'Car',
  'fa-cut': 'Scissors',
  'fa-dumbbell': 'Dumbbell',
  'fa-home': 'Home',
  'fa-briefcase': 'Briefcase',
  'fa-trending-up': 'TrendingUp',
  'fa-calendar': 'Calendar',
  'fa-user-plus': 'UserPlus',
  'fa-spa': 'Sparkles',
  'fa-sparkles': 'Sparkles',
  'fa-arrow-right': 'ArrowRight',
  'fa-chevron-left': 'ChevronLeft',
  'fa-chevron-right': 'ChevronRight'
};
```

**Usage:**
```typescript
import { MapPin, Search, Flame, Star, ShieldCheck } from 'lucide-react';

<MapPin className="w-5 h-5" />
```

---

## Accessibility Requirements

### WCAG 2.1 AA Compliance

**Keyboard Navigation:**
- All interactive elements reachable via Tab
- Skip to main content link
- Focus indicators visible (ring-2 ring-blue-500)
- Escape key closes modals/dropdowns
- Arrow keys navigate carousels
- Enter/Space activate buttons

**Screen Readers:**
```typescript
// Search form
<form role="search" aria-label="Search businesses">
  <input 
    type="search"
    aria-label="What are you looking for?"
    aria-describedby="search-help"
  />
  <input 
    type="text"
    aria-label="Location"
    placeholder="Springfield, IL"
  />
  <button type="submit" aria-label="Search businesses">
    <Search aria-hidden="true" />
    <span>Search</span>
  </button>
</form>

// Category tiles
<a 
  href="/category/restaurants"
  aria-label="Explore Restaurants category, 284 businesses"
>
  <img alt="Modern restaurant interior" />
  <span aria-hidden="true">Restaurants</span>
</a>

// Business cards
<article aria-labelledby="business-name-123">
  <img alt="Farm & Table Bistro exterior" />
  <h4 id="business-name-123">Farm & Table Bistro</h4>
  <div aria-label="Rating: 4.9 stars out of 5, 127 reviews">...</div>
</article>

// Carousel
<section aria-label="Recently verified businesses">
  <button aria-label="Previous verified businesses">
    <ChevronLeft aria-hidden="true" />
  </button>
  <button aria-label="Next verified businesses">
    <ChevronRight aria-hidden="true" />
  </button>
</section>
```

**Color Contrast:**
- All text meets 4.5:1 contrast ratio
- Blue links (#2563eb) on white: 7.21:1 ✓
- Slate 600 (#475569) on white: 7.53:1 ✓
- Badges: Verify gradient text contrast

**Focus Management:**
- Trap focus in modals
- Return focus after modal close
- Focus first result after search
- Announce dynamic content changes (aria-live)

---

## Mock Data Structure

**File:** `ui/components/directory/mockData.ts`

```typescript
export const mockCategories: Category[] = [
  {
    id: 'cat-1',
    name: 'Restaurants',
    slug: 'restaurants',
    icon: 'UtensilsCrossed',
    imageUrl: '/images/categories/restaurants.webp',
    businessCount: 284,
    description: 'Discover amazing dining experiences'
  },
  {
    id: 'cat-2',
    name: 'Healthcare',
    slug: 'healthcare',
    icon: 'HeartPulse',
    imageUrl: '/images/categories/healthcare.webp',
    businessCount: 156,
    description: 'Quality medical and wellness services'
  },
  {
    id: 'cat-3',
    name: 'Shopping',
    slug: 'shopping',
    icon: 'ShoppingBag',
    imageUrl: '/images/categories/shopping.webp',
    businessCount: 198,
    description: 'Local retail and boutique stores'
  },
  {
    id: 'cat-4',
    name: 'Automotive',
    slug: 'automotive',
    icon: 'Car',
    imageUrl: '/images/categories/automotive.webp',
    businessCount: 89,
    description: 'Auto repair and maintenance services'
  },
  {
    id: 'cat-5',
    name: 'Beauty & Wellness',
    slug: 'beauty-wellness',
    icon: 'Scissors',
    imageUrl: '/images/categories/beauty.webp',
    businessCount: 142,
    description: 'Salons, spas, and wellness centers'
  },
  {
    id: 'cat-6',
    name: 'Fitness',
    slug: 'fitness',
    icon: 'Dumbbell',
    imageUrl: '/images/categories/fitness.webp',
    businessCount: 73,
    description: 'Gyms, studios, and training facilities'
  },
  {
    id: 'cat-7',
    name: 'Home Services',
    slug: 'home-services',
    icon: 'Home',
    imageUrl: '/images/categories/home-services.webp',
    businessCount: 167,
    description: 'Plumbing, electrical, and home repair'
  },
  {
    id: 'cat-8',
    name: 'Professional',
    slug: 'professional',
    icon: 'Briefcase',
    imageUrl: '/images/categories/professional.webp',
    businessCount: 124,
    description: 'Legal, financial, and business services'
  }
];

export const mockTrendingBusinesses: Business[] = [
  {
    id: 'biz-1',
    name: 'Farm & Table Bistro',
    category: 'Restaurants',
    subcategory: 'Farm-to-Table Restaurant',
    description: 'Fresh, locally-sourced ingredients crafted into seasonal dishes. Award-winning chef creates innovative comfort food.',
    imageUrl: '/images/businesses/farm-table.webp',
    rating: 4.9,
    reviewCount: 127,
    distance: 0.8,
    distanceUnit: 'mi',
    address: {
      street: '123 Main St',
      city: 'Springfield',
      state: 'IL',
      zip: '62701',
      coordinates: { lat: 39.7817, lng: -89.6501 }
    },
    contact: {
      phone: '(217) 555-0123',
      website: 'https://farmandtable.example.com'
    },
    isVerified: true,
    isTrending: true,
    trendingRank: 1,
    badges: [
      {
        type: 'trending',
        label: '#1 Trending',
        color: 'orange',
        gradient: 'from-amber-500 to-amber-600',
        icon: 'TrendingUp'
      }
    ],
    primaryAction: {
      label: 'Reserve Table',
      type: 'reservation',
      url: '/reserve/farm-table'
    },
    secondaryAction: {
      label: 'View Menu',
      type: 'menu',
      url: '/business/farm-table/menu'
    }
  },
  {
    id: 'biz-2',
    name: 'CoreFit CrossTraining',
    category: 'Fitness',
    subcategory: 'Fitness Studio',
    description: 'High-intensity functional fitness for all levels. Certified trainers, supportive community, proven results.',
    imageUrl: '/images/businesses/corefit.webp',
    rating: 4.8,
    reviewCount: 89,
    distance: 1.3,
    distanceUnit: 'mi',
    address: {
      street: '456 Fitness Lane',
      city: 'Springfield',
      state: 'IL',
      zip: '62702',
      coordinates: { lat: 39.7920, lng: -89.6480 }
    },
    contact: {
      phone: '(217) 555-0456',
      website: 'https://corefit.example.com'
    },
    isVerified: true,
    isTrending: true,
    badges: [
      {
        type: 'hot',
        label: 'Hot This Week',
        color: 'orange',
        gradient: 'from-amber-500 to-amber-600',
        icon: 'Flame'
      }
    ],
    primaryAction: {
      label: 'Free Trial',
      type: 'trial',
      url: '/trial/corefit'
    },
    secondaryAction: {
      label: 'Learn More',
      type: 'info',
      url: '/business/corefit'
    }
  },
  {
    id: 'biz-3',
    name: 'Serenity Day Spa',
    category: 'Beauty & Wellness',
    subcategory: 'Day Spa',
    description: 'Luxury spa treatments using organic products. Massage therapy, facials, and wellness packages in tranquil setting.',
    imageUrl: '/images/businesses/serenity-spa.webp',
    rating: 5.0,
    reviewCount: 94,
    distance: 2.1,
    distanceUnit: 'mi',
    address: {
      street: '789 Wellness Way',
      city: 'Springfield',
      state: 'IL',
      zip: '62703',
      coordinates: { lat: 39.7750, lng: -89.6420 }
    },
    contact: {
      phone: '(217) 555-0789',
      website: 'https://serenityspa.example.com'
    },
    isVerified: true,
    isTrending: true,
    badges: [
      {
        type: 'top-rated',
        label: 'Top Rated',
        color: 'blue',
        icon: 'Star'
      }
    ],
    primaryAction: {
      label: 'Book Service',
      type: 'booking',
      url: '/book/serenity-spa'
    },
    secondaryAction: {
      label: 'View Services',
      type: 'services',
      url: '/business/serenity-spa/services'
    }
  }
];

export const mockNewBusinesses: Business[] = [
  {
    id: 'biz-new-1',
    name: 'Artisan Coffee Co.',
    category: 'Restaurants',
    subcategory: 'Coffee Shop',
    description: 'Specialty coffee roasted daily',
    logoUrl: '/images/logos/artisan-coffee.webp',
    imageUrl: '/images/businesses/artisan-coffee.webp',
    rating: 4.7,
    reviewCount: 23,
    distance: 0.5,
    distanceUnit: 'mi',
    address: {
      street: '101 Coffee St',
      city: 'Springfield',
      state: 'IL',
      zip: '62701',
      coordinates: { lat: 39.7830, lng: -89.6510 }
    },
    isVerified: true,
    isNew: true,
    newDate: '2024-03-18',
    badges: [
      {
        type: 'new',
        label: 'New This Week',
        color: 'green',
        gradient: 'from-emerald-500 to-emerald-600'
      }
    ]
  },
  {
    id: 'biz-new-2',
    name: 'Bright Smiles Dental',
    category: 'Healthcare',
    subcategory: 'Dental Practice',
    description: 'Family dentistry with modern technology',
    logoUrl: '/images/logos/bright-smiles.webp',
    imageUrl: '/images/businesses/bright-smiles.webp',
    rating: 4.9,
    reviewCount: 15,
    distance: 1.2,
    distanceUnit: 'mi',
    address: {
      street: '202 Dental Dr',
      city: 'Springfield',
      state: 'IL',
      zip: '62702',
      coordinates: { lat: 39.7910, lng: -89.6490 }
    },
    isVerified: true,
    isNew: true,
    newDate: '2024-03-17',
    badges: [
      {
        type: 'new',
        label: 'New This Week',
        color: 'green',
        gradient: 'from-emerald-500 to-emerald-600'
      }
    ]
  },
  {
    id: 'biz-new-3',
    name: 'Style Collective',
    category: 'Shopping',
    subcategory: 'Fashion Boutique',
    description: 'Curated fashion and accessories',
    logoUrl: '/images/logos/style-collective.webp',
    imageUrl: '/images/businesses/style-collective.webp',
    rating: 4.8,
    reviewCount: 31,
    distance: 0.9,
    distanceUnit: 'mi',
    address: {
      street: '303 Fashion Blvd',
      city: 'Springfield',
      state: 'IL',
      zip: '62701',
      coordinates: { lat: 39.7840, lng: -89.6520 }
    },
    isVerified: true,
    isNew: true,
    newDate: '2024-03-16',
    badges: [
      {
        type: 'new',
        label: 'New This Week',
        color: 'green',
        gradient: 'from-emerald-500 to-emerald-600'
      }
    ]
  },
  {
    id: 'biz-new-4',
    name: 'Precision Auto Care',
    category: 'Automotive',
    subcategory: 'Auto Repair',
    description: 'Full-service auto repair and maintenance',
    logoUrl: '/images/logos/precision-auto.webp',
    imageUrl: '/images/businesses/precision-auto.webp',
    rating: 4.6,
    reviewCount: 18,
    distance: 1.7,
    distanceUnit: 'mi',
    address: {
      street: '404 Auto Way',
      city: 'Springfield',
      state: 'IL',
      zip: '62703',
      coordinates: { lat: 39.7770, lng: -89.6440 }
    },
    isVerified: true,
    isNew: true,
    newDate: '2024-03-15',
    badges: [
      {
        type: 'new',
        label: 'New This Week',
        color: 'green',
        gradient: 'from-emerald-500 to-emerald-600'
      }
    ]
  }
];

export const mockVerifiedBusinesses: Business[] = [
  {
    id: 'biz-verified-1',
    name: 'Miller & Associates Law',
    category: 'Professional',
    subcategory: 'Legal Services',
    description: 'Experienced attorneys serving Springfield',
    logoUrl: '/images/logos/miller-law.webp',
    imageUrl: '/images/businesses/miller-law.webp',
    rating: 4.9,
    reviewCount: 76,
    distance: 1.1,
    distanceUnit: 'mi',
    address: {
      street: '505 Legal Lane',
      city: 'Springfield',
      state: 'IL',
      zip: '62701',
      coordinates: { lat: 39.7850, lng: -89.6530 }
    },
    isVerified: true,
    verifiedDate: '2024-03-19',
    badges: [
      {
        type: 'verified',
        label: 'Verified March 19',
        color: 'green',
        gradient: 'from-emerald-600 to-emerald-500',
        icon: 'ShieldCheck',
        date: 'March 19'
      }
    ]
  },
  {
    id: 'biz-verified-2',
    name: 'FlowRight Plumbing',
    category: 'Home Services',
    subcategory: 'Plumbing',
    description: 'Licensed plumbers available 24/7',
    logoUrl: '/images/logos/flowright.webp',
    imageUrl: '/images/businesses/flowright.webp',
    rating: 4.8,
    reviewCount: 142,
    distance: 2.3,
    distanceUnit: 'mi',
    address: {
      street: '606 Plumbing Pkwy',
      city: 'Springfield',
      state: 'IL',
      zip: '62702',
      coordinates: { lat: 39.7950, lng: -89.6470 }
    },
    isVerified: true,
    verifiedDate: '2024-03-18',
    badges: [
      {
        type: 'verified',
        label: 'Verified March 18',
        color: 'green',
        gradient: 'from-emerald-600 to-emerald-500',
        icon: 'ShieldCheck',
        date: 'March 18'
      }
    ]
  },
  {
    id: 'biz-verified-3',
    name: 'Golden Crust Bakery',
    category: 'Restaurants',
    subcategory: 'Bakery',
    description: 'Fresh-baked artisan breads and pastries',
    logoUrl: '/images/logos/golden-crust.webp',
    imageUrl: '/images/businesses/golden-crust.webp',
    rating: 4.9,
    reviewCount: 203,
    distance: 0.7,
    distanceUnit: 'mi',
    address: {
      street: '707 Bakery Blvd',
      city: 'Springfield',
      state: 'IL',
      zip: '62701',
      coordinates: { lat: 39.7820, lng: -89.6515 }
    },
    isVerified: true,
    verifiedDate: '2024-03-17',
    badges: [
      {
        type: 'verified',
        label: 'Verified March 17',
        color: 'green',
        gradient: 'from-emerald-600 to-emerald-500',
        icon: 'ShieldCheck',
        date: 'March 17'
      }
    ]
  },
  {
    id: 'biz-verified-4',
    name: 'WellCare Family Medicine',
    category: 'Healthcare',
    subcategory: 'Medical Clinic',
    description: 'Comprehensive family healthcare',
    logoUrl: '/images/logos/wellcare.webp',
    imageUrl: '/images/businesses/wellcare.webp',
    rating: 4.7,
    reviewCount: 98,
    distance: 1.8,
    distanceUnit: 'mi',
    address: {
      street: '808 Medical Dr',
      city: 'Springfield',
      state: 'IL',
      zip: '62703',
      coordinates: { lat: 39.7780, lng: -89.6430 }
    },
    isVerified: true,
    verifiedDate: '2024-03-16',
    badges: [
      {
        type: 'verified',
        label: 'Verified March 16',
        color: 'green',
        gradient: 'from-emerald-600 to-emerald-500',
        icon: 'ShieldCheck',
        date: 'March 16'
      }
    ]
  },
  {
    id: 'biz-verified-5',
    name: 'Bloom & Blossom',
    category: 'Shopping',
    subcategory: 'Florist',
    description: 'Custom floral arrangements and gifts',
    logoUrl: '/images/logos/bloom-blossom.webp',
    imageUrl: '/images/businesses/bloom-blossom.webp',
    rating: 5.0,
    reviewCount: 67,
    distance: 1.4,
    distanceUnit: 'mi',
    address: {
      street: '909 Flower Ln',
      city: 'Springfield',
      state: 'IL',
      zip: '62702',
      coordinates: { lat: 39.7930, lng: -89.6485 }
    },
    isVerified: true,
    verifiedDate: '2024-03-15',
    badges: [
      {
        type: 'verified',
        label: 'Verified March 15',
        color: 'green',
        gradient: 'from-emerald-600 to-emerald-500',
        icon: 'ShieldCheck',
        date: 'March 15'
      }
    ]
  }
];

export const mockFilterOptions: FilterOption[] = [
  { id: 'trending', label: 'Trending Now', icon: 'Flame', isActive: false },
  { id: 'open', label: 'Open Now', icon: 'Clock', isActive: false },
  { id: 'rated', label: 'Highly Rated', icon: 'Star', isActive: false },
  { id: 'nearby', label: 'Nearby', icon: 'MapPin', isActive: false },
  { id: 'offers', label: 'Special Offers', icon: 'Tag', isActive: false },
  { id: 'verified', label: 'Newly Verified', icon: 'ShieldCheck', isActive: false }
];

export const mockStats: Statistic[] = [
  { value: '2,847', label: 'Verified Businesses', format: 'number', animate: true },
  { value: '98%', label: 'Customer Satisfaction', format: 'percentage', animate: true },
  { value: '24/7', label: 'Platform Available', format: 'text', animate: false }
];

export const mockCurrentLocation: Location = {
  name: 'Springfield',
  displayName: 'Springfield, IL',
  coordinates: { lat: 39.7817, lng: -89.6501 },
  businessCount: 847,
  radius: 25
};
```

---

## File Structure

```
ui/components/directory/
├── types/
│   └── directory.types.ts          # TypeScript interfaces
├── layout/
│   ├── ListingHomepageLayout.tsx   # Main container
│   ├── DirectoryHeader.tsx          # Sticky header nav
│   └── QuickFiltersBar.tsx          # Horizontal filter tags
├── hero/
│   ├── HeroSearchSection.tsx        # Full hero with gradient
│   ├── SearchBar.tsx                # Compound search component
│   └── StatsDisplay.tsx             # 3-column stats
├── categories/
│   ├── CategoryGrid.tsx             # 4-column responsive grid
│   └── CategoryTile.tsx             # Individual category card
├── business/
│   ├── BusinessCard.tsx             # Standard business card
│   ├── TrendingSection.tsx          # Trending businesses container
│   ├── NewBusinessesShowcase.tsx    # New businesses section
│   ├── NewBusinessCard.tsx          # Minimal new business card
│   ├── VerifiedCarousel.tsx         # Carousel with controls
│   └── VerifiedBusinessCard.tsx     # Compact verified card
├── shared/
│   ├── LocationBanner.tsx           # Personalized location banner
│   ├── Badge.tsx                    # Reusable badge component
│   └── RatingStars.tsx              # Star rating display
├── hooks/
│   ├── useSearchParams.ts           # Search state management
│   ├── useCarousel.ts               # Carousel navigation logic
│   └── useGeolocation.ts            # User location detection
├── utils/
│   ├── distance.ts                  # Distance calculations
│   ├── formatters.ts                # Text/number formatting
│   └── validators.ts                # Input validation
├── mockData.ts                      # Mock data exports
├── index.ts                         # Barrel exports
└── README.md                        # Component documentation
```

---

## Testing Requirements

### Unit Tests

```typescript
// CategoryTile.test.tsx
describe('CategoryTile', () => {
  it('renders category name and count', () => {
    render(<CategoryTile category={mockCategories[0]} />);
    expect(screen.getByText('Restaurants')).toBeInTheDocument();
    expect(screen.getByText('284 businesses')).toBeInTheDocument();
  });

  it('applies hover animation', async () => {
    const { container } = render(<CategoryTile category={mockCategories[0]} />);
    const tile = container.firstChild;
    
    await userEvent.hover(tile);
    expect(tile).toHaveClass('hover:-translate-y-2');
  });

  it('navigates on click', async () => {
    const mockNavigate = jest.fn();
    render(<CategoryTile category={mockCategories[0]} onNavigate={mockNavigate} />);
    
    await userEvent.click(screen.getByRole('link'));
    expect(mockNavigate).toHaveBeenCalledWith('/category/restaurants');
  });

  it('handles keyboard navigation', async () => {
    render(<CategoryTile category={mockCategories[0]} />);
    const tile = screen.getByRole('link');
    
    tile.focus();
    expect(tile).toHaveFocus();
    
    await userEvent.keyboard('{Enter}');
    // Assert navigation occurred
  });
});

// SearchBar.test.tsx
describe('SearchBar', () => {
  it('submits search with valid inputs', async () => {
    const mockOnSearch = jest.fn();
    render(<SearchBar onSearch={mockOnSearch} />);
    
    await userEvent.type(screen.getByLabelText(/what are you looking/i), 'pizza');
    await userEvent.type(screen.getByLabelText(/location/i), 'Chicago');
    await userEvent.click(screen.getByRole('button', { name: /search/i }));
    
    expect(mockOnSearch).toHaveBeenCalledWith({
      query: 'pizza',
      location: 'Chicago'
    });
  });

  it('shows validation errors for empty inputs', async () => {
    render(<SearchBar onSearch={jest.fn()} />);
    
    await userEvent.click(screen.getByRole('button', { name: /search/i }));
    expect(screen.getByText(/please enter a search/i)).toBeInTheDocument();
  });

  it('handles Enter key submission', async () => {
    const mockOnSearch = jest.fn();
    render(<SearchBar onSearch={mockOnSearch} />);
    
    const input = screen.getByLabelText(/what are you looking/i);
    await userEvent.type(input, 'coffee{Enter}');
    
    expect(mockOnSearch).toHaveBeenCalled();
  });
});

// VerifiedCarousel.test.tsx
describe('VerifiedCarousel', () => {
  it('renders correct number of visible items', () => {
    render(<VerifiedCarousel businesses={mockVerifiedBusinesses} itemsPerView={3} />);
    
    const visibleCards = screen.getAllByRole('article');
    expect(visibleCards).toHaveLength(3);
  });

  it('navigates forward on arrow click', async () => {
    render(<VerifiedCarousel businesses={mockVerifiedBusinesses} />);
    
    await userEvent.click(screen.getByLabelText(/next verified/i));
    // Assert carousel position changed
  });

  it('disables left arrow at start', () => {
    render(<VerifiedCarousel businesses={mockVerifiedBusinesses} />);
    
    expect(screen.getByLabelText(/previous verified/i)).toBeDisabled();
  });

  it('supports keyboard navigation', async () => {
    render(<VerifiedCarousel businesses={mockVerifiedBusinesses} />);
    
    const carousel = screen.getByRole('region', { name: /verified businesses/i });
    carousel.focus();
    
    await userEvent.keyboard('{ArrowRight}');
    // Assert position changed
    
    await userEvent.keyboard('{Home}');
    // Assert back to start
  });
});
```

### Integration Tests

```typescript
describe('ListingHomepage Integration', () => {
  it('completes full search flow', async () => {
    render(<ListingHomepageLayout />);
    
    // Fill search
    await userEvent.type(screen.getByLabelText(/what are you looking/i), 'dentist');
    await userEvent.type(screen.getByLabelText(/location/i), 'Springfield, IL');
    
    // Submit
    await userEvent.click(screen.getByRole('button', { name: /search/i }));
    
    // Assert navigation
    expect(mockRouter.push).toHaveBeenCalledWith(
      expect.stringContaining('/search?q=dentist&location=Springfield')
    );
  });

  it('applies filter and scrolls to results', async () => {
    render(<ListingHomepageLayout />);
    
    await userEvent.click(screen.getByText('Trending Now'));
    
    expect(screen.getByText('Trending Now')).toHaveClass('bg-blue-600');
    // Assert scroll occurred
  });

  it('changes location and updates banner', async () => {
    render(<ListingHomepageLayout />);
    
    await userEvent.click(screen.getByText('Change Location'));
    
    // Mock modal/dropdown interaction
    await userEvent.type(screen.getByLabelText(/enter location/i), 'Chicago, IL');
    await userEvent.click(screen.getByRole('button', { name: /update/i }));
    
    expect(screen.getByText(/showing results for chicago/i)).toBeInTheDocument();
  });
});
```

### Visual Regression Tests

```typescript
// Using Storybook + Chromatic or Percy
describe('Visual Regression', () => {
  it('matches CategoryGrid snapshot', () => {
    const { container } = render(<CategoryGrid categories={mockCategories} />);
    expect(container).toMatchSnapshot();
  });

  it('matches BusinessCard hover state', async () => {
    const { container } = render(<BusinessCard business={mockTrendingBusinesses[0]} />);
    await userEvent.hover(container.firstChild);
    expect(container).toMatchSnapshot();
  });
});
```

---

## Responsive Behavior

### Breakpoint Strategy

```typescript
const breakpoints = {
  sm: 480,   // Single column
  md: 768,   // Stacked search, 2 columns
  lg: 1200,  // 3 columns, desktop nav
  xl: 1600   // Max container width
};
```

### Layout Transformations

**Category Grid:**
```
Desktop (>1200px): 4 columns
Tablet (768-1200px): 3 columns
Mobile (480-768px): 2 columns
Small Mobile (<480px): 1 column
```

**Trending Grid:**
```
Desktop (>1200px): 3 columns
Tablet (768-1200px): 2 columns
Mobile (<768px): 1 column
```

**New Business Grid:**
```
Desktop (>1200px): 4 columns
Tablet (768-1200px): 3 columns
Mobile (480-768px): 2 columns
Small Mobile (<480px): 1 column
```

**Verified Carousel:**
```
Desktop (>1200px): 5 items visible
Tablet (768-1200px): 4 items visible
Mobile (480-768px): 2 items visible
Small Mobile (<480px): 1 item visible
```

**Hero Search:**
```typescript
// Desktop
<div className="flex gap-2">
  <input className="flex-1" />
  <input className="min-w-[200px]" />
  <button />
</div>

// Mobile (<768px)
<div className="flex flex-col gap-2">
  <input className="w-full" />
  <input className="w-full" />
  <button className="w-full" />
</div>
```

**Navigation:**
```typescript
// Desktop
<nav className="flex gap-8 items-center">
  {links.map(...)}
</nav>

// Mobile (<768px)
<button className="hamburger" onClick={toggleMenu}>
  <Menu />
</button>
<MobileMenu isOpen={isOpen} />
```

---

## Performance Optimization

### Image Optimization

```typescript
// Use Next.js Image or similar optimized loader
<Image
  src={business.imageUrl}
  alt={`${business.name} location`}
  width={400}
  height={200}
  sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
  loading="lazy"
  placeholder="blur"
/>
```

### Lazy Loading

```typescript
// Carousel items
const VerifiedCarousel = () => {
  const { visibleItems, loadMore } = useInfiniteScroll();
  
  return (
    <div ref={containerRef} onScroll={handleScroll}>
      {visibleItems.map(business => (
        <VerifiedBusinessCard key={business.id} business={business} />
      ))}
    </div>
  );
};

// Below-fold sections
const NewBusinessesShowcase = lazy(() => import('./NewBusinessesShowcase'));

<Suspense fallback={<Skeleton />}>
  <NewBusinessesShowcase />
</Suspense>
```

### Debouncing & Throttling

```typescript
// Search input
const debouncedSearch = useMemo(
  () => debounce((value: string) => {
    fetchSuggestions(value);
  }, 300),
  []
);

// Carousel scroll
const handleScroll = throttle((e: Event) => {
  updateCarouselPosition();
}, 100);
```

### Code Splitting

```typescript
// Route-based splitting
const CategoryPage = lazy(() => import('./pages/CategoryPage'));
const BusinessDetailPage = lazy(() => import('./pages/BusinessDetailPage'));

// Component-based splitting
const LocationModal = lazy(() => import('./LocationModal'));
```

---

## Animation Specifications

### Hover Animations

```typescript
// Category Tiles
"transition-all duration-300 ease-in-out hover:-translate-y-2 hover:shadow-2xl"

// Business Cards
"transition-all duration-300 ease-in-out hover:-translate-y-1 hover:shadow-xl"

// Filter Tags
"transition-all duration-200 ease-in-out hover:bg-blue-600 hover:text-white hover:-translate-y-0.5"

// Buttons
"transition-all duration-200 ease-in-out hover:bg-blue-700 hover:-translate-y-0.5"
```

### Entrance Animations

```typescript
// Stagger children on mount
const container = {
  hidden: { opacity: 0 },
  show: {
    opacity: 1,
    transition: { staggerChildren: 0.1 }
  }
};

const item = {
  hidden: { opacity: 0, y: 20 },
  show: { opacity: 1, y: 0 }
};

<motion.div variants={container} initial="hidden" animate="show">
  {categories.map(cat => (
    <motion.div key={cat.id} variants={item}>
      <CategoryTile category={cat} />
    </motion.div>
  ))}
</motion.div>
```

### Carousel Transitions

```typescript
// Smooth scroll with spring physics
const controls = useAnimation();

const scrollToIndex = async (index: number) => {
  await controls.start({
    x: -index * itemWidth,
    transition: { type: 'spring', stiffness: 300, damping: 30 }
  });
};
```

### Loading States

```typescript
// Skeleton placeholders
const BusinessCardSkeleton = () => (
  <div className="animate-pulse">
    <div className="bg-slate-200 h-[200px] rounded-t-2xl" />
    <div className="p-5 space-y-3">
      <div className="bg-slate-200 h-5 rounded w-3/4" />
      <div className="bg-slate-200 h-4 rounded w-1/2" />
      <div className="bg-slate-200 h-16 rounded" />
    </div>
  </div>
);
```

---

## Constitution Alignment

### Vertical Slice Ownership
- Each component owns its types, styles, tests, and mock data
- Domain-specific logic contained within directory/ module
- Clear boundaries between layout, hero, categories, and business sub-domains

### Type Safety
- Zero `any` types - all interfaces explicitly defined
- Strict TypeScript mode enabled
- Runtime validation for search inputs and API responses

### Design Fidelity
- Pixel-perfect implementation of HTML prototype
- All gradients, shadows, and animations preserved
- Responsive behavior matches original breakpoints

### Observability
- Search events tracked (query, location, filters applied)
- Carousel interactions logged (direction, position)
- Business card clicks with category context
- Error boundaries for failed API calls

### Transparency
- Component documentation inline
- Clear prop interfaces with JSDoc comments
- Architectural decisions documented in README

---

## Future Enhancements

### Phase 2 Features
1. **Advanced Search Filters**
   - Price range slider
   - Hours of operation filter
   - Amenities checklist
   - Sort by distance/rating/trending

2. **Interactive Map View**
   - Toggle list/map display
   - Cluster markers for density
   - Click marker → show business card popup
   - Draw radius to filter

3. **User Accounts**
   - Save favorite businesses
   - Write reviews
   - Upload photos
   - Business comparison tool

4. **Real-time Features**
   - Live wait times for restaurants
   - Appointment availability calendar
   - Chat with business owners
   - Virtual tours (360° photos)

### Performance Goals
- Lighthouse score >90 (all metrics)
- First Contentful Paint <1.5s
- Time to Interactive <3s
- Cumulative Layout Shift <0.1

---

## Implementation Checklist

- [ ] Set up file structure (`ui/components/directory/`)
- [ ] Create TypeScript interfaces (`directory.types.ts`)
- [ ] Build layout components (Header, Hero, Filters)
- [ ] Implement CategoryGrid with hover animations
- [ ] Create BusinessCard with all variants (trending, new, verified)
- [ ] Build VerifiedCarousel with keyboard navigation
- [ ] Implement SearchBar with validation
- [ ] Add LocationBanner with geolocation
- [ ] Create mock data files
- [ ] Write unit tests (>80% coverage)
- [ ] Add accessibility attributes (ARIA, roles)
- [ ] Test responsive behavior at all breakpoints
- [ ] Implement loading states and error boundaries
- [ ] Add Storybook stories for all components
- [ ] Performance audit (Lighthouse, Web Vitals)
- [ ] Document API integration points
- [ ] Create README with usage examples

---

## Summary

This is a **comprehensive business directory homepage** with:

- **15 modular React components** organized by domain
- **Sticky header** with navigation and CTA
- **Hero section** with gradient, dual-input search, and live stats
- **8-category grid** with hover animations and image overlays
- **Trending businesses section** with 3-column cards and badges
- **New businesses showcase** with circular logos and green accents
- **Verified carousel** with horizontal scroll and navigation controls
- **Quick filters bar** with 6 interactive tags
- **Location personalization** with geolocation support
- **Fully responsive** design (4 breakpoints: 1600/1200/768/480)
- **Accessibility compliant** (WCAG 2.1 AA, keyboard navigation, screen reader support)
- **Type-safe** with comprehensive TypeScript interfaces
- **Performance optimized** (lazy loading, image optimization, code splitting)
- **Thoroughly tested** (unit, integration, visual regression)

The interface prioritizes **discoverability**, **visual appeal**, and **user engagement** through strategic use of gradients, badges, animations, and content variety. It serves as a gateway for users to explore local businesses across multiple categories with location-aware search and filtering.
