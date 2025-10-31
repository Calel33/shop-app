# 🎯 Business Owner Dashboard Integration Prompt

## 📋 Integration Request

I want to integrate a custom Business Owner Dashboard with split-view editor interface into our **project-componets** component library. Please extract and adapt this interface to work with our React + TypeScript + Tailwind CSS stack.

---

## **CURRENT PROJECT CONTEXT:**

- **Framework**: React 19 + Vite
- **Styling**: Tailwind CSS 3 (token-based design system from `design -system/`)
- **Backend**: Demo-ready components (no live backend, uses mock data)
- **Language**: TypeScript 5 (strict, no `any` types)
- **Target Directory**: `ui/components/business-dashboard/` (new domain)
- **Demo File**: `src/BusinessDashboardDemo.tsx`
- **Existing Functionality**: Component library with admin, payment, business-listing domains

---

## **UI TO INTEGRATE:**

Source: `ideas/businesslistingdash1.html`

### **Design Overview:**
A business owner's listing management dashboard with split-screen editor and live preview. The interface allows real-time editing with immediate visual feedback.

**Layout Structure:**
- Left sidebar navigation (280px, white background)
- Main content area split into two panes:
  - **Edit Section (55% width)**: Tabbed form interface with bottom actions
  - **Preview Section (45% width)**: Live preview with status card
- Three-tier structure: Header → Split Container → Content

**Key Visual Elements:**

1. **Sidebar Navigation**
   - Logo with icon: "LocalBiz Directory" (blue)
   - 5 nav items with icons:
     - Dashboard
     - Manage Listing (active)
     - Analytics
     - Settings
     - Help & Support
   - Active state: light blue background (#eff6ff), blue text
   - Hover: light gray background

2. **Header Bar**
   - Title: "Manage Your Listing" (28px, bold)
   - Right actions:
     - "Preview Live" button (secondary, with eye icon)
     - "Save Changes" button (primary blue, with save icon)
   - White background, bottom border

3. **Edit Section (Left Pane, 55%)**
   
   **Tabs Bar:**
   - 4 tabs: Basic Info (active), Hours, Photos, Contact Details
   - Light gray background for inactive tabs
   - White background + blue bottom border for active tab
   - Horizontal layout, full width

   **Form Content (scrollable):**
   - Business Name: Text input, pre-filled "The Corner Café"
   - Category: Dropdown with options (Restaurant & Dining selected)
   - Description: Textarea (100px height, resizable)
   - Address: Text input
   - Tags: Text input with comma-separated values
   - Business Photos: Drag-and-drop upload area
     - Dashed border
     - Cloud upload icon (48px, gray)
     - "Drag and drop photos here" text
     - Hint: "or click to browse • JPG, PNG up to 5MB each"
     - Hover: border turns blue, background light blue

   **Bottom Actions:**
   - Left: Version info "Last updated: Dec 15, 2024 • Version 3" with history icon
   - Right: Two buttons
     - "Save Draft" (secondary)
     - "Submit for Approval" (green/success, with paper plane icon)

4. **Preview Section (Right Pane, 45%)**
   
   **Preview Header:**
   - Title: "Live Preview" (18px, bold)
   - Subtitle: "This is how customers will see your listing" (gray, 14px)
   - White background

   **Preview Content (scrollable, light gray background):**
   
   **Status Card:**
   - White card with orange left border (4px)
   - Clock icon + "Pending Approval" title
   - Gray message text explaining review status
   
   **Business Card Preview:**
   - White card with shadow, rounded corners
   - Hero section: 200px gradient background (purple gradient)
     - Centered image icon placeholder
   - Info section padding:
     - Business name (24px, bold)
     - Category (blue text, medium weight)
     - Description paragraph (gray)
     - Details list (5 items with icons):
       - Map marker: Address
       - Clock: "Open • Closes at 8:00 PM"
       - Phone: Number
       - Globe: Website
       - Tags: Comma-separated tags

**Color Palette:**
- Primary Blue: #2563eb, #1d4ed8
- Light Blue: #eff6ff
- Success Green: #059669, #047857
- Warning Orange: #f59e0b (status border)
- Gray Scale: #f8fafc, #f1f5f9, #e2e8f0, #d1d5db, #9ca3af, #6b7280, #64748b, #475569, #374151, #1e293b, #0f172a
- Purple Gradient: #667eea to #764ba2 (hero placeholder)

**Typography:**
- Font: Inter (system-ui fallback)
- Header: 28px, 700 weight
- Card title: 24px, 700 weight
- Section titles: 18px, 600 weight
- Labels: 14px, 600 weight
- Body: 14px, 400-500 weight

**Split Layout:**
- Edit: 55% width
- Preview: 45% width
- Both sections scroll independently
- Vertical divider border between them

---

## **INTEGRATION REQUIREMENTS:**

### 1. 🔄 **Preserve Project Standards**
   - Follow `constitution.md` v1.0.0 principles
   - Use design tokens from `design -system/` ONLY
   - No hard-coded colors, spacing, or shadows
   - Files <500 lines each
   - Export all types from `ui/components/types/business-dashboard.types.ts`

### 2. 🎨 **Adapt Design Elements**
   - Convert HTML/CSS to modular React components
   - Replace inline styles with Tailwind utility classes
   - Create component hierarchy:
     - `BusinessDashboardLayout.tsx` (full page with sidebar)
     - `DashboardSidebar.tsx` (navigation)
     - `DashboardHeader.tsx` (header with actions)
     - `SplitViewContainer.tsx` (two-pane layout)
     - `EditPanel.tsx` (left pane with tabs and form)
     - `FormTabs.tsx` (tabbed navigation)
     - `BasicInfoForm.tsx` (basic info fields)
     - `HoursForm.tsx` (hours scheduler - placeholder)
     - `PhotosForm.tsx` (photo upload interface)
     - `ContactForm.tsx` (contact details - placeholder)
     - `DragDropUpload.tsx` (reusable file upload)
     - `PreviewPanel.tsx` (right pane with preview)
     - `StatusCard.tsx` (approval status display)
     - `BusinessCardPreview.tsx` (live preview card)
   - Responsive: stack panes vertically on mobile
   - WCAG 2.1 AA compliance

### 3. 🔧 **Technical Adaptations**
   - Create TypeScript interfaces in `ui/components/types/business-dashboard.types.ts`:
     - `BusinessEditData` (all editable fields)
     - `FormTabType` (enum: 'basic' | 'hours' | 'photos' | 'contact')
     - `ApprovalStatus` (enum: 'draft' | 'pending' | 'approved' | 'rejected')
     - `VersionHistory` (timestamp, version number)
     - `FileUpload` (file, preview URL, size)
   - State management:
     - Active tab state
     - Form field values (real-time sync)
     - Upload files state
     - Draft vs. published state
   - React 19 patterns (no unnecessary memo)
   - Real-time preview updates on form change
   - File upload with drag-and-drop

### 4. 📱 **Feature Integration**
   - **Tab Navigation**:
     - Click tab to switch form content
     - Active tab styling (blue border, white bg)
     - Preserve form state across tab switches
   - **Real-Time Preview**:
     - Update preview immediately on form input
     - Debounce text inputs (300ms)
     - Instant updates for selects/checkboxes
   - **File Upload**:
     - Drag-and-drop area
     - Click to browse files
     - Visual feedback on hover/drag
     - File type validation (JPG, PNG)
     - Size limit validation (5MB)
     - Preview uploaded images
   - **Form Actions**:
     - "Save Draft" button (saves locally)
     - "Submit for Approval" button (changes status)
     - "Preview Live" opens preview in new tab/modal
     - "Save Changes" primary action
   - **Version History**:
     - Display last updated timestamp
     - Version number tracking
   - **Independent Scrolling**:
     - Edit section scrolls independently
     - Preview section scrolls independently
     - Header/sidebar fixed

### 5. 🎯 **Specific Adaptations Needed**
   - Convert Font Awesome to Lucide icons:
     - `fa-map-marked-alt` → `MapPinned`
     - `fa-chart-bar` → `BarChart3`
     - `fa-edit` → `Edit`
     - `fa-chart-line` → `TrendingUp`
     - `fa-cog` → `Settings`
     - `fa-question-circle` → `HelpCircle`
     - `fa-eye` → `Eye`
     - `fa-save` → `Save`
     - `fa-cloud-upload-alt` → `CloudUpload`
     - `fa-history` → `History`
     - `fa-paper-plane` → `Send`
     - `fa-clock` → `Clock`
     - `fa-image` → `Image`
     - `fa-map-marker-alt` → `MapPin`
     - `fa-phone` → `Phone`
     - `fa-globe` → `Globe`
     - `fa-tags` → `Tags`
   - Split view layout: `grid grid-cols-[55%_45%]` or flexbox
   - Hero gradient: `bg-gradient-to-br from-indigo-500 to-purple-600`
   - Status border: `border-l-4 border-orange-500`
   - Drag-drop states: manage hover/active styling with React state

---

## **DELIVERABLES:**

1. ✅ Complete React component library under `ui/components/business-dashboard/`
2. ✅ TypeScript interfaces in `ui/components/types/business-dashboard.types.ts`
3. ✅ Tailwind CSS styling (100% token-based)
4. ✅ Demo implementation in `src/BusinessDashboardDemo.tsx` with:
   - Pre-filled business data
   - All 4 tabs functional
   - Real-time preview updates
   - File upload simulation
   - Version history tracking
5. ✅ Barrel export in `ui/components/business-dashboard/index.ts`
6. ✅ README.md with:
   - Usage examples
   - Tab system documentation
   - Real-time preview implementation guide
   - File upload integration
7. ✅ Integration summary: `BUSINESS_DASHBOARD_INTEGRATION_COMPLETE.md`
8. ✅ Responsive design: desktop split view → mobile stacked
9. ✅ Accessibility: keyboard nav, focus management, ARIA labels

---

## **TESTING REQUIREMENTS:**

- Verify tab switching preserves form state
- Test real-time preview updates for all form fields
- Validate file upload:
  - Drag-and-drop functionality
  - Click to browse
  - File type validation
  - Size limit enforcement
  - Multiple file handling
- Confirm independent scrolling in both panes
- Test responsive breakpoints (split → stacked)
- Validate "Save Draft" and "Submit for Approval" actions
- Check "Preview Live" modal/new tab functionality
- Test form validation for required fields
- Verify version history updates on save
- Test with various data:
  - Empty form (new business)
  - Partially filled form
  - Fully filled form
  - Long descriptions/addresses
  - Many tags
- Keyboard navigation through form fields
- Screen reader compatibility
- Focus management across tabs

---

## **DESIGN SYSTEM MAPPING:**

Map CSS values to Tailwind/design tokens:

**Colors:**
- `#2563eb` → `blue-600`
- `#1d4ed8` → `blue-700`
- `#eff6ff` → `blue-50`
- `#059669` → `green-600`
- `#047857` → `green-700`
- `#f59e0b` → `amber-500`
- `#f8fafc` → `slate-50`
- `#f1f5f9` → `slate-100`
- `#e2e8f0` → `slate-200`
- `#d1d5db` → `gray-300`
- `#64748b` → `slate-500`
- `#0f172a` → `slate-900`

**Layout:**
- Sidebar: `w-[280px]`
- Edit pane: `w-[55%]` or flex-grow
- Preview pane: `w-[45%]`
- Split container: `flex` or `grid grid-cols-[55%_45%]`

**Spacing:**
- Section padding: `p-8` (32px)
- Card padding: `p-6` (24px)
- Form spacing: `space-y-6` (24px)
- Gap: `gap-4` (16px)

**Typography:**
- Header: `text-3xl font-bold` (28px)
- Card title: `text-2xl font-bold` (24px)
- Section title: `text-lg font-semibold` (18px)
- Label: `text-sm font-semibold` (14px)

**Border Radius:**
- Cards: `rounded-xl` (12px)
- Inputs: `rounded-lg` (8px)
- Upload area: `rounded-xl` (12px)

---

## **FILE STRUCTURE:**

```
ui/components/business-dashboard/
├── index.ts                          # Barrel export
├── README.md                         # Documentation
├── BusinessDashboardLayout.tsx       # Full page container
├── DashboardSidebar.tsx              # Navigation sidebar
├── DashboardHeader.tsx               # Header with actions
├── SplitViewContainer.tsx            # Two-pane layout manager
├── EditPanel.tsx                     # Left pane wrapper
├── FormTabs.tsx                      # Tab navigation
├── forms/
│   ├── BasicInfoForm.tsx             # Basic info fields
│   ├── HoursForm.tsx                 # Hours scheduler
│   ├── PhotosForm.tsx                # Photo management
│   └── ContactForm.tsx               # Contact details
├── DragDropUpload.tsx                # File upload component
├── PreviewPanel.tsx                  # Right pane wrapper
├── StatusCard.tsx                    # Approval status display
└── BusinessCardPreview.tsx           # Live preview card

ui/components/types/
└── business-dashboard.types.ts       # All interfaces

src/
└── BusinessDashboardDemo.tsx         # Demo with full functionality
```

---

## **MOCK DATA STRUCTURE:**

Demo should include:

```typescript
interface MockDataStructure {
  business: BusinessEditData;          // The Corner Café data
  versionHistory: VersionHistory;      // Timestamp + version
  approvalStatus: ApprovalStatus;      // 'pending'
  categories: string[];                // All category options
  tabs: FormTabType[];                 // All available tabs
}

interface BusinessEditData {
  id: string;
  name: string;
  category: string;
  description: string;
  address: string;
  tags: string[];
  phone?: string;
  website?: string;
  email?: string;
  photos: FileUpload[];
  hours?: BusinessHours;
  status: 'open' | 'closed';
  closingTime?: string;
}
```

**Pre-filled Example:**
- Name: "The Corner Café"
- Category: "Restaurant & Dining"
- Description: "A cozy neighborhood café serving freshly roasted coffee..."
- Address: "123 Main Street, Downtown"
- Tags: ["coffee", "breakfast", "wifi", "outdoor seating"]
- Phone: "(555) 123-4567"
- Website: "www.cornercafe.com"
- Status: "Pending Approval"
- Last Updated: "Dec 15, 2024"
- Version: 3

---

## **STATE MANAGEMENT:**

Demo should manage:

```typescript
// Active tab
const [activeTab, setActiveTab] = useState<FormTabType>('basic');

// Form data (real-time updates)
const [formData, setFormData] = useState<BusinessEditData>(initialData);

// Upload state
const [uploadedFiles, setUploadedFiles] = useState<FileUpload[]>([]);
const [isDragging, setIsDragging] = useState(false);

// Draft state
const [isDraft, setIsDraft] = useState(true);
const [lastSaved, setLastSaved] = useState<Date>(new Date());

// Preview updates (debounced for text inputs)
const debouncedFormData = useDebounce(formData, 300);
```

---

## **REAL-TIME PREVIEW LOGIC:**

Implement immediate feedback:

```typescript
// Update preview on form change
useEffect(() => {
  // Update preview panel with debouncedFormData
  updatePreview(debouncedFormData);
}, [debouncedFormData]);

// Handle input changes
const handleFieldChange = (field: keyof BusinessEditData, value: any) => {
  setFormData(prev => ({ ...prev, [field]: value }));
};

// For selects/checkboxes (instant)
const handleSelectChange = (field: keyof BusinessEditData, value: string) => {
  setFormData(prev => ({ ...prev, [field]: value }));
  // Update preview immediately (no debounce)
};
```

---

## **FILE UPLOAD IMPLEMENTATION:**

Drag-and-drop functionality:

```typescript
const handleDrop = (e: React.DragEvent) => {
  e.preventDefault();
  setIsDragging(false);
  
  const files = Array.from(e.dataTransfer.files);
  const validFiles = files.filter(file => 
    ['image/jpeg', 'image/png'].includes(file.type) &&
    file.size <= 5 * 1024 * 1024 // 5MB
  );
  
  // Process valid files
  processFiles(validFiles);
};

const handleDragOver = (e: React.DragEvent) => {
  e.preventDefault();
  setIsDragging(true);
};

const handleDragLeave = () => {
  setIsDragging(false);
};

const handleClick = () => {
  // Trigger file input
  fileInputRef.current?.click();
};
```

---

## **TAB SYSTEM IMPLEMENTATION:**

Preserve state across tabs:

```typescript
const TabContent = ({ activeTab, formData, onChange }) => {
  switch (activeTab) {
    case 'basic':
      return <BasicInfoForm data={formData} onChange={onChange} />;
    case 'hours':
      return <HoursForm data={formData.hours} onChange={onChange} />;
    case 'photos':
      return <PhotosForm photos={formData.photos} onUpload={handleUpload} />;
    case 'contact':
      return <ContactForm data={formData} onChange={onChange} />;
    default:
      return null;
  }
};

// Tab navigation
const handleTabChange = (tab: FormTabType) => {
  setActiveTab(tab);
  // Form state persists, just changes visible content
};
```

---

## **INTERACTIVE BEHAVIORS:**

1. **Tab Switching**:
   - Click tab → change active tab
   - Blue bottom border slides to active tab
   - Form content swaps instantly
   - Form state preserved

2. **Real-Time Preview**:
   - Type in name → preview updates (debounced)
   - Select category → preview updates instantly
   - Edit description → preview updates (debounced)
   - Change address → preview updates (debounced)
   - Add tags → preview updates instantly

3. **File Upload**:
   - Drag files over → border blue, background light blue
   - Drop files → validate and process
   - Click area → open file dialog
   - Show error for invalid files (wrong type, too large)

4. **Form Actions**:
   - "Save Draft" → save form data, update last saved time
   - "Submit for Approval" → change status to pending, show success message
   - "Preview Live" → open modal or new tab with full preview
   - "Save Changes" → persist changes, update version

5. **Responsive Behavior**:
   - Desktop (>1024px): side-by-side 55/45 split
   - Tablet (768-1023px): narrower split or stacked
   - Mobile (<768px): fully stacked (edit above, preview below)

---

## **ACCESSIBILITY REQUIREMENTS:**

- Semantic HTML: `<nav>`, `<main>`, `<form>`, `<button>`
- Tab navigation: `role="tablist"`, `role="tab"`, `role="tabpanel"`
- `aria-label` for icon-only buttons
- `aria-current` for active nav item and tab
- `aria-describedby` for form hints
- Focus management: focus moves to tab panel on tab click
- Keyboard navigation: Arrow keys between tabs (optional enhancement)
- Error messages: `aria-live="polite"` for form validation
- File upload: keyboard accessible (Enter/Space to trigger)
- Color contrast: all text meets WCAG AA
- Focus visible states on all interactive elements

---

## **CONSTITUTION ALIGNMENT:**

This integration follows:
- ✅ **Principle 1**: Vertical slice (UI + types + demo + docs)
- ✅ **Principle 2**: Type-safe (strict TypeScript, validated schemas)
- ✅ **Principle 3**: Design system fidelity (tokens only)
- ✅ **Principle 4**: Observability (track save/submit events, upload metrics)
- ✅ **Principle 5**: Transparency (integration summary + session log)

---

## **USE CASES:**

This dashboard serves:
- Business owners managing their directory listings
- Self-service business profile editing
- Multi-step form with live preview
- Document/photo upload interfaces
- Draft/approval workflow UIs
- Admin content management systems
- Profile editing interfaces

**Reusability:**
- Split-view editor pattern reusable for any edit-preview workflow
- File upload component reusable for any drag-drop need
- Tab system reusable for multi-step forms
- Preview panel pattern reusable for live previews
- Status card reusable for workflow status displays

---

Please analyze the provided UI design from `ideas/businesslistingdash1.html` and implement it step-by-step, maintaining our component library standards while delivering a professional split-view business dashboard with real-time preview, file uploads, and multi-tab editing capabilities.
