# Design Document: theAGNT.ai

## Design Philosophy

theAGNT.ai embodies digital mystique through restraint. Every pixel serves the narrative of an organization that operates in the shadows, building the future without fanfare. The design whispers power through absence, not presence.

## Visual Identity

### Color Palette

**Primary Colors**
- `#000000` - True Black (primary background)
- `#0A0A0A` - Near Black (subtle elevation)
- `#FFFFFF` - Pure White (primary text)

**Accent Colors**
- `#1A1A1A` - Charcoal (interactive elements)
- `#2A2A2A` - Dark Gray (hover states)
- `#00FF88` - Electric Mint (singular accent - waitlist confirmation only)

**Functional Colors**
- `#FF3B30` - Error Red (system use only)
- `#34C759` - Success Green (minimal use)

### Typography

**Primary Typeface**: Inter
- Display: Inter 200 (Thin) - for "theAGNT.ai"
- Body: Inter 400 (Regular) - for UI elements
- Emphasis: Inter 500 (Medium) - for buttons

**Type Scale**
- Hero: 72px (desktop) / 48px (mobile)
- Body: 16px
- Small: 14px
- Micro: 12px (legal only)

### Grid & Spacing

**Layout System**
- 12-column grid with 24px gutters
- Base unit: 8px (all spacing multiples of 8)
- Max content width: 1440px
- Minimum margins: 24px (mobile) / 64px (desktop)

## Component Design

### Landing Page

**Hero Section**
- Full viewport height
- Centered logomark: "theAGNT.ai" in thin weight
- Subtle breathing animation (opacity 1 → 0.8 → 1, 4s loop)
- No tagline, no description

**Authentication Entry**
- Appears 100px below logo
- Ghost buttons with 1px border
- Labels: "Continue with Google" / "Continue with Apple" / "Continue with Email"
- 16px text, 48px height, full-width on mobile
- Hover: Background fills to #1A1A1A
- Active: Background to #2A2A2A

### Authenticated States

**Waitlist CTA (State 1)**
- Single button, perfectly centered
- Size: 200px × 56px
- Background: #1A1A1A
- Border: 1px solid #2A2A2A
- Text: "Join the Waitlist" (Inter Medium, 18px)
- Hover: Subtle glow effect (box-shadow)
- Click: Micro-interaction scale (0.98)

**Waitlist Confirmation (State 2)**
- Text: "You're on the waitlist."
- Color: #00FF88 (electric mint)
- Subtle fade-in animation
- Optional: Particle effect on confirmation

### Admin Dashboard

**Design Principles**
- Brutalist data presentation
- Monospace for data (IBM Plex Mono)
- High contrast, no decoration
- Function over form

**Layout**
- Fixed header with logout
- Left sidebar for navigation (future-proof)
- Main content area with data table
- No rounded corners anywhere

## Interaction Design

### Micro-interactions

**Page Load**
- Fade in from black (0.5s)
- Logo appears first, auth options 0.2s later

**Button Interactions**
- All transitions: 200ms ease-out
- Focus states: 2px offset outline
- Disabled states: 30% opacity

**Waitlist Joining**
- Button transforms to loading spinner
- Success: Morphs into confirmation text
- Subtle haptic feedback on mobile

### Animation Principles

- **Purposeful**: Every animation has meaning
- **Subtle**: Nothing calls attention to itself
- **Smooth**: 60fps minimum, prefer CSS over JS
- **Fast**: Nothing over 300ms except breathing effects

## Responsive Behavior

### Breakpoints
- Mobile: 320px - 767px
- Tablet: 768px - 1023px
- Desktop: 1024px+

### Mobile Adaptations
- Stack authentication options vertically
- Reduce logo size to 48px
- Increase tap targets to 44px minimum
- Remove hover effects, add touch feedback

## Accessibility

- WCAG AA compliance minimum
- Focus indicators on all interactive elements
- Screen reader announcements for state changes
- Keyboard navigation fully supported
- Respect prefers-reduced-motion

## Dark Mode Only

This is not a feature—it's the only mode. The interface is permanently dark, reinforcing our aesthetic and operational philosophy.

## Design Assets Needed

1. **Logo Design**
   - "theAGNT.ai" wordmark
   - Optional: Minimal logomark for favicon
   - Vector format (SVG)

2. **Icons**
   - Google "G" (official)
   - Apple logo (official)
   - Email icon (custom, minimal)
   - Loading spinner (custom)

3. **Error States**
   - 404 page (minimal)
   - 500 page (minimal)
   - Offline state

## Implementation Notes

### CSS Architecture
- CSS Modules for component isolation
- CSS variables for theme values
- Tailwind for utility classes
- No external UI libraries

### Performance Considerations
- Inline critical CSS
- Lazy load authentication providers
- Optimize font loading (preload Inter)
- No images except logos (SVG only)

### Browser Support
- Chrome/Edge (latest 2 versions)
- Safari (latest 2 versions)
- Firefox (latest 2 versions)
- Mobile Safari/Chrome

## Future Design Expansions

While out of current scope, the design system should accommodate:
- Venture reveal pages (maintaining mystery)
- Notification system (minimal toast)
- User settings (if needed)
- Email templates (same aesthetic)

## Design Inspiration

- Swiss International Style (reduction)
- Cyberpunk minimalism (mood)
- High-fashion websites (mystique)
- Crypto/DeFi interfaces (cutting-edge feel)

## Non-Negotiables

1. No explanatory text anywhere
2. No social proof or testimonials
3. No gradient backgrounds
4. No decorative elements
5. No light mode option
6. No personality—let mystery be the personality

The design should feel like discovering a secret society's digital doorway—intriguing, sophisticated, and slightly intimidating.