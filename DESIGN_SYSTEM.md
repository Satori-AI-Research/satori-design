# Satori Design System

## Philosophy

**Satori** (悟り) — the Japanese Zen concept of sudden clarity, seeing things as they truly are.

Our design follows the same principle: strip away everything that doesn't serve understanding. What remains should feel inevitable.

**Ma (間) — emptiness defines meaning.** Generous whitespace isn't empty, it's active. Every screen should feel like a calm, blank page that invites interaction. When in doubt, remove elements rather than add them.

**Progressive disclosure.** Show only what's needed. Empty states should feel welcoming, not broken. Hide sections until they have content. Reveal complexity gradually, not all at once.

**Typography-first.** Let beautiful type do the heavy lifting. Avoid boxing everything up. Use whitespace generously. The right typeface at the right weight communicates more than any icon or illustration.

---

## Colors

```css
/* Backgrounds */
--color-background-primary: #FAFAF8;     /* Warm off-white */
--color-background-secondary: #dae5f3;     /* Light blue */
--color-background-dark: #203148;          /* Navy */

/* Text */
--color-text-primary: #203148;             /* Navy - main text */
--color-text-secondary: #515151;           /* Gray - secondary text */

/* Accent */
--color-accent: #2584fa;                   /* Electric blue - single accent throughout */

/* UI / State */
--color-border-light: #d1d5db;
--color-error: #d4635f;
--color-success: #4a9b6d;
--color-warning: #c49a3c;
```

**Usage:**
- One accent color only (`#2584fa`) — for links, active states, hover effects
- Text is navy (`#203148`) or gray (`#515151`), never pure black
- Backgrounds are white or the subtle `hero-gradient`
- State colors (error/success/warning) only for status indicators and validation — never decorative

---

## Typography

**Fonts:**
- **Headings:** Poppins (semibold, tracking-wide)
- **Body:** Manrope (light weight, relaxed leading)
- **Mono/Labels:** Source Code Pro (uppercase, tracking-wider)

**Scale:**
```
.heading-1    → Hero titles (3rem → 4.5rem responsive)
.heading-2    → Page titles (2.25rem → 3.75rem responsive)
.heading-3    → Section titles (1.25rem → 1.5rem)
.heading-4    → Card titles (1.125rem → 1.25rem)

.body-text    → Default body (0.875rem → 1rem, light weight)
.body-text-lg → Emphasized body (1rem → 1.125rem)
.body-text-sm → Secondary text (0.875rem)
```

**Tags:**
```html
<span class="tag">Draft</span>
```
- Monospace, uppercase, small (12px)
- Subtle border, slightly rounded (4px) - NOT pill-shaped
- Use for: status badges, categories, metadata labels, section markers
- Keep it understated - tags are metadata, not the main content

---

## Layout

**Containers:**
```
.content-narrow  → max-w-2xl (forms, focused content)
.content-default → max-w-4xl (standard pages)
.content-wide    → max-w-7xl (dashboards, lists)
```

**Spacing principle:** Generous. When something feels cramped, add more space.

**Hero gradient background:**
```html
<div class="hero-gradient min-h-screen">
```
Use for: landing pages, empty states, project detail pages - anywhere we want that calm, inviting feel.

---

## Components

### Interactive Elements (Actions vs Navigation)

**When to use what:**

| Element | Use for | Examples |
|---------|---------|----------|
| `.link-arrow` | Navigation (going somewhere) | "View project →", "Back to dashboard" |
| `.btn-primary` | Primary action (doing something) | "Start Scrape", "Create Project", "Save" |
| `.btn-secondary` | Secondary action | "Cancel", "Skip", "Export" |
| `.tag` | Informational labels (not interactive) | Status badges, categories, metadata |

### Links (Navigation)
```html
<a class="link-arrow gap-2">
  View Details <ArrowRight size={16} />
</a>
```
- Monospace, uppercase, tracking-wider
- Black at rest, accent blue on hover
- Often paired with arrow icon
- **Use for navigation** - going to another page/view

### Buttons (Actions)
```html
<button class="btn-primary">Start Scrape</button>
<button class="btn-secondary">Cancel</button>
```
- **Use for actions** - triggering operations, form submissions, state changes
- Slightly rounded (4px) - NOT pill-shaped
- Primary: blue fill → outline on hover
- Secondary: subtle border → darker border on hover

**Disabled state:**
```html
<button class="btn-primary opacity-50 cursor-not-allowed pointer-events-none" disabled>
  Loading...
</button>
```

### Cards
```html
<div class="card card-hover">
  Content
</div>
```
- Subtle border (`border-gray-200`), rounded-xl
- On hover: border goes accent blue
- **Avoid heavy shadows** - we use outline style, not elevation

### Form Inputs
```html
<input class="input-field" placeholder="..." />
```
- Minimal underline style (no borders, transparent bg)
- Bottom border only, thickens + turns accent on focus
- Labels: simple gray text above, NOT monospace uppercase (save that for section markers)

**Boxed variant** (for date pickers, selects - where underline doesn't work):
```html
<input type="date" class="input-boxed" />
```

### Tag Input Pattern
For multi-value inputs (tags, subreddits, etc.):
```html
<input placeholder="Type and press Enter" class="input-field" />
<div class="flex flex-wrap gap-2 mt-3">
  <span class="tag flex items-center gap-2">
    Tag name
    <button class="hover:text-accent"><X size={12} /></button>
  </span>
</div>
```
- Input for adding, tags display below
- Tags use `.tag` class with X button to remove
- Enter key to add, no separate "Add" button needed

### Status Indicators
Just use text color, not colored badges:
```html
<span class="text-xs font-mono uppercase text-gray-500">Draft</span>
<span class="text-xs font-mono uppercase text-green-600">Ready</span>
```

---

## Patterns

### Multi-Step Wizards / Forms

**Philosophy:** Forms should feel like a conversation, not paperwork. One question at a time. No chrome.

**Structure:**
```html
<div class="min-h-screen hero-gradient flex flex-col">
  <!-- Minimal header: just logo, links back to exit -->
  <header>
    <Logo opacity-60 hover:opacity-100 />
  </header>

  <!-- Centered content -->
  <main class="flex-1 flex items-center justify-center">
    <div class="max-w-xl">
      <!-- Context breadcrumb (what they've entered so far) -->
      <p class="text-gray-400 font-mono text-sm uppercase tracking-wider mb-4">
        Project Name
      </p>

      <!-- Question as heading -->
      <h1 class="heading-1 mb-8">
        What are you<br />trying to learn?
      </h1>

      <!-- Single input -->
      <input class="input-field text-lg mb-12" />

      <!-- Navigation -->
      <div class="flex justify-between">
        <button class="text-gray-400 hover:text-gray-600 font-mono text-sm uppercase">Back</button>
        <button class="link-arrow">Continue →</button>
      </div>
    </div>
  </main>
</div>
```

**Key principles:**
- Full-screen with `hero-gradient` background (same calm feel as landing/dashboard)
- One question per screen when possible
- Question IS the heading (conversational, e.g. "What should we call this project?")
- Context breadcrumb shows what they've already entered (project name in gray mono)
- No step indicators (1 of 5) - feels bureaucratic
- "Continue" not "Next" - forward momentum
- "Skip" for optional fields, shows they can move on
- Back button is subtle gray, not a link-arrow

**Choice cards** (when offering options):
```html
<button class="w-full text-left p-6 bg-white/60 backdrop-blur-sm rounded-xl
               border border-transparent hover:border-accent transition-all group">
  <h3 class="heading-4 mb-2 group-hover:text-accent">Option title</h3>
  <p class="body-text-sm">Description of what this does.</p>
</button>
```
- Glassmorphism cards (`bg-white/60 backdrop-blur-sm`)
- Invisible border until hover
- Title highlights on hover

### Empty States
Center the content. Make it feel like an invitation, not an error.
```html
<div class="text-center pt-24">
  <span class="label">Projects</span>
  <h1 class="heading-1 mt-6 mb-6">Start<br />Something New</h1>
  <p class="body-text mb-10 max-w-md mx-auto">
    Helpful, friendly description.
  </p>
  <a class="link-arrow">Get Started <ArrowRight /></a>
</div>
```

### Page Headers
Simple. Label + big title. Maybe a subtitle.
```html
<span class="label">Section</span>
<h1 class="heading-1 mt-6 mb-6">Page Title</h1>
<p class="body-text-lg">Optional description</p>
```

### Navigation
- Navbar: Logo left, minimal actions right
- No heavy nav menus - keep it minimal

**Back navigation pattern:**
- Subtle arrow, never a full "← Back to X" text link
- Arrow floats in the **left margin**, content stays flush:
  ```html
  <div class="flex">
    <Link href="/back" class="-ml-8 mr-4 mt-1 text-gray-300 hover:text-accent">
      <ArrowLeft size={16} />
    </Link>
    <div>
      <span class="tag">Label</span>
      <h1 class="heading-1 mt-4">Title</h1>
    </div>
  </div>
  ```
- This keeps content alignment consistent between list and detail pages
- On centered/hero pages, arrow can go next to logo in header instead

### Data Display
Simple key-value rows, not boxed cards:
```html
<div class="flex justify-between py-3 border-b border-gray-200">
  <span class="text-gray-500">Label</span>
  <span class="font-mono">Value</span>
</div>
```

---

## Border Radius

Keep it subtle and consistent. We're not doing the 2010s "pill button" look.

```
--border-radius-sm: 4px   → tags, buttons, inputs
--border-radius-md: 8px   → small cards
--border-radius-lg: 12px  → cards
--border-radius-xl: 16px  → large cards, modals
--border-radius-full      → circles ONLY (avatars, close buttons)
```

**Rule:** If it's not a circle, don't use `rounded-full`.

---

## Performance & Navigation

**Overlays use state, not routes.**

When something opens as a full-screen overlay (wizard, modal, lightbox), use React state - not a separate page/route.

```tsx
// ✅ Good - instant open/close
const [showWizard, setShowWizard] = useState(false);
{showWizard && <Wizard onClose={() => setShowWizard(false)} />}

// ❌ Bad - triggers page navigation, server fetch, slow
router.push("/dashboard/new");
```

**Why:** Next.js page navigation triggers server-side data fetching, even with client components. A simple `useState` toggle is instant because no navigation occurs - the overlay just renders on top.

**Rule:** If the underlying page should stay loaded (dashboard behind a wizard), don't navigate away from it.

---

## Loading States

**Principle:** Skeleton only what's dynamic. Static content renders immediately.

| Content Type | Loading Behavior |
|--------------|------------------|
| Navbar | Render immediately (static) |
| Page titles/headers | Render immediately (static) |
| Section labels ("DATA CONFIG", "PROJECT INFO") | Render immediately (static) |
| Buttons/actions | Render immediately, disabled state |
| Filters/search | Render immediately, disabled state |
| Table headers | Render immediately (static) |
| **DB data** (names, values, lists) | **Skeleton** |

**Skeleton pattern:**
```html
<div className="h-4 w-32 bg-gray-200 rounded animate-pulse" />
```
- Use `bg-gray-200` for skeleton blocks
- Add `animate-pulse` for subtle animation
- Match approximate dimensions of real content

**Example - list page loading:**
```tsx
// ✅ Good - static shell with data skeletons
<Navbar />
<h1>All Projects</h1>  {/* static */}
<SearchInput disabled />  {/* static, disabled */}
<table>
  <thead>...</thead>  {/* static headers */}
  <tbody>
    {[...Array(5)].map(i => <SkeletonRow />)}  {/* skeleton rows */}
  </tbody>
</table>

// ❌ Bad - everything is skeleton
<SkeletonNavbar />
<SkeletonTitle />
<SkeletonFilters />
<SkeletonTable />
```

---

## Don'ts

- ❌ Heavy borders and shadows
- ❌ Multiple accent colors
- ❌ Pill-shaped buttons (rounded-full on rectangles)
- ❌ Crowded layouts with lots of sections
- ❌ Empty placeholder sections (hide until there's content)
- ❌ ALL CAPS for headings (only for tags)
- ❌ Complex multi-column layouts when single column works
- ❌ Buttons when links would do
- ❌ Generic "Submit" / "Cancel" - be specific
- ❌ Page routes for overlays/modals (use state instead)

## Do's

- ✓ Generous whitespace
- ✓ Let typography breathe
- ✓ Hero gradient for key pages
- ✓ Progressive disclosure (show less by default)
- ✓ Centered layouts for focused content
- ✓ Subtle hover states (border color change, not dramatic transforms)
- ✓ Friendly, inviting copy in empty states
- ✓ Monospace for data, dates, technical info

---

## Reference

The main website (satori-website) is the source of truth for the visual language. When unsure, check how something is done there.

Key files:
- `src/app/globals.css` - All component classes
- `src/components/Navbar.tsx` - Navigation pattern
- `src/app/page.tsx` - Landing page / sign-in pattern
- `src/app/dashboard/page.tsx` - Empty state pattern
