# Satori Design System

Shared design tokens and component styles for Satori products.

## Contents

- `tokens.css` - Design tokens (colors, typography, spacing)
- `components.css` - Component classes (buttons, cards, forms, etc.)
- `DESIGN_SYSTEM.md` - Design philosophy and usage guide

## Usage

### As a Git Submodule

Add to your project:
```bash
git submodule add https://github.com/your-org/satori-design.git design
```

Import in your CSS (after your Tailwind/framework imports):
```css
@import "./design/tokens.css";
@import "./design/components.css";
```

### Required Fonts

Load these fonts in your app:
- **Poppins** (300-700) - Headings
- **Manrope** (300-700) - Body text
- **Source Code Pro** - Monospace/labels

Example with Next.js:
```tsx
import { Poppins, Manrope, Source_Code_Pro } from "next/font/google";
```

## Updating

When the design system is updated:
```bash
git submodule update --remote
```

## Philosophy

**Zen, minimal, inviting.** See `DESIGN_SYSTEM.md` for the full guide.
