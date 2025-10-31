# CommunityHub Map View - UI Integration Prompt

## Project Context

**Interface Type:** Interactive Map View with Business Directory  
**Source File:** `ideas/mapview1.html`  
**Target Framework:** React 19 + TypeScript + Tailwind CSS + Map Library (Mapbox/Google Maps)  
**Design System:** project-componets design tokens  
**Complexity Level:** Very High (Map integration, real-time markers, modals, filters, search suggestions)

---

## Visual Design Analysis

### Layout Structure

**Primary Layout:**
- Sticky header with blur backdrop (80px height)
- Full-screen map + sidebar layout (`calc(100vh - 80px)`)
- Three-column structure:
  - Floating search/filter bar (top overlay)
  - Map section (flexible, fills remaining space)
  - Business list panel (fixed 400px right sidebar)
- Sliding filter panel (320px, slides from left)
- Full-screen modal overlay (quick view)

**Key Sections:**
1. Header navigation (sticky, frosted glass effect)
2. Search & filter bar (absolute positioned, top overlay)
3. Map container with markers (8 business locations)
4. Filter panel (slide-in from left, 320px)
5. Business list sidebar (scrollable, 400px fixed width)
6. Quick view modal (centered overlay, max 680px)
7. Search suggestions dropdown

### Color Palette

**Primary Colors:**
```
Emerald/Green Primary: #059669 (logo, buttons, links, markers)
Emerald Light: #10b981 (gradients, hover states)
Emerald 50: #f0fdf4 (backgrounds, badges)
Emerald 100: #d1fae5 (borders, highlights)
Emerald 800: #065f46 (dark text on green backgrounds)
Emerald 900: #047857 (button hover states)

Secondary/Accent Colors:
Amber 500: #f59e0b (rating stars, cafe markers)
Blue 500: #3b82f6 (shop markers)
Purple 500: #8b5cf6 (service markers)
Red 500: #ef4444 (health/wellness markers)
Cyan 500: #06b6d4 (retail markers)

Neutral Palette:
White: #ffffff (cards, panels, backgrounds)
Gray 50: #f9fafb (panel backgrounds, card hover)
Gray 100: #f3f4f6 (borders, subtle dividers)
Gray 200: #e5e7eb (input borders, inactive states)
Gray 300: #d1d5db
Gray 400: #9ca3af
Gray 500: #6b7280 (secondary text, icons)
Gray 600: #4b5563 (nav links, body text)
Gray 700: #374151 (primary text)
Gray 800: #1f2937 (headings, dark text)
Gray 900: #111827 (darkest text, titles)

Background:
Page Background: #ffffff (white)
Map Background: linear-gradient(135deg, #e0f2fe 0%, #f0f9ff 100%) (sky gradient)
Panel Background: #fafafa (off-white for contrast)
```

**Gradients:**
```css
Primary Button: linear-gradient(135deg, #059669, #10b981)
Logo Icon: linear-gradient(135deg, #059669, #10b981)
Card Top Border: linear-gradient(90deg, #059669, #10b981)
Info Card Icon: linear-gradient(135deg, #059669, #10b981)
Map Background: linear-gradient(135deg, #e0f2fe 0%, #f0f9ff 100%)
```

**Marker Colors (Category-based):**
```
Restaurant: #059669 (emerald)
Cafe: #f59e0b (amber)
Shop: #3b82f6 (blue)
Service: #8b5cf6 (purple)
Health: #ef4444 (red)
Retail: #06b6d4 (cyan)
Food: #059669 (emerald)
Wellness: #ef4444 (red)
```

### Typography

**Font Family:** 'Inter', system-ui, -apple-system, sans-serif

**Type Scale:**
```
Logo: 24px, weight 700, color emerald-600
Nav Links: 15px, weight 500, color gray-600
H2 (Panel Title): 20px, weight 700, color gray-900
H3 (Business Name): 17px, weight 600, color gray-900
Business Category: 13px, weight 600, uppercase, letter-spacing 0.5px
Modal Business Name: 28px, weight 700, color gray-900
Modal Category: 16px, weight 600, uppercase, letter-spacing 0.5px
Filter Title: 18px, weight 700, color gray-900
Filter Section: 15px, weight 600, color gray-900
Button Text: 14px, weight 600
Badge Text: 12-13px, weight 600
Body Text: 14-15px, weight 400
```

### Spacing System

```
Header Padding: 20px 40px
Search Bar Inset: 20px from edges
Search Container Padding: 16px 20px
Filter Panel Width: 320px
Business Panel Width: 400px
Card Padding: 20px
Modal Body Padding: 32px
Info Card Padding: 20px

Gaps:
- Search Bar Gap: 12px
- Nav Center Gap: 32px
- Nav Actions Gap: 12px
- Filter Chips Gap: 8px
- Modal Info Grid Gap: 24px
- Business Card Gap: 16px
```

### Border Radius & Shadows

**Border Radius:**
```
Header Nav: none (straight edges)
Search Container: 16px
Filter Toggle Button: 16px
Business Cards: 16px
Filter Panel: 20px
Filter Chips: 12px
Buttons: 10px
Modal: 24px
Info Icons: 12px
Badges: 8px
Map Markers: 50% (circles)
Modal Close Button: 50% (circle)
```

**Box Shadows:**
```
Header: none (just border-bottom)
Search Container: 0 10px 25px -5px rgba(0, 0, 0, 0.08), 0 10px 10px -5px rgba(0, 0, 0, 0.04)
Search Focus: 0 10px 25px -5px rgba(16, 185, 129, 0.15), 0 0 0 4px rgba(16, 185, 129, 0.1)
Filter Panel: 0 25px 50px -12px rgba(0, 0, 0, 0.15)
Business Card Hover: 0 12px 25px rgba(0, 0, 0, 0.08)
Primary Button: 0 4px 12px 0 rgba(5, 150, 105, 0.25)
Primary Button Hover: 0 6px 20px 0 rgba(5, 150, 105, 0.35)
Map Marker: 0 6px 12px rgba(0, 0, 0, 0.15)
Modal: 0 25px 50px -12px rgba(0, 0, 0, 0.25)
```

### Special Effects

**Backdrop Blur:**
```css
Header: backdrop-filter: blur(12px), background: rgba(255, 255, 255, 0.98)
Modal Overlay: backdrop-filter: blur(4px), background: rgba(0, 0, 0, 0.6)
```

**Map Pattern:**
```css
.map-bg-pattern {
  opacity: 0.1;
  background-image: 
    linear-gradient(90deg, #10b981 1px, transparent 1px),
    linear-gradient(180deg, #10b981 1px, transparent 1px);
  background-size: 50px 50px;
}
```

---

## Component Hierarchy

### Primary Components (22 total)

1. **`MapViewLayout`** (Container)
   - Full-screen layout manager
   - Header + main container orchestration
   - Modal and panel state management
   - Escape key handler

2. **`BlurredHeader`**
   - Frosted glass effect (backdrop-filter: blur(12px))
   - Sticky positioning
   - Logo with gradient icon
   - Center navigation (4 links with active state)
   - Right actions (Sign In + Get Started)

3. **`SearchFilterBar`**
   - Absolute positioned overlay (top: 20px)
   - Dual-input search (query + location)
   - Search button with green gradient
   - Filter toggle button
   - Search suggestions dropdown
   - Focus state with green glow

4. **`SearchSuggestionsDropdown`**
   - 4 suggestion items
   - Icons + name + type badge
   - Hover states
   - Click to populate search
   - Auto-focus handling

5. **`InteractiveMap`**
   - Map library integration (Mapbox GL or Google Maps)
   - Custom marker components (8 categories)
   - Grid pattern overlay
   - Center placeholder with compass icon
   - Marker click handlers

6. **`MapMarker`**
   - Circular colored pins (36px)
   - Category-specific colors and icons
   - Hover scale animation (1.3x)
   - White border (3px)
   - Click to show quick view
   - Dynamic positioning

7. **`FilterPanel`**
   - Slide-in from left (320px width)
   - 4 filter sections: Categories, Rating, Hours, Features
   - Chip-based selection
   - Radio buttons for ratings
   - Close button
   - Active state toggle

8. **`FilterSection`**
   - Section title
   - Filter chips or radio options
   - Multi-select support
   - Active state management

9. **`FilterChip`**
   - Pill-shaped selectors
   - Inactive: white bg, gray border
   - Active: green gradient bg, white text
   - Hover: green border, green bg tint

10. **`BusinessListPanel`**
    - Fixed 400px right sidebar
    - Scrollable business list
    - Panel header with title + sort
    - Results count display
    - Sort dropdown

11. **`BusinessCard`**
    - Horizontal layout (image + details)
    - 70px square image with green border
    - Business name + category + rating
    - Distance badge + status badge
    - Top border animation on hover
    - Click to open quick view

12. **`BusinessImage`**
    - 70px × 70px rounded square
    - Gradient background fallback
    - Green border (2px)
    - Cover object-fit

13. **`BusinessMetaRow`**
    - Distance badge (green background)
    - Status badge (open/closed)
    - Space-between alignment

14. **`QuickViewModal`**
    - Full-screen overlay with blur
    - Centered content (max 680px)
    - Hero image header (240px)
    - Business details
    - 2×2 info grid (address, phone, hours, distance)
    - 3-button action row

15. **`ModalHeader`**
    - 240px height
    - Hero image background
    - Gradient fallback
    - Close button (top-right floating)

16. **`ModalInfoGrid`**
    - 2-column grid
    - 4 info cards with icons
    - Green gradient icon backgrounds
    - Labels + values

17. **`InfoCard`**
    - Horizontal layout
    - Icon (48px gradient square)
    - Label + value text
    - Gray background

18. **`ModalActions`**
    - 3-column button grid
    - Directions (outline)
    - Call Now (primary)
    - Save (outline)

19. **`RatingDisplay`**
    - Star icons (filled/half)
    - Rating number
    - Review count in gray

20. **`DistanceBadge`**
    - Green tint background
    - Dark green text
    - Rounded pill shape
    - Border

21. **`StatusBadge`**
    - Open: green background, dark green text
    - Closed: red background, dark red text
    - 24/7: special variant

22. **`SortDropdown`**
    - Custom styled select
    - Gray background
    - Border
    - Options: Distance, Rating, Name

---

## Interaction Specifications

### Map Interactions

**Marker Clicks:**
```typescript
interface MapMarkerProps {
  business: Business;
  position: { lat: number; lng: number };
  category: BusinessCategory;
  onClick: (business: Business) => void;
}

// Click marker → Open quick view modal
const handleMarkerClick = (business: Business) => {
  setSelectedBusiness(business);
  setIsQuickViewOpen(true);
};

// Hover marker → Scale 1.3x, increase z-index
// Mobile: Tap marker → Show tooltip, second tap → Open modal
```

**Map Controls:**
```typescript
interface MapState {
  center: { lat: number; lng: number };
  zoom: number;
  bounds: MapBounds;
  visibleMarkers: Business[];
}

// Pan map → Update visible businesses in sidebar
// Zoom → Recalculate distances
// Fit bounds to show all markers on load
```

### Search & Filter Interactions

**Search Input:**
```typescript
interface SearchState {
  query: string;
  location: string;
  suggestions: BusinessSuggestion[];
  isDropdownOpen: boolean;
}

// Focus input → Show suggestions
// Type → Filter suggestions (debounced 300ms)
// Click suggestion → Populate input, close dropdown
// Blur → Close dropdown after 200ms delay
// Enter key → Execute search
```

**Filter Panel:**
```typescript
interface FilterState {
  isOpen: boolean;
  categories: string[];
  rating: number | null;
  hours: string[];
  features: string[];
}

// Click "Filters" button → Slide in panel from left
// Toggle filter panel → Update button active state
// Click close (X) → Slide out panel
// Escape key → Close panel
// Click chip → Toggle active state
// Apply filters → Update map markers + business list
```

**Filter Application:**
```typescript
const applyFilters = (filters: FilterState, businesses: Business[]) => {
  return businesses.filter(business => {
    // Category filter
    if (filters.categories.length > 0) {
      if (!filters.categories.includes(business.category)) return false;
    }
    
    // Rating filter
    if (filters.rating && business.rating < filters.rating) return false;
    
    // Hours filter
    if (filters.hours.includes('Open Now') && !business.isOpen) return false;
    if (filters.hours.includes('Open 24/7') && !business.is24x7) return false;
    
    // Features filter
    if (filters.features.length > 0) {
      const hasAllFeatures = filters.features.every(f => 
        business.features?.includes(f)
      );
      if (!hasAllFeatures) return false;
    }
    
    return true;
  });
};
```

### Business Card Interactions

```typescript
// Hover business card → Show top green border, lift shadow
// Click business card → Open quick view modal
// Hover in list → Highlight corresponding marker on map (pulse animation)
```

### Modal Interactions

**Quick View Modal:**
```typescript
// Click business card or marker → Open modal
// Click close button → Close modal
// Click outside modal → Close modal
// Escape key → Close modal
// Modal open → Lock body scroll
// Modal close → Restore body scroll

// Action buttons
const handleDirections = (business: Business) => {
  const url = `https://maps.google.com/?q=${business.address.coordinates.lat},${business.address.coordinates.lng}`;
  window.open(url, '_blank');
};

const handleCallNow = (business: Business) => {
  window.location.href = `tel:${business.contact.phone}`;
};

const handleSave = (business: Business) => {
  // Add to saved businesses (user account feature)
  saveBusiness(business.id);
  showToast('Business saved!');
};
```

### Sort & Display

```typescript
interface SortOption {
  value: 'distance' | 'rating' | 'name';
  label: string;
}

const sortBusinesses = (businesses: Business[], sortBy: SortOption['value']) => {
  switch(sortBy) {
    case 'distance':
      return [...businesses].sort((a, b) => a.distance - b.distance);
    case 'rating':
      return [...businesses].sort((a, b) => b.rating - a.rating);
    case 'name':
      return [...businesses].sort((a, b) => a.name.localeCompare(b.name));
    default:
      return businesses;
  }
};
```

### State Management

**Global State:**
```typescript
interface MapViewState {
  // Map state
  mapCenter: { lat: number; lng: number };
  mapZoom: number;
  visibleBounds: MapBounds;
  
  // Search & filter
  searchQuery: string;
  locationQuery: string;
  activeFilters: FilterState;
  searchSuggestions: BusinessSuggestion[];
  
  // UI state
  isFilterPanelOpen: boolean;
  isQuickViewOpen: boolean;
  selectedBusiness: Business | null;
  
  // Data
  businesses: Business[];
  filteredBusinesses: Business[];
  sortBy: SortOption['value'];
}
```

---

## TypeScript Interfaces

**File:** `ui/components/types/map-view.types.ts`

```typescript
export interface Business {
  id: string;
  name: string;
  category: BusinessCategory;
  subcategory?: string;
  description?: string;
  image: string;
  rating: number;
  reviewCount: number;
  distance: number;
  distanceUnit: 'mi' | 'km';
  location: {
    lat: number;
    lng: number;
    address: string;
    city: string;
    state?: string;
    zip?: string;
  };
  contact: {
    phone: string;
    email?: string;
    website?: string;
  };
  hours: BusinessHours;
  isOpen: boolean;
  is24x7?: boolean;
  features?: BusinessFeature[];
  status: 'open' | 'closed' | 'open24x7';
}

export type BusinessCategory = 
  | 'restaurant' 
  | 'cafe' 
  | 'shop' 
  | 'service' 
  | 'health' 
  | 'retail' 
  | 'food' 
  | 'wellness';

export type BusinessFeature = 
  | 'delivery' 
  | 'takeout' 
  | 'wifi' 
  | 'parking' 
  | 'petFriendly' 
  | 'wheelchairAccess';

export interface BusinessHours {
  monday?: DayHours;
  tuesday?: DayHours;
  wednesday?: DayHours;
  thursday?: DayHours;
  friday?: DayHours;
  saturday?: DayHours;
  sunday?: DayHours;
}

export interface DayHours {
  open: string;
  close: string;
  isClosed: boolean;
}

export interface MapMarkerData {
  business: Business;
  position: { lat: number; lng: number };
  color: string;
  icon: string;
}

export interface FilterState {
  categories: BusinessCategory[];
  rating: number | null;
  hours: HoursFilter[];
  features: BusinessFeature[];
}

export type HoursFilter = 'openNow' | 'open24x7' | 'weekendHours';

export interface SearchSuggestion {
  id: string;
  name: string;
  type: 'business' | 'category' | 'location';
  category?: BusinessCategory;
  icon: string;
  business?: Business;
}

export interface MapBounds {
  north: number;
  south: number;
  east: number;
  west: number;
}

export interface MapState {
  center: { lat: number; lng: number };
  zoom: number;
  bounds: MapBounds | null;
  markers: MapMarkerData[];
}

export interface SortOption {
  value: 'distance' | 'rating' | 'name';
  label: string;
}

export const CATEGORY_COLORS: Record<BusinessCategory, string> = {
  restaurant: '#059669',
  cafe: '#f59e0b',
  shop: '#3b82f6',
  service: '#8b5cf6',
  health: '#ef4444',
  retail: '#06b6d4',
  food: '#059669',
  wellness: '#ef4444'
};

export const CATEGORY_ICONS: Record<BusinessCategory, string> = {
  restaurant: 'UtensilsCrossed',
  cafe: 'Coffee',
  shop: 'Book',
  service: 'Wrench',
  health: 'HeartPulse',
  retail: 'ShoppingBag',
  food: 'Apple',
  wellness: 'Sparkles'
};
```

---

## Design System Token Mapping

### Colors

```typescript
// Map HTML hex colors to design system tokens
{
  // Primary (Emerald)
  '#059669': 'emerald.600',
  '#10b981': 'emerald.500',
  '#f0fdf4': 'emerald.50',
  '#d1fae5': 'emerald.100',
  '#dcfce7': 'emerald.100',
  '#065f46': 'emerald.800',
  '#047857': 'emerald.700',
  
  // Status Colors
  '#f59e0b': 'amber.500',
  '#3b82f6': 'blue.500',
  '#8b5cf6': 'purple.500',
  '#ef4444': 'red.500',
  '#06b6d4': 'cyan.500',
  
  // Neutrals
  '#ffffff': 'white',
  '#fafafa': 'gray.50',
  '#f9fafb': 'gray.50',
  '#f3f4f6': 'gray.100',
  '#e5e7eb': 'gray.200',
  '#d1d5db': 'gray.300',
  '#9ca3af': 'gray.400',
  '#6b7280': 'gray.500',
  '#4b5563': 'gray.600',
  '#374151': 'gray.700',
  '#1f2937': 'gray.800',
  '#111827': 'gray.900'
}
```

### Tailwind Utility Classes

```typescript
// Component-specific class mappings

BlurredHeader:
"sticky top-0 z-[100] bg-white/98 backdrop-blur-xl border-b border-gray-100"

SearchFilterBar:
"absolute top-5 left-5 right-[420px] z-50 flex gap-3"

SearchContainer:
"flex-1 bg-white rounded-2xl shadow-lg border-2 border-transparent transition-all focus-within:border-emerald-500 focus-within:shadow-emerald-100 focus-within:ring-4 focus-within:ring-emerald-50"

FilterToggleButton:
"bg-white border-2 border-gray-200 rounded-2xl px-5 py-4 font-semibold text-gray-700 transition-all hover:border-emerald-500 hover:text-emerald-600 hover:bg-emerald-50 active:bg-emerald-500 active:text-white active:border-emerald-500"

MapMarker:
"absolute w-9 h-9 rounded-full flex items-center justify-center text-white text-sm shadow-lg border-3 border-white transition-all hover:scale-130 hover:z-20"

BusinessCard:
"bg-white rounded-2xl p-5 mb-4 cursor-pointer transition-all border-2 border-transparent hover:-translate-y-1 hover:shadow-xl hover:border-emerald-100 relative overflow-hidden before:absolute before:top-0 before:left-0 before:right-0 before:h-0.5 before:bg-gradient-to-r before:from-emerald-600 before:to-emerald-500 before:scale-x-0 before:transition-transform hover:before:scale-x-100"

FilterPanel:
"absolute top-20 left-5 w-80 bg-white rounded-3xl shadow-2xl z-[60] border-2 border-gray-200 max-h-[calc(100vh-120px)] overflow-y-auto transition-transform duration-400 ease-out -translate-x-full active:translate-x-0"

FilterChip:
"px-4 py-2 border-2 border-gray-200 rounded-xl text-sm font-medium cursor-pointer transition-all bg-white hover:border-emerald-500 hover:bg-emerald-50 hover:text-emerald-600 active:bg-gradient-to-br active:from-emerald-600 active:to-emerald-500 active:text-white active:border-emerald-600"

QuickViewModal:
"fixed inset-0 bg-black/60 z-[200] hidden items-center justify-center p-6 backdrop-blur-sm active:flex"

ModalContent:
"bg-white rounded-3xl w-full max-w-[680px] max-h-[85vh] overflow-y-auto shadow-2xl"

DistanceBadge:
"bg-emerald-50 text-emerald-800 px-2.5 py-1 rounded-lg text-xs font-semibold border border-emerald-100"

StatusBadgeOpen:
"bg-emerald-100 text-emerald-900 px-2.5 py-1 rounded-lg text-xs font-semibold"

StatusBadgeClosed:
"bg-red-100 text-red-900 px-2.5 py-1 rounded-lg text-xs font-semibold"
```

---

## Icon Mapping

**Font Awesome → Lucide React:**

```typescript
const iconMap = {
  // Navigation
  'fa-compass': 'Compass',
  'fa-search': 'Search',
  'fa-sliders-h': 'SlidersHorizontal',
  'fa-times': 'X',
  
  // Business Categories
  'fa-utensils': 'UtensilsCrossed',
  'fa-coffee': 'Coffee',
  'fa-book': 'Book',
  'fa-wrench': 'Wrench',
  'fa-heartbeat': 'HeartPulse',
  'fa-shopping-bag': 'ShoppingBag',
  'fa-apple-alt': 'Apple',
  'fa-spa': 'Sparkles',
  
  // Info & Actions
  'fa-map-marker-alt': 'MapPin',
  'fa-phone': 'Phone',
  'fa-clock': 'Clock',
  'fa-route': 'Route',
  'fa-directions': 'Navigation',
  'fa-heart': 'Heart',
  
  // Ratings
  'fa-star': 'Star'
};
```

**Usage:**
```typescript
import { 
  Compass, Search, SlidersHorizontal, X,
  UtensilsCrossed, Coffee, MapPin, Phone, Heart
} from 'lucide-react';

<Compass className="w-6 h-6" />
```

---

## Map Integration

### Map Library Setup

**Option 1: Mapbox GL JS**
```typescript
import mapboxgl from 'mapbox-gl';
import 'mapbox-gl/dist/mapbox-gl.css';

mapboxgl.accessToken = process.env.NEXT_PUBLIC_MAPBOX_TOKEN;

const map = new mapboxgl.Map({
  container: mapRef.current,
  style: 'mapbox://styles/mapbox/light-v11',
  center: [lng, lat],
  zoom: 13
});

// Add custom markers
businesses.forEach(business => {
  const el = document.createElement('div');
  el.className = 'custom-marker';
  el.style.backgroundColor = CATEGORY_COLORS[business.category];
  
  new mapboxgl.Marker(el)
    .setLngLat([business.location.lng, business.location.lat])
    .addTo(map);
});
```

**Option 2: React Map GL (Mapbox wrapper)**
```typescript
import Map, { Marker } from 'react-map-gl';

<Map
  mapboxAccessToken={process.env.NEXT_PUBLIC_MAPBOX_TOKEN}
  initialViewState={{
    latitude: 37.7749,
    longitude: -122.4194,
    zoom: 13
  }}
  style={{ width: '100%', height: '100%' }}
  mapStyle="mapbox://styles/mapbox/light-v11"
>
  {businesses.map(business => (
    <Marker
      key={business.id}
      latitude={business.location.lat}
      longitude={business.location.lng}
      onClick={() => handleMarkerClick(business)}
    >
      <MapMarkerComponent business={business} />
    </Marker>
  ))}
</Map>
```

**Option 3: Google Maps React**
```typescript
import { GoogleMap, LoadScript, Marker } from '@react-google-maps/api';

<LoadScript googleMapsApiKey={process.env.NEXT_PUBLIC_GOOGLE_MAPS_KEY}>
  <GoogleMap
    mapContainerStyle={{ width: '100%', height: '100%' }}
    center={{ lat: 37.7749, lng: -122.4194 }}
    zoom={13}
  >
    {businesses.map(business => (
      <Marker
        key={business.id}
        position={{ 
          lat: business.location.lat, 
          lng: business.location.lng 
        }}
        icon={{
          path: google.maps.SymbolPath.CIRCLE,
          fillColor: CATEGORY_COLORS[business.category],
          fillOpacity: 1,
          strokeColor: '#ffffff',
          strokeWeight: 3,
          scale: 18
        }}
        onClick={() => handleMarkerClick(business)}
      />
    ))}
  </GoogleMap>
</LoadScript>
```

### Custom Map Marker Component

```typescript
interface MapMarkerProps {
  business: Business;
  isHovered?: boolean;
  isSelected?: boolean;
}

export const MapMarkerComponent: React.FC<MapMarkerProps> = ({
  business,
  isHovered,
  isSelected
}) => {
  const Icon = CATEGORY_ICONS[business.category];
  const color = CATEGORY_COLORS[business.category];
  
  return (
    <div
      className={cn(
        "w-9 h-9 rounded-full flex items-center justify-center",
        "text-white text-sm shadow-lg border-3 border-white",
        "transition-all cursor-pointer",
        isHovered && "scale-130 z-20",
        isSelected && "scale-150 z-30 ring-4 ring-emerald-200"
      )}
      style={{ backgroundColor: color }}
    >
      <Icon className="w-4 h-4" />
    </div>
  );
};
```

---

## Accessibility Requirements

### WCAG 2.1 AA Compliance

**Keyboard Navigation:**
- Tab through all interactive elements
- Enter/Space activate buttons
- Escape closes modals and panels
- Arrow keys navigate suggestions
- Focus visible on all elements

**Screen Readers:**
```typescript
// Map container
<div 
  role="application" 
  aria-label="Interactive business map"
  aria-describedby="map-instructions"
>
  <div id="map-instructions" className="sr-only">
    Use arrow keys to pan map. Click markers to view business details.
  </div>
</div>

// Map markers
<button
  role="button"
  aria-label={`${business.name}, ${business.category}, ${business.distance} miles away, rating ${business.rating} stars`}
  onClick={() => handleMarkerClick(business)}
>
  <Icon aria-hidden="true" />
</button>

// Business cards
<article
  role="article"
  aria-labelledby={`business-name-${business.id}`}
  onClick={() => handleCardClick(business)}
>
  <h3 id={`business-name-${business.id}`}>{business.name}</h3>
  <div aria-label={`Rating: ${business.rating} stars out of 5, ${business.reviewCount} reviews`}>
    <Stars />
    <span>{business.rating}</span>
    <span>({business.reviewCount} reviews)</span>
  </div>
</article>

// Filter panel
<aside
  role="complementary"
  aria-label="Filter options"
  aria-hidden={!isFilterPanelOpen}
>
  <h3>Filter Results</h3>
  <div role="group" aria-labelledby="category-filter-label">
    <h4 id="category-filter-label">Categories</h4>
    {/* Filter chips */}
  </div>
</aside>

// Modal
<div
  role="dialog"
  aria-modal="true"
  aria-labelledby="modal-business-name"
  aria-describedby="modal-business-category"
>
  <h2 id="modal-business-name">{business.name}</h2>
  <p id="modal-business-category">{business.category}</p>
</div>
```

**Color Contrast:**
- All text meets 4.5:1 contrast ratio
- Marker icons visible against colored backgrounds
- Status badges have sufficient contrast
- Focus indicators clearly visible

**Focus Management:**
- Trap focus in modal when open
- Return focus to trigger element on close
- Focus first interactive element when filter panel opens
- Skip link to main content

---

## Mock Data Structure

**File:** `ui/components/map-view/mockData.ts`

```typescript
export const mockBusinesses: Business[] = [
  {
    id: 'biz-1',
    name: 'Corner Coffee House',
    category: 'cafe',
    subcategory: 'Coffee Shop',
    description: 'Cozy neighborhood coffee shop with artisan roasts and homemade pastries',
    image: '/images/businesses/corner-coffee.webp',
    rating: 4.9,
    reviewCount: 247,
    distance: 0.2,
    distanceUnit: 'mi',
    location: {
      lat: 37.7849,
      lng: -122.4094,
      address: '456 Community St',
      city: 'Downtown',
      state: 'CA',
      zip: '94102'
    },
    contact: {
      phone: '(555) 987-6543',
      email: 'info@cornercoffee.com',
      website: 'https://cornercoffee.example.com'
    },
    hours: {
      monday: { open: '7:00 AM', close: '9:00 PM', isClosed: false },
      tuesday: { open: '7:00 AM', close: '9:00 PM', isClosed: false },
      wednesday: { open: '7:00 AM', close: '9:00 PM', isClosed: false },
      thursday: { open: '7:00 AM', close: '9:00 PM', isClosed: false },
      friday: { open: '7:00 AM', close: '10:00 PM', isClosed: false },
      saturday: { open: '8:00 AM', close: '10:00 PM', isClosed: false },
      sunday: { open: '8:00 AM', close: '8:00 PM', isClosed: false }
    },
    isOpen: true,
    is24x7: false,
    features: ['wifi', 'parking', 'petFriendly', 'takeout'],
    status: 'open'
  },
  {
    id: 'biz-2',
    name: 'Roasted Bean Café',
    category: 'cafe',
    subcategory: 'Coffee Roastery',
    image: '/images/businesses/roasted-bean.webp',
    rating: 4.6,
    reviewCount: 128,
    distance: 0.4,
    distanceUnit: 'mi',
    location: {
      lat: 37.7889,
      lng: -122.4124,
      address: '789 Bean Street',
      city: 'Downtown',
      state: 'CA',
      zip: '94103'
    },
    contact: {
      phone: '(555) 456-7890'
    },
    hours: {
      monday: { open: '6:00 AM', close: '8:00 PM', isClosed: false },
      tuesday: { open: '6:00 AM', close: '8:00 PM', isClosed: false },
      wednesday: { open: '6:00 AM', close: '8:00 PM', isClosed: false },
      thursday: { open: '6:00 AM', close: '8:00 PM', isClosed: false },
      friday: { open: '6:00 AM', close: '9:00 PM', isClosed: false },
      saturday: { open: '7:00 AM', close: '9:00 PM', isClosed: false },
      sunday: { open: '7:00 AM', close: '7:00 PM', isClosed: false }
    },
    isOpen: true,
    features: ['wifi', 'delivery', 'takeout'],
    status: 'open'
  },
  {
    id: 'biz-3',
    name: 'Morning Brew & Bistro',
    category: 'restaurant',
    subcategory: 'Café & Bistro',
    image: '/images/businesses/morning-brew.webp',
    rating: 4.8,
    reviewCount: 195,
    distance: 0.6,
    distanceUnit: 'mi',
    location: {
      lat: 37.7799,
      lng: -122.4064,
      address: '321 Breakfast Blvd',
      city: 'Downtown',
      state: 'CA',
      zip: '94102'
    },
    contact: {
      phone: '(555) 123-4567'
    },
    hours: {
      monday: { open: '8:00 AM', close: '3:00 PM', isClosed: false },
      tuesday: { open: '8:00 AM', close: '3:00 PM', isClosed: false },
      wednesday: { open: '8:00 AM', close: '3:00 PM', isClosed: false },
      thursday: { open: '8:00 AM', close: '3:00 PM', isClosed: false },
      friday: { open: '8:00 AM', close: '4:00 PM', isClosed: false },
      saturday: { open: '9:00 AM', close: '4:00 PM', isClosed: false },
      sunday: { open: '9:00 AM', close: '2:00 PM', isClosed: false }
    },
    isOpen: true,
    features: ['wifi', 'delivery', 'takeout', 'parking'],
    status: 'open'
  },
  {
    id: 'biz-4',
    name: 'Artisan Coffee Co.',
    category: 'cafe',
    subcategory: 'Specialty Coffee',
    image: '/images/businesses/artisan-coffee.webp',
    rating: 4.7,
    reviewCount: 86,
    distance: 0.8,
    distanceUnit: 'mi',
    location: {
      lat: 37.7769,
      lng: -122.4184,
      address: '555 Artisan Way',
      city: 'Downtown',
      state: 'CA',
      zip: '94103'
    },
    contact: {
      phone: '(555) 789-0123'
    },
    hours: {
      monday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
      tuesday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
      wednesday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
      thursday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
      friday: { open: '7:00 AM', close: '6:00 PM', isClosed: false },
      saturday: { open: '8:00 AM', close: '5:00 PM', isClosed: false },
      sunday: { open: '', close: '', isClosed: true }
    },
    isOpen: false,
    features: ['wifi', 'takeout'],
    status: 'closed'
  },
  {
    id: 'biz-5',
    name: 'Campus Grind',
    category: 'cafe',
    subcategory: 'Study Café',
    image: '/images/businesses/campus-grind.webp',
    rating: 4.3,
    reviewCount: 312,
    distance: 1.1,
    distanceUnit: 'mi',
    location: {
      lat: 37.7819,
      lng: -122.4154,
      address: '888 Campus Drive',
      city: 'Downtown',
      state: 'CA',
      zip: '94102'
    },
    contact: {
      phone: '(555) 246-8135'
    },
    hours: {
      monday: { open: '24/7', close: '24/7', isClosed: false },
      tuesday: { open: '24/7', close: '24/7', isClosed: false },
      wednesday: { open: '24/7', close: '24/7', isClosed: false },
      thursday: { open: '24/7', close: '24/7', isClosed: false },
      friday: { open: '24/7', close: '24/7', isClosed: false },
      saturday: { open: '24/7', close: '24/7', isClosed: false },
      sunday: { open: '24/7', close: '24/7', isClosed: false }
    },
    isOpen: true,
    is24x7: true,
    features: ['wifi', 'parking', 'wheelchairAccess', 'takeout'],
    status: 'open24x7'
  }
];

export const mockSearchSuggestions: SearchSuggestion[] = [
  {
    id: 'sug-1',
    name: 'Corner Coffee House',
    type: 'business',
    category: 'cafe',
    icon: 'Coffee',
    business: mockBusinesses[0]
  },
  {
    id: 'sug-2',
    name: 'Roasted Bean Café',
    type: 'business',
    category: 'cafe',
    icon: 'Coffee',
    business: mockBusinesses[1]
  },
  {
    id: 'sug-3',
    name: 'Morning Brew & Bistro',
    type: 'business',
    category: 'restaurant',
    icon: 'UtensilsCrossed',
    business: mockBusinesses[2]
  },
  {
    id: 'sug-4',
    name: 'Downtown District',
    type: 'location',
    icon: 'MapPin'
  }
];

export const mockFilterOptions = {
  categories: ['Coffee Shops', 'Restaurants', 'Shopping', 'Services', 'Health', 'Wellness', 'Entertainment'],
  ratings: [
    { value: 5, label: 'Perfect (5 stars)', stars: '★★★★★' },
    { value: 4, label: 'Excellent (4+ stars)', stars: '★★★★' },
    { value: 3, label: 'Good (3+ stars)', stars: '★★★' }
  ],
  hours: ['Open Now', 'Open 24/7', 'Weekend Hours'],
  features: ['Delivery', 'Takeout', 'WiFi', 'Parking', 'Pet Friendly', 'Wheelchair Access']
};

export const mockSortOptions: SortOption[] = [
  { value: 'distance', label: 'Sort by Distance' },
  { value: 'rating', label: 'Sort by Rating' },
  { value: 'name', label: 'Sort by Name' }
];
```

---

## File Structure

```
ui/components/map-view/
├── types/
│   └── map-view.types.ts            # TypeScript interfaces
├── layout/
│   ├── MapViewLayout.tsx             # Main container
│   ├── BlurredHeader.tsx             # Frosted glass header
│   └── SearchFilterBar.tsx           # Top overlay search/filter
├── map/
│   ├── InteractiveMap.tsx            # Map library wrapper
│   ├── MapMarker.tsx                 # Custom marker component
│   └── MapControls.tsx               # Zoom, center controls
├── search/
│   ├── SearchContainer.tsx           # Dual input search
│   ├── SearchSuggestionsDropdown.tsx # Autocomplete dropdown
│   └── SuggestionItem.tsx            # Individual suggestion
├── filter/
│   ├── FilterPanel.tsx               # Slide-in filter panel
│   ├── FilterSection.tsx             # Section container
│   ├── FilterChip.tsx                # Chip selector
│   └── RatingOption.tsx              # Radio button option
├── business/
│   ├── BusinessListPanel.tsx         # Right sidebar
│   ├── BusinessCard.tsx              # Compact card
│   ├── BusinessImage.tsx             # 70px image
│   ├── BusinessMetaRow.tsx           # Distance + status
│   ├── DistanceBadge.tsx             # Green badge
│   └── StatusBadge.tsx               # Open/closed badge
├── modal/
│   ├── QuickViewModal.tsx            # Full modal
│   ├── ModalHeader.tsx               # Hero image header
│   ├── ModalInfoGrid.tsx             # 2x2 info grid
│   ├── InfoCard.tsx                  # Icon + label + value
│   └── ModalActions.tsx              # 3-button row
├── shared/
│   ├── RatingDisplay.tsx             # Stars + count
│   └── SortDropdown.tsx              # Sort select
├── hooks/
│   ├── useMapState.ts                # Map interactions
│   ├── useFilterState.ts             # Filter management
│   ├── useSearch.ts                  # Search + suggestions
│   └── useGeolocation.ts             # User location
├── utils/
│   ├── distance.ts                   # Distance calculations
│   ├── filters.ts                    # Filter logic
│   ├── mapHelpers.ts                 # Map utilities
│   └── hours.ts                      # Business hours logic
├── mockData.ts                       # Mock businesses + suggestions
├── index.ts                          # Barrel exports
└── README.md                         # Component documentation
```

---

## Testing Requirements

### Unit Tests

```typescript
// MapMarker.test.tsx
describe('MapMarker', () => {
  it('renders with correct category color', () => {
    render(<MapMarker business={mockBusinesses[0]} />);
    
    const marker = screen.getByRole('button');
    expect(marker).toHaveStyle({ backgroundColor: CATEGORY_COLORS.cafe });
  });

  it('scales on hover', async () => {
    const { container } = render(<MapMarker business={mockBusinesses[0]} />);
    
    await userEvent.hover(container.firstChild);
    expect(container.firstChild).toHaveClass('scale-130');
  });

  it('calls onClick when clicked', async () => {
    const mockOnClick = jest.fn();
    render(<MapMarker business={mockBusinesses[0]} onClick={mockOnClick} />);
    
    await userEvent.click(screen.getByRole('button'));
    expect(mockOnClick).toHaveBeenCalledWith(mockBusinesses[0]);
  });
});

// FilterPanel.test.tsx
describe('FilterPanel', () => {
  it('slides in when active', () => {
    render(<FilterPanel isOpen={true} />);
    
    expect(screen.getByRole('complementary')).toHaveClass('translate-x-0');
  });

  it('toggles filter chip active state', async () => {
    render(<FilterPanel isOpen={true} />);
    
    const chip = screen.getByText('Coffee Shops');
    await userEvent.click(chip);
    
    expect(chip).toHaveClass('active');
  });

  it('closes on escape key', async () => {
    const mockOnClose = jest.fn();
    render(<FilterPanel isOpen={true} onClose={mockOnClose} />);
    
    await userEvent.keyboard('{Escape}');
    expect(mockOnClose).toHaveBeenCalled();
  });
});

// SearchSuggestionsDropdown.test.tsx
describe('SearchSuggestionsDropdown', () => {
  it('shows suggestions on focus', async () => {
    render(<SearchContainer />);
    
    const input = screen.getByPlaceholderText(/find restaurants/i);
    await userEvent.click(input);
    
    expect(screen.getByText('Corner Coffee House')).toBeVisible();
  });

  it('populates input on suggestion click', async () => {
    render(<SearchContainer />);
    
    const input = screen.getByPlaceholderText(/find restaurants/i);
    await userEvent.click(input);
    
    await userEvent.click(screen.getByText('Corner Coffee House'));
    expect(input).toHaveValue('Corner Coffee House');
  });
});
```

### Integration Tests

```typescript
describe('MapView Integration', () => {
  it('filters businesses when filter applied', async () => {
    render(<MapViewLayout businesses={mockBusinesses} />);
    
    // Open filter panel
    await userEvent.click(screen.getByText('Filters'));
    
    // Select category
    await userEvent.click(screen.getByText('Coffee Shops'));
    
    // Verify filtered results
    const businessCards = screen.getAllByRole('article');
    businessCards.forEach(card => {
      expect(card).toHaveTextContent(/coffee|café/i);
    });
  });

  it('opens quick view modal on marker click', async () => {
    render(<MapViewLayout businesses={mockBusinesses} />);
    
    // Click map marker
    const marker = screen.getByLabelText(/corner coffee house/i);
    await userEvent.click(marker);
    
    // Verify modal opens
    expect(screen.getByRole('dialog')).toBeVisible();
    expect(screen.getByRole('heading', { name: 'Corner Coffee House' })).toBeVisible();
  });

  it('sorts businesses correctly', async () => {
    render(<MapViewLayout businesses={mockBusinesses} />);
    
    // Change sort
    const sortSelect = screen.getByRole('combobox');
    await userEvent.selectOptions(sortSelect, 'rating');
    
    // Verify order
    const businessNames = screen.getAllByRole('heading', { level: 3 });
    expect(businessNames[0]).toHaveTextContent('Corner Coffee House'); // 4.9
    expect(businessNames[1]).toHaveTextContent('Morning Brew'); // 4.8
  });
});
```

---

## Performance Optimization

### Map Rendering

```typescript
// Cluster markers when zoomed out
const useMark erClustering = (businesses: Business[], zoom: number) => {
  if (zoom < 11) {
    return clusterBusinesses(businesses);
  }
  return businesses;
};

// Lazy load map library
const Map = lazy(() => import('./InteractiveMap'));

<Suspense fallback={<MapSkeleton />}>
  <Map businesses={visibleBusinesses} />
</Suspense>
```

### Virtual Scrolling

```typescript
// Use react-window for long business lists
import { VariableSizeList } from 'react-window';

<VariableSizeList
  height={window.innerHeight - 200}
  itemCount={filteredBusinesses.length}
  itemSize={() => 150}
  width="100%"
>
  {({ index, style }) => (
    <div style={style}>
      <BusinessCard business={filteredBusinesses[index]} />
    </div>
  )}
</VariableSizeList>
```

---

## Constitution Alignment

### Vertical Slice Ownership
- Map domain owns all map-related components
- Clear separation: map, search, filter, business list
- Shared utilities for distance calculation and filtering

### Type Safety
- Comprehensive interfaces for all map data
- Strict typing for filter state and map bounds
- No `any` types in component props

### Design Fidelity
- Exact frosted glass header effect
- Precise marker colors per category
- Smooth slide-in animations for panels

### Observability
- Track map interactions (pan, zoom, marker clicks)
- Log filter applications
- Monitor search queries
- Track modal opens and action clicks

---

## Summary

This is a **comprehensive interactive map view interface** with:

- **22 modular React components** organized by domain
- **Full-screen map layout** with Mapbox/Google Maps integration
- **Frosted glass header** with backdrop blur
- **Floating search bar** with dual inputs and autocomplete
- **8 category-colored map markers** with hover animations
- **Slide-in filter panel** (320px) with 4 filter types
- **Fixed business list sidebar** (400px, scrollable)
- **Quick view modal** with hero image and actions
- **Real-time filtering** and sorting
- **Search suggestions** with business/location types
- **Responsive to map interactions** (pan, zoom)
- **Accessibility compliant** (WCAG 2.1 AA, keyboard navigation, screen reader support)
- **Type-safe** with comprehensive TypeScript interfaces
- **Performance optimized** (marker clustering, lazy loading, virtual scrolling)

The interface prioritizes **discoverability**, **visual appeal**, and **interactive exploration** through intuitive map controls, dynamic filtering, and immediate business details via quick view modals. Perfect for location-based business discovery applications.
