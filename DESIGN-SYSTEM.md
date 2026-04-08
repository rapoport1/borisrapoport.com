# Quantum Ascent — Design System

## Overview

**Quantum Ascent** is a glass morphism-inspired design system for personal brand websites, combining cosmic nebula aesthetics with rock climbing accents. The theme is production-ready, fully responsive, and requires zero JavaScript for core functionality.

## Design Philosophy

1. **Glass Morphism** — Frosted glass cards (blur + semi-transparent backgrounds) over dynamic backgrounds
2. **Cosmic Palette** — Deep space blacks, nebula purples/blues/pinks, inspired by planetary nebulae spectra
3. **Climbing Accents** — Warm oranges and rust tones representing earth, metal, and stone
4. **Minimal Motion** — Subtle, purposeful animations that enhance rather than distract
5. **Accessibility First** — WCAG AA compliance, keyboard navigation, reduced-motion support
6. **No JavaScript Dependencies** — Pure CSS for animations, hover states, and responsive design

## Color Palette

### Primary Space
- **Deep Navy** (`#0a0e27`) — Primary background, body text on light backgrounds
- **Secondary Navy** (`#1a1f3a`) — Footer, secondary backgrounds
- **Text Light** (`#f8fafc`) — Primary text color on dark backgrounds
- **Text Muted** (`#cbd5e1`) — Secondary text, descriptions

### Nebula Gradient
- **Purple** (`#7c3aed`) — Primary accent, headings, links
- **Blue** (`#3b82f6`) — Secondary nebula color, gradient transitions
- **Pink** (`#ec4899`) — Tertiary nebula color, dynamic accents

### Rock Climbing Accents
- **Orange** (`#f97316`) — CTA buttons, hover states, secondary actions
- **Rust** (`#b45309`) — Decorative accents, mountain silhouettes

### Glass
- **Glass Base** (`rgba(255, 255, 255, 0.1)`) — Default card background
- **Glass Hover** (`rgba(255, 255, 255, 0.15)`) — Hover state, enhanced clarity

## Typography

### Fonts
- **Headers:** Space Grotesk (modern, geometric, space-themed)
  - Fallback: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif
- **Body:** Inter (clean, readable, excellent at small sizes)
  - Fallback: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif
- **Code:** Courier New (monospace, technical consistency)

### Type Scale
```
H1: clamp(2.5rem, 8vw, 4.5rem)    — Hero titles, main headings
H2: 2rem                           — Section titles
H3: 1.5rem                         — Card headers
H4: 1.25rem                        — Subsections
P:  1rem (body) / 0.95rem (meta)   — Readable body text
```

### Line Heights
- Headings: 1.1 (tight, impactful)
- Body: 1.6 (readable, comfortable)
- Code: 1.5 (readable for technical content)

## Spacing System

```css
--spacing-xs:  0.5rem   (8px)
--spacing-sm:  1rem     (16px)
--spacing-md:  1.5rem   (24px)
--spacing-lg:  2rem     (32px)
--spacing-xl:  3rem     (48px)
--spacing-2xl: 4rem     (64px)
```

**Usage Pattern:**
- Margins between sections: `--spacing-2xl`
- Card padding: `--spacing-lg`
- Element gaps: `--spacing-md` / `--spacing-lg`
- Fine adjustments: `--spacing-xs` / `--spacing-sm`

## Components

### Glass Card (`.glass-card`)
```css
backdrop-filter: blur(10px);
background: rgba(255, 255, 255, 0.1);
border: 1px solid rgba(255, 255, 255, 0.1);
border-radius: 1rem;
padding: 2rem;
transition: all 300ms ease-out;
```

**States:**
- **Hover:** Elevated (`translateY(-4px)`), enhanced glass effect, glow shadow
- **Focus:** Purple outline (2px, 4px offset)

### Button Variants

#### Primary Button (`.btn-primary`)
- Background: Linear gradient (purple → blue)
- Shadow: Medium shadow + purple glow
- Hover: Lifted, enhanced glow

#### Secondary Button (`.btn-secondary`)
- Background: Glass effect
- Border: Subtle white border
- Hover: Border highlights, lifted

### Navigation (`.main-nav`)
- Sticky positioning at top
- Glass background with slight transparency
- Active link indicator (animated underline)
- Logo scales on hover

### Project Card (`.project-card`)
- Glass card base
- Flexible layout (title, description, tech badges, links)
- Status badge (green for active, gray for archived)
- Tech badges with purple outline
- Smooth link underline animations on hover

## Layout System

### Container
- Max-width: 1200px
- Responsive padding: `--spacing-lg` (2rem desktop, adjusts down)
- Horizontal centering with `margin: 0 auto`

### Grid Breakpoints
| Breakpoint | Width | Columns | Purpose |
|-----------|-------|---------|---------|
| Mobile | < 768px | 1 | Phone, small tablets |
| Tablet | 768px–1024px | 2 | Tablets, landscape phones |
| Desktop | 1024px–1400px | 3 | Desktops, wide laptops |
| Large | 1400px+ | 3+ | Ultra-wide displays |

### Responsive Behavior
- **Mobile-first:** Base styles for mobile, enhance with media queries
- **Fluid sizing:** Use `clamp()` for font sizes and spacing
- **Grid auto-fit:** `repeat(auto-fit, minmax(300px, 1fr))` for flexible grids
- **Touch-friendly:** Buttons 44px+ tall, 44px+ wide on touch devices

## Animations

### Nebula Drift (Background)
- **Duration:** 20–30 seconds
- **Easing:** Ease-in-out
- **Effect:** Subtle translation, creates sense of movement
- **Reduces Motion:** Disabled entirely

### Fade-In (Entrance)
- **Duration:** 600–800ms
- **Easing:** Ease-out
- **Used for:** Page sections, cards, hero content
- **Stagger:** 100ms between items in grids

### Hover Effects
- **Glass Cards:** Subtle lift (`-4px`) + glow
- **Links:** Animated underline (width: 0 → 100%)
- **Buttons:** Minimal lift on primary, border highlight on secondary

### Starfield Twinkle
- **Duration:** 5 seconds
- **Opacity:** 0.3–0.8 (subtle)
- **Creates:** Living background effect

## Accessibility

### WCAG AA Compliance
- Color contrast: 4.5:1 (text on background)
- Interactive elements: 3:1 (visual distinguishability)
- Keyboard navigation: All interactive elements focusable
- Focus indicators: 2px purple outline, 4px offset

### Responsive Text
- Base font size: 16px (100% of user preference)
- Scaling: Relative units (rem) for easy customization
- Min/max sizes via `clamp()` prevent extreme scaling

### Motion
- Respects `prefers-reduced-motion`
- All animations can be disabled via media query
- Core functionality works without motion

### Touch Devices
- Buttons: 44×44px minimum (WCAG AAA)
- Spacing: Adequate touch targets with breathing room
- Removed hover effects on coarse pointer devices (use `:active` instead)

## Performance Optimizations

### CSS
- No @imports (external fonts are preconnected)
- Efficient selectors (avoid deep nesting)
- Hardware acceleration for transforms
- CSS variables for theme customization

### Assets
- SVG icons (scalable, no HTTP requests)
- Optimized images (WebP with PNG fallback)
- Lazy loading for below-fold images
- Static fonts (no dynamic loading)

### Lighthouse Targets
- Performance: 90+
- Accessibility: 95+
- Best Practices: 90+
- SEO: 100

## Dark Mode (Default)

This theme is **dark-mode-first**. No light mode is currently implemented, but the CSS structure makes it easy to add:

```css
@media (prefers-color-scheme: light) {
  :root {
    --color-space-primary: #ffffff;
    --color-text-light: #1a1f3a;
    /* ... etc */
  }
}
```

## Customization

### Changing Colors
Edit CSS variables in `:root` in `quantum-ascent.css`:
```css
:root {
  --color-nebula-purple: #7c3aed; /* Change primary accent */
  --color-accent-orange: #f97316; /* Change CTA color */
}
```

### Changing Typography
Swap font families in `:root`:
```css
--font-header: "Your Font", sans-serif;
--font-body: "Your Font", sans-serif;
```

### Adjusting Spacing
Modify spacing scale in `:root`:
```css
--spacing-lg: 2.5rem; /* Increase from 2rem */
```

### Container Width
Change in `quantum-ascent.css`:
```css
.container {
  max-width: 1400px; /* From 1200px */
}
```

## File Structure

```
themes/quantum-ascent/
├── layouts/
│   ├── _default/
│   │   ├── baseof.html       (Base template)
│   │   ├── single.html       (Single post/page)
│   │   └── list.html         (List pages)
│   ├── index.html            (Homepage)
│   ├── partials/
│   │   ├── nav.html          (Navigation)
│   │   └── footer.html       (Footer)
│   └── section/
│       ├── projects.html     (Projects grid)
│       └── contact.html      (Contact form)
├── static/
│   ├── css/
│   │   ├── quantum-ascent.css (Main styles)
│   │   ├── animations.css     (Animation definitions)
│   │   └── responsive.css     (Media queries)
│   ├── js/                    (Empty — no dependencies)
│   └── images/
│       ├── favicon.svg        (Site icon)
│       └── logo.svg           (Optional branding)
└── theme.toml
```

## Browser Support

- Chrome/Edge: 100+
- Firefox: 95+
- Safari: 15+
- Mobile: iOS Safari 15+, Chrome Android 100+

**Unsupported Features:**
- IE11 (no CSS Grid, no CSS variables, no backdrop-filter)
- Very old Safari versions (pre-CSS Grid)

## Future Enhancements

Potential additions without breaking changes:
- [ ] Dark/light theme toggle (CSS variables support this)
- [ ] Blog section template
- [ ] Image lightbox (pure CSS)
- [ ] Newsletter signup (embedded form)
- [ ] Client testimonials carousel
- [ ] Search functionality (static site search via JSON)

## Questions?

This design system is documented and maintainable. See `MAINTENANCE.md` for updating and extending the theme.
