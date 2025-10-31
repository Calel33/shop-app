# 🎯 Portfolio Grid Component Integration Prompt

## Generated from UI Integration Template
**Source Component:** `test/Responsive Portfolio Grid with Hover Cards.html`  
**Generated:** 2025-09-29

---

```
I want to integrate a custom UI design into our React Portfolio Components project. Please extract and adapt this interface to work with our React + TypeScript + Tailwind CSS stack.

**CURRENT PROJECT CONTEXT:**
- Framework: React 19 + Vite
- Styling: Tailwind CSS (with design system tokens)
- Backend: Static content (can be extended to CMS/API)
- Language: TypeScript
- Target file: src/components/portfolio/PortfolioGrid.tsx
- Existing functionality: Component library for portfolio/showcase websites

**UI TO INTEGRATE:**
```html
<section id="portfolio" class="mt-10">
    <div class="flex sm:mb-8 mb-6 items-end justify-between">
      <div class="">
        <p class="text-[11px] sm:text-xs tracking-widest text-neutral-500 uppercase font-geist">(03) Selected Work</p>
        <h3 class="mt-2 text-2xl sm:text-3xl tracking-tight font-geist font-medium" style="">A few projects I'm proud of.</h3>
      </div>
      <a href="#work" class="hidden sm:inline-flex items-center gap-2 ring-1 ring-neutral-200 hover:shadow text-sm text-neutral-700 font-geist bg-white rounded-full pt-2 pr-4 pb-2 pl-4">
        View Portfolio
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-up-right" class="lucide lucide-arrow-up-right w-[24px] h-[16px]" style="width: 24px; height: 16px; color: rgb(64, 64, 64);"><path d="M7 7h10v10" class=""></path><path d="M7 17 17 7" class=""></path></svg>
      </a>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 sm:gap-5">
      <!-- Column 1 -->
      <div class="flex flex-col gap-4 sm:gap-5">
        <a href="#work" class="group relative overflow-hidden ring-1 ring-neutral-200 bg-white rounded-3xl shadow-sm">
          <img src="https://hoirqrkdgbmvpwutwuwj-all.supabase.co/storage/v1/object/public/assets/assets/af5c4f11-0653-43c0-b21e-5b8cc085c9f3_800w.jpg" alt="Cloud Analytics dashboard project" class="h-56 w-full transition-transform duration-500 group-hover:scale-105 object-cover">
          <div class="pointer-events-none absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
          <div class="absolute bottom-0 left-0 right-0 p-5">
            <p class="text-xs text-white/70 font-geist">SaaS • Product</p>
            <div class="mt-1 flex items-center justify-between">
              <h4 class="text-base sm:text-lg tracking-tight font-medium text-white font-geist">Cloud Analytics</h4>
              <span class="inline-flex h-8 w-8 items-center justify-center rounded-full bg-white/90 text-neutral-900">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-right" class="lucide lucide-arrow-right h-4 w-4"><path d="M5 12h14" class=""></path><path d="m12 5 7 7-7 7" class=""></path></svg>
              </span>
            </div>
          </div>
        </a>

        <a href="#work" class="group relative overflow-hidden ring-1 ring-neutral-200 bg-white rounded-3xl shadow-sm">
          <img src="https://hoirqrkdgbmvpwutwuwj-all.supabase.co/storage/v1/object/public/assets/assets/60f49edd-2009-43cf-a12a-d82fd91aae5e_800w.jpg" alt="E-commerce platform" class="h-72 w-full transition-transform duration-500 group-hover:scale-105 object-cover">
          <div class="pointer-events-none absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
          <div class="absolute bottom-0 left-0 right-0 p-5">
            <p class="text-xs text-white/70 font-geist">E-commerce • Platform</p>
            <div class="mt-1 flex items-center justify-between">
              <h4 class="text-base sm:text-lg tracking-tight font-medium text-white font-geist">Shop Pro</h4>
              <span class="inline-flex h-8 w-8 items-center justify-center rounded-full bg-white/90 text-neutral-900">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-right" class="lucide lucide-arrow-right h-4 w-4"><path d="M5 12h14" class=""></path><path d="m12 5 7 7-7 7" class=""></path></svg>
              </span>
            </div>
          </div>
        </a>

        <a href="#work" class="group relative overflow-hidden ring-1 ring-neutral-200 bg-white rounded-3xl shadow-sm">
          <img src="https://hoirqrkdgbmvpwutwuwj-all.supabase.co/storage/v1/object/public/assets/assets/27aa90c0-b947-4bfd-b8da-7cf0ab291ab1_800w.jpg" alt="Portfolio website" class="h-48 w-full transition-transform duration-500 group-hover:scale-105 object-cover">
          <div class="pointer-events-none absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
          <div class="absolute bottom-0 left-0 right-0 p-5">
            <p class="text-xs text-white/70 font-geist">Portfolio • Website</p>
            <div class="mt-1 flex items-center justify-between">
              <h4 class="text-base sm:text-lg tracking-tight font-medium text-white font-geist">Creative Hub</h4>
              <span class="inline-flex h-8 w-8 items-center justify-center rounded-full bg-white/90 text-neutral-900">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-right" class="lucide lucide-arrow-right h-4 w-4"><path d="M5 12h14" class=""></path><path d="m12 5 7 7-7 7" class=""></path></svg>
              </span>
            </div>
          </div>
        </a>
      </div>

      <!-- Column 2 -->
      <div class="flex flex-col gap-4 sm:gap-5">
        <a href="#work" class="group relative overflow-hidden ring-1 ring-neutral-200 bg-white rounded-3xl shadow-sm">
          <img src="https://hoirqrkdgbmvpwutwuwj-all.supabase.co/storage/v1/object/public/assets/assets/b19e7d3a-309c-4d55-9373-80ca043c0f49_800w.jpg" alt="Product launch landing page" class="h-64 w-full object-cover transition-transform duration-500 group-hover:scale-105">
          <div class="pointer-events-none absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
          <div class="absolute bottom-0 left-0 right-0 p-5">
            <p class="text-xs text-white/70 font-geist">Platform • Website</p>
            <div class="mt-1 flex items-center justify-between">
              <h4 class="text-base sm:text-lg tracking-tight font-medium text-white font-geist">Boltshift Launch</h4>
              <span class="inline-flex h-8 w-8 items-center justify-center rounded-full bg-white/90 text-neutral-900">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-right" class="lucide lucide-arrow-right h-4 w-4"><path d="M5 12h14" class=""></path><path d="m12 5 7 7-7 7" class=""></path></svg>
              </span>
            </div>
          </div>
        </a>

        <a href="#work" class="group relative overflow-hidden ring-1 ring-neutral-200 bg-white rounded-3xl shadow-sm">
          <img src="https://hoirqrkdgbmvpwutwuwj-all.supabase.co/storage/v1/object/public/assets/assets/a76e4f7e-e0f8-4732-8b99-5b3abe6fd91d_800w.jpg" alt="Mobile app design" class="h-56 w-full transition-transform duration-500 group-hover:scale-105 object-cover">
          <div class="pointer-events-none absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
          <div class="absolute bottom-0 left-0 right-0 p-5">
            <p class="text-xs text-white/70 font-geist">Mobile • App</p>
            <div class="mt-1 flex items-center justify-between">
              <h4 class="text-base sm:text-lg tracking-tight font-medium text-white font-geist">FitTracker</h4>
              <span class="inline-flex h-8 w-8 items-center justify-center rounded-full bg-white/90 text-neutral-900">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-right" class="lucide lucide-arrow-right h-4 w-4"><path d="M5 12h14" class=""></path><path d="m12 5 7 7-7 7" class=""></path></svg>
              </span>
            </div>
          </div>
        </a>

        <a href="#work" class="group relative overflow-hidden ring-1 ring-neutral-200 bg-white rounded-3xl shadow-sm">
          <img src="https://hoirqrkdgbmvpwutwuwj-all.supabase.co/storage/v1/object/public/assets/assets/cac77434-d322-40be-a298-4e2198a61175_800w.jpg" alt="Data visualization" class="h-56 w-full transition-transform duration-500 group-hover:scale-105 object-cover">
          <div class="pointer-events-none absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
          <div class="absolute bottom-0 left-0 right-0 p-5">
            <p class="text-xs text-white/70 font-geist">Data • Visualization</p>
            <div class="mt-1 flex items-center justify-between">
              <h4 class="text-base sm:text-lg tracking-tight font-medium text-white font-geist">DataFlow</h4>
              <span class="inline-flex h-8 w-8 items-center justify-center rounded-full bg-white/90 text-neutral-900">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-right" class="lucide lucide-arrow-right h-4 w-4"><path d="M5 12h14" class=""></path><path d="m12 5 7 7-7 7" class=""></path></svg>
              </span>
            </div>
          </div>
        </a>
      </div>

      <!-- Column 3 -->
      <div class="flex flex-col gap-4 sm:gap-5">
        <a href="#work" class="group relative overflow-hidden ring-1 ring-neutral-200 bg-white rounded-3xl shadow-sm">
          <img src="https://hoirqrkdgbmvpwutwuwj-all.supabase.co/storage/v1/object/public/assets/assets/7df94c66-5d1e-4235-a476-1d2d8881a456_800w.jpg" alt="Design system" class="h-72 w-full transition-transform duration-500 group-hover:scale-105 object-cover">
          <div class="pointer-events-none absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
          <div class="absolute bottom-0 left-0 right-0 p-5">
            <p class="text-xs text-white/70 font-geist">Design • System</p>
            <div class="mt-1 flex items-center justify-between">
              <h4 class="text-base sm:text-lg tracking-tight font-medium text-white font-geist">Nexus System</h4>
              <span class="inline-flex h-8 w-8 items-center justify-center rounded-full bg-white/90 text-neutral-900">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-right" class="lucide lucide-arrow-right h-4 w-4"><path d="M5 12h14" class=""></path><path d="m12 5 7 7-7 7" class=""></path></svg>
              </span>
            </div>
          </div>
        </a>

        <a href="#work" class="group relative overflow-hidden ring-1 ring-neutral-200 bg-white rounded-3xl shadow-sm">
          <img src="https://hoirqrkdgbmvpwutwuwj-all.supabase.co/storage/v1/object/public/assets/assets/b1350108-f0ef-4f66-83ae-fe50447f6f74_800w.jpg" alt="Brand identity and campaign visuals" class="h-48 w-full object-cover transition-transform duration-500 group-hover:scale-105">
          <div class="pointer-events-none absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
          <div class="absolute bottom-0 left-0 right-0 p-5">
            <p class="text-xs text-white/70 font-geist">Identity • Campaign</p>
            <div class="mt-1 flex items-center justify-between">
              <h4 class="text-base sm:text-lg tracking-tight font-medium text-white font-geist">Quotient Rebrand</h4>
              <span class="inline-flex h-8 w-8 items-center justify-center rounded-full bg-white/90 text-neutral-900">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-right" class="lucide lucide-arrow-right h-4 w-4"><path d="M5 12h14" class=""></path><path d="m12 5 7 7-7 7" class=""></path></svg>
              </span>
            </div>
          </div>
        </a>

        <a href="#work" class="group relative overflow-hidden ring-1 ring-neutral-200 bg-white rounded-3xl shadow-sm">
          <img src="https://hoirqrkdgbmvpwutwuwj-all.supabase.co/storage/v1/object/public/assets/assets/68a7825c-0f07-4225-a8e0-d22929426aa3_800w.jpg" alt="Web application" class="h-56 w-full transition-transform duration-500 group-hover:scale-105 object-cover">
          <div class="pointer-events-none absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
          <div class="absolute bottom-0 left-0 right-0 p-5">
            <p class="text-xs text-white/70 font-geist">Web • Application</p>
            <div class="mt-1 flex items-center justify-between">
              <h4 class="text-base sm:text-lg tracking-tight font-medium text-white font-geist">TaskFlow Pro</h4>
              <span class="inline-flex h-8 w-8 items-center justify-center rounded-full bg-white/90 text-neutral-900">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-right" class="lucide lucide-arrow-right h-4 w-4"><path d="M5 12h14" class=""></path><path d="m12 5 7 7-7 7" class=""></path></svg>
              </span>
            </div>
          </div>
        </a>
      </div>
    </div>

    <div class="mt-8 sm:mt-10 flex justify-center">
      <a href="#work" class="inline-flex items-center gap-2 rounded-full bg-white ring-1 ring-neutral-200 px-5 py-3 text-sm text-neutral-700 hover:shadow font-geist">
        View All Work
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-up-right" class="lucide lucide-arrow-up-right w-[24px] h-[16px]" style="width: 24px; height: 16px; color: rgb(64, 64, 64);"><path d="M7 7h10v10" class=""></path><path d="M7 17 17 7" class=""></path></svg>
      </a>
    </div>
  </section>
```

**INTEGRATION REQUIREMENTS:**
1. 🔄 **Preserve All Existing Functionality**
   - Maintain component modularity and reusability
   - Keep TypeScript type safety
   - Preserve responsive design patterns
   - Maintain accessibility standards (ARIA labels, semantic HTML)

2. 🎨 **Adapt Design Elements**
   - Convert HTML to React TSX components
   - Replace inline SVGs with Lucide React icons (ArrowUpRight, ArrowRight)
   - Use design system tokens from `design-system/design.md` for:
     - Colors: neutral palette, white backgrounds
     - Typography: font-geist, tracking, text sizes
     - Spacing: gap-4, gap-5, padding values
     - Radius: rounded-3xl, rounded-full
     - Shadows: shadow-sm, hover:shadow
   - Ensure responsive breakpoints (sm:, md:) match Tailwind config
   - Maintain hover effects and transitions

3. 🔧 **Technical Adaptations**
   - Create TypeScript interfaces for:
     - `PortfolioItem` (image, title, category, link, height variant)
     - `PortfolioGridProps` (items array, sectionTitle, sectionSubtitle, viewAllLink)
   - Use React best practices:
     - Functional components with proper typing
     - Props destructuring
     - Map over items array for dynamic rendering
   - Implement proper event handlers for links
   - Add image loading optimization (lazy loading)
   - Optimize for React 19 performance

4. 📱 **Feature Integration**
   - Masonry-style grid layout with varying card heights
   - Hover scale animation on images (scale-105)
   - Gradient overlay on hover cards
   - Responsive column layout (1 col mobile, 3 cols desktop)
   - Icon button animations
   - Smooth transitions (duration-500)

5. 🎯 **Specific Adaptations Needed**
   - Replace `<a>` tags with Next.js `Link` component (or React Router if applicable)
   - Convert inline SVGs to `lucide-react` imports
   - Use design system color tokens instead of hard-coded colors
   - Adapt font-geist to project's typography system
   - Make portfolio items data-driven (accept props)
   - Create separate sub-components:
     - `PortfolioCard.tsx` - Individual card component
     - `PortfolioHeader.tsx` - Section header with title and CTA
     - `PortfolioGrid.tsx` - Main grid container
   - Ensure image URLs are configurable (not hard-coded)

**COMPONENT STRUCTURE:**
```
src/components/portfolio/
├── PortfolioGrid.tsx          # Main container component
├── PortfolioCard.tsx           # Individual portfolio card
├── PortfolioHeader.tsx         # Section header
├── types.ts                    # TypeScript interfaces
└── index.ts                    # Barrel export
```

**DELIVERABLES:**
1. ✅ Complete React + TypeScript component implementation
2. ✅ TypeScript interfaces in `types.ts`
3. ✅ Tailwind CSS with design system tokens
4. ✅ Lucide React icons integration
5. ✅ Working hover animations and transitions
6. ✅ Responsive design (mobile-first approach)
7. ✅ README.md with usage examples
8. ✅ INSTALLATION.md with setup instructions
9. ✅ USAGE_EXAMPLE.tsx with implementation example

**TESTING REQUIREMENTS:**
- Ensure component renders without errors
- Verify all hover effects work correctly
- Test responsive behavior on mobile, tablet, desktop
- Confirm image loading and optimization
- Validate TypeScript types are correct
- Check accessibility (keyboard navigation, screen readers)
- Test with different data sets (varying number of items)
- Verify design system tokens are applied correctly

**DESIGN SYSTEM COMPLIANCE:**
- Use only design system tokens (no hard-coded values)
- Follow spacing scale from design system
- Use typography tokens for all text
- Apply color palette consistently
- Use border radius tokens
- Apply shadow tokens for elevation

Please analyze the provided UI design and implement it step-by-step, maintaining our component library standards while delivering the exact visual design requested. Follow the file structure pattern established in `alimonyapp/componets/medical/` for consistency.
```

---

## 📦 **Expected Output Structure**

```
alimonyapp/componets/portfolio/
├── PortfolioGrid.tsx
├── PortfolioCard.tsx
├── PortfolioHeader.tsx
├── types.ts
├── index.ts
├── README.md
├── INSTALLATION.md
└── USAGE_EXAMPLE.tsx
```

## 🎨 **Design System Reference**

This component must use tokens from `design-system/design.md`:
- **Colors:** neutral-50 through neutral-900, white
- **Typography:** text-xs, text-sm, text-base, text-lg, text-2xl, text-3xl
- **Spacing:** gap-4, gap-5, p-5, mt-2, mb-6, mb-8
- **Radius:** rounded-3xl, rounded-full
- **Shadows:** shadow-sm, hover:shadow
- **Transitions:** duration-500, transition-transform

## 🚀 **Next Steps**

1. Copy this entire prompt
2. Submit to AI agent for implementation
3. Review generated components
4. Test in development environment
5. Integrate into main application

---

**Template Version:** 1.0  
**Component Type:** Portfolio Grid with Hover Cards  
**Complexity:** Medium  
**Estimated Implementation Time:** 2-3 hours
