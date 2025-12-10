# Satori Design System

## Philosophy

**Zen, minimal, inviting.** Every screen should feel like a calm, blank page that invites interaction. Avoid clutter, heavy borders, and complex layouts. When in doubt, remove elements rather than add them.

**Progressive disclosure.** Show only what's needed. Empty states should feel welcoming, not broken. Hide sections until they have content.

**Typography-first.** Let beautiful type do the heavy lifting. Avoid boxing everything up. Use whitespace generously.

---

## Colors

```css
/* Primary palette */
--color-background-primary: white;
--color-background-secondary: #dae5f3;     /* Light blue */
--color-background-dark: #203148;          /* Navy */
--color-background-beige: #eddbc8;

/* Text */
--color-text-primary: #203148;             /* Navy - main text */
--color-text-secondary: #515151;           /* Gray - secondary text */

/* Accent */
--color-accent: #2584fa;                   /* Electric blue - single accent throughout */

/* UI */
--color-border-light: #d1d5db;
--color-error: #ef4444;
```

**Usage:**
- One accent color only (`#2584fa`) - for links, active states, hover effects
- Text is navy (`#203148`) or gray (`#515151`), never pure black
- Backgrounds are white or the subtle `hero-gradient`

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

**Labels/Pills:**
```html
<span class="label">Draft</span>
```
- Monospace, uppercase, small
- Bordered pill style
- Use for: status badges, categories, tags, section markers

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

### Links (Primary interaction)
```html
<a class="link-arrow gap-2">
  Action <ArrowRight size={16} />
</a>
```
- Monospace, uppercase, tracking-wider
- Black at rest, accent blue on hover
- Often paired with arrow icon
- **Preferred over buttons** for most CTAs

### Buttons (Secondary)
```html
<button class="btn-primary">Submit</button>
<button class="btn-secondary">Cancel</button>
```
- Reserve for form submissions or destructive actions
- Pill-shaped (rounded-full)
- Primary: blue fill → outline on hover
- Secondary: outline → fill on hover

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

### Chip/Tag Input Pattern
For multi-value inputs (tags, subreddits, etc.):
```html
<input placeholder="Type and press Enter" class="input-field" />
<div class="flex flex-wrap gap-2 mt-3">
  <span class="label flex items-center gap-2">
    Tag name
    <button class="hover:text-accent"><X size={12} /></button>
  </span>
</div>
```
- Input for adding, chips display below
- Chips use `.label` class with X button to remove
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
- Back navigation: Subtle arrow integrated with logo, not a separate link
- No heavy nav menus - keep it minimal

### Data Display
Simple key-value rows, not boxed cards:
```html
<div class="flex justify-between py-3 border-b border-gray-200">
  <span class="text-gray-500">Label</span>
  <span class="font-mono">Value</span>
</div>
```

---

## Don'ts

- ❌ Heavy borders and shadows
- ❌ Multiple accent colors
- ❌ Crowded layouts with lots of sections
- ❌ Empty placeholder sections (hide until there's content)
- ❌ ALL CAPS for headings (only for labels/pills)
- ❌ Complex multi-column layouts when single column works
- ❌ Buttons when links would do
- ❌ Generic "Submit" / "Cancel" - be specific

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
