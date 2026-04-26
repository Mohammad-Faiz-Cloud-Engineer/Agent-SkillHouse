---
name: UI/UX Design
version: 1.0.0
description: Designer-grade UI/UX engineering for stunning, unique, production-ready interfaces
author: Mohammad Faiz
tags: [ui, ux, design, frontend, components, styling, accessibility]
category: specialized
activation: manual
priority: high
file_patterns: ["**/*.{jsx,tsx,vue,svelte,html,css,scss}"]
design_principles: [personality-driven, visual-hierarchy, motion-aware, accessibility-first]
output_quality: designer-grade
---

# UI/UX Design

World-class UI/UX engineering. Every interface must look designer-crafted, not AI-generated. Generic is unacceptable. Boring is a bug. Ship beauty.

## Before Writing Code

Answer these first:
1. What is the personality? (bold, minimal, playful, premium, futuristic, warm)
2. What is the visual hierarchy? (what user sees first, second, third)
3. What makes this screen feel alive? (motion, depth, texture, color, contrast)
4. What would make someone screenshot this?

If you can't answer, you're not ready to build.

## Design System

### Color
- Never use raw defaults (blue-500, gray-200 straight from box)
- Build deliberate system: one primary, one accent, one surface, one text scale
- Use color with intent, not decoration
- Gradients: subtle angles, layer with opacity for depth
- Dark backgrounds: true deep tones (#0a0a0f, #0d0d1a, #0f0e17) not #000 or #111
- Light backgrounds: warm/cool off-whites (#fafaf9, #f8f7ff) not #fff
- Accent colors must pop against surface — test contrast
- Use color to guide attention

### Typography
- Define clear type scale: display → heading → subheading → body → caption
- Display text: bold, large, confident (if looks "fine", make bigger)
- Line height: tight for headings (1.1–1.2), relaxed for body (1.6–1.7)
- Letter spacing: tight for large headings (-0.02em), open for all-caps labels (0.08–0.12em)
- Font weight contrast creates hierarchy — use aggressively
- Never mix >2 typefaces
- Text needs breathing room from background

### Spacing & Layout
- Consistent spacing scale — every gap/padding/margin on grid
- Generous whitespace is design
- Sections need breathing room — large padding-top/bottom
- Cards/modals/containers need luxurious internal padding
- Alignment must be deliberate
- Asymmetry can be beautiful
- Group related things. Separate unrelated with space.

### Depth & Dimension
- Flat and lifeless is lazy, not minimal
- Shadows with personality:
  - Soft: `0 2px 8px rgba(0,0,0,0.06)`
  - Medium: `0 8px 32px rgba(0,0,0,0.12)`
  - Strong: `0 24px 64px rgba(0,0,0,0.2)`
  - Colored: element's color at low opacity
- Glassmorphism: `backdrop-filter: blur(16px)` with semi-transparent backgrounds (only on dark/image backgrounds)
- Borders: 1px with subtle opacity on dark surfaces
- Layer intentionally: foreground, midground, background

### Motion & Interaction
- Every interactive element must have hover state. No exceptions.
- Hover states must feel designed:
  - Scale up: `transform: scale(1.02)`
  - Shift shadow depth
  - Slide in underline/accent
  - Change background with smooth transition
- Transitions: `150–250ms ease` for micro-interactions, `300–400ms ease` for larger changes
- Entrance animations: fade up (`opacity 0→1 + translateY 16px→0`), stagger children 50–80ms delay
- Loading states: skeleton screens, animated shimmer, purposeful spinners (never plain "Loading...")
- Empty states: illustration, icon, helpful copy

## Component Standards

### Buttons
- Primary: bold background, strong contrast text, rounded corners, hover scale + shadow shift, active press scale down
- Never plain flat rectangle with default blue
- Consider: gradient fill, border-only ghost, icon + label
- Size must feel substantial

### Cards
- Must have visual personality (not white box with gray border)
- Use: subtle gradient backgrounds, left accent borders, icon headers, image banners, glassmorphism, layered shadows
- Hover state must animate (lift, glow, reveal hidden elements)

### Forms & Inputs
- Premium feel: floating labels, animated focus rings, smooth border transitions
- Focus ring: colored glow matching accent (not default blue outline)
- Error states: red border + shake animation + inline message
- Success states: green accent + checkmark animation

### Navigation
- Active states obvious and designed (not just bold text)
- Hover states smooth
- Mobile nav slides in with animation (never just appears)

### Hero Sections
- Clear focal point: headline, subheadline, CTA
- Never center everything
- Background: gradient, mesh gradient, image with overlay, particle field, abstract shapes (never plain solid unless extremely intentional)

### Tables & Lists
- Alternating row colors or hover highlights (never plain grids)
- Data must breathe — enough row padding

## Forbidden Patterns

Never build:
- Default browser button styles
- Plain white cards with gray borders and no character
- Forms with no focus states
- Pages with no visual hierarchy
- Blue #3B82F6 as primary with no customization
- Centered text on every section
- No hover states on interactive elements
- `border-radius: 4px` uniformly
- Placeholder grey boxes as images
- Generic sans-serif at 16px with no type scale
- Pages from Tailwind tutorials

## Responsiveness

- Mobile-first always
- Tap targets minimum 44x44px on mobile
- Font sizes must scale gracefully
- Spacing compresses on mobile (not uniform shrink)
- Navigation: deliberate mobile pattern (drawer, bottom nav, hamburger with designed open state)

## Accessibility (Non-Negotiable)

- Color contrast minimum 4.5:1 for body text, 3:1 for large text
- All interactive elements keyboard focusable with visible focus ring
- Images have descriptive alt text
- ARIA labels on icon-only buttons
- Don't rely on color alone to communicate state

## Dark Mode

- Never just invert colors
- Dark surfaces use layered neutrals (not one flat dark)
- Text on dark: never pure white (#fff) — use #f0f0f0, #e8e8e8, tinted whites
- Shadows on dark: colored glows instead of dark box shadows
- Borders on dark: `rgba(255,255,255,0.08)` (not hard white lines)

## Final Check

Before delivering:
- [ ] Would senior designer approve without changes?
- [ ] Every interactive element has hover and focus state?
- [ ] Clear visual hierarchy on every screen?
- [ ] Color system intentional and consistent?
- [ ] Transitions and animations smooth and purposeful?
- [ ] Looks unique (not like every other AI-generated UI)?
- [ ] Would someone screenshot and share this?

If any answer is no, fix before delivering.

## Output Format

```
COMPONENT: [Name]
──────────────────────────────────────────
DESIGN DECISIONS:
- Personality: [chosen]
- Primary Color: [hex + rationale]
- Typography: [fonts + scale]
- Key Interactions: [hover states, animations]
- Unique Elements: [what makes this special]
──────────────────────────────────────────
CODE:
[Complete component code with all styles]
──────────────────────────────────────────
ACCESSIBILITY NOTES:
- Contrast ratios: [verified values]
- Keyboard navigation: [implementation]
- ARIA labels: [where applied]
```

## Non-Negotiable Rules

1. Generic is unacceptable — every UI must have personality
2. Every interactive element has hover and focus states — no exceptions
3. Visual hierarchy must be obvious
4. Color system must be intentional
5. Spacing must be generous
6. Accessibility is mandatory
7. Mobile-first always
8. Animations must be smooth
9. Components must be unique
10. The bar is beauty, not just "it works"

## Conflict Resolution

If request conflicts with design standards:
1. Apply standards by default
2. State conflict: "This would create generic-looking UI"
3. Offer designer-grade alternative
4. Deviate only if user explicitly overrides

The bar is not "it works." The bar is "it is beautiful, unique, and production-ready."
