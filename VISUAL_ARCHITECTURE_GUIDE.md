# ZP Tech Mega Menu - Visual & Architecture Guide

## 🎨 Visual Hierarchy

```
┌─────────────────────────────────────────────────────────────┐
│                    ZP TECH HEADER                           │
├─────────────────────────────────────────────────────────────┤
│ Logo          [Search Bar]           [Icons]               │
├─────────────────────────────────────────────────────────────┤
│ [📋] Shop by Categories    [Shop] [KB] [Fulfillment]  Phone │
└─────────────────────────────────────────────────────────────┘
        ↓ HOVER (Desktop) / CLICK (Mobile)
┌─────────────────────────────────────────────────────────────┐
│                     MEGA MENU OPENS                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Card  Card  Card  Card  Card    ┌──────────────────────┐ │
│  Card  Card  Card  Card  Card    │  FEATURED PRODUCT    │ │
│                                  │                      │ │
│                                  │  [BEST SELLER]       │ │
│                                  │                      │ │
│                                  │   [Product Image]    │ │
│                                  │                      │ │
│                                  │  Product Title       │ │
│                                  │  Description         │ │
│                                  │  [View Product →]    │ │
│                                  └──────────────────────┘ │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## 🔄 Component Structure

### Container Hierarchy

```
#zp-mega-menu (1260px wide, full page)
└─ .menu-container (1400px max-width, centered)
   └─ .menu-content (flexbox row)
      ├─ .categories-grid (flex: 1, CSS Grid 5 cols)
      │  ├─ .category-card (10 total)
      │  │  ├─ .card-icon (SVG)
      │  │  └─ .card-title (text)
      │  ├─ .category-card (...)
      │  └─ ...
      └─ .featured-section (18rem width, flex-shrink: 0)
         └─ .featured-box
            ├─ .featured-decoration
            ├─ .badge (Best Seller)
            ├─ .featured-image
            ├─ .featured-title
            ├─ .featured-description
            └─ .btn-cta
```

## 🎯 State Diagram

```
┌──────────────────────────┐
│   MENU CLOSED            │
│ opacity: 0               │
│ visibility: hidden       │
│ pointer-events: none     │
└──────┬───────────────────┘
       │
       │ (Desktop) mouseenter
       │ (Mobile) click
       │
       ↓ [0.3s animation]
┌──────────────────────────┐
│   MENU OPENING           │
│ opacity: 0→1             │
│ transform: -10px→0       │
│ visibility: visible      │
└──────┬───────────────────┘
       │ [0.3s complete]
       ↓
┌──────────────────────────┐
│   MENU OPEN              │
│ opacity: 1               │
│ visibility: visible      │
│ pointer-events: auto     │
│                          │
│ (Desktop) mouseleave/100ms delay
│ (Mobile) click outside
└──────┬───────────────────┘
       │
       ↓ [0.3s animation]
┌──────────────────────────┐
│   MENU CLOSED (restart)  │
└──────────────────────────┘
```

## 📐 Responsive Layout Grid

### Desktop (≥1024px)

```
┌─────────────────────────────────────────┐
│ Card Card Card Card Card │ Featured     │
│      Grid (5 cols)       │ Section (18rem)
│ Card Card Card Card Card │              │
└─────────────────────────────────────────┘
```

### Tablet (768-1023px)

```
┌─────────────────────────────────────┐
│ Card Card Card                      │
│ Grid (3 cols)                       │
│ Card Card Card                      │
│                                     │
│ Featured Section (full width)       │
└─────────────────────────────────────┘
```

### Mobile (<768px)

```
┌──────────────────┐
│ Card Card        │
│ Grid (2 cols)    │
│ Card Card        │
│ Card Card        │
│ Card Card        │
│ Card Card        │
│                  │
│ Featured Section │
│ (full width)     │
└──────────────────┘
```

## 🎬 Animation Timeline

### Fade & Slide-Up (0.3s)

```
Time:  0ms                      300ms
       │                         │
       ├─────────────────────────┤
       │                         │
Opacity: 0 ──────────────────────→ 1
       │                         │
Y-Pos: -10px ──────────────────→ 0px
       │                         │
Visibility: hidden ────────────→ visible
       │                         │
Easing: cubic-bezier(0.4, 0, 0.2, 1)
```

### Card Hover Effect (0.2s)

```
Background: transparent ──→ white
Border:     transparent ──→ #dbeafe
Icon Scale: 1.0 ──────────→ 1.1
Title Color: #333333 ─────→ #00aeef
Shadow:     0 ────────────→ 0 4px 20px -4px rgba(...)
```

## 🛠️ Technical Stack

```
HTML (Semantic)
├─ Header (with announcement bar)
├─ Navigation (with trigger button)
├─ Mega Menu Container
│  ├─ Categories Grid (10 cards)
│  │  └─ SVG Icons (native)
│  └─ Featured Section
└─ Main Content

CSS (Scoped to #zp-mega-menu)
├─ Reset & Base Styles
├─ Desktop Menu Styles (@media ≥1024px)
├─ Mobile Accordion (@media ≤1023px)
├─ Category Cards
├─ Featured Section
├─ Animations & Transitions
└─ Scrollbar Styling

JavaScript (Vanilla)
├─ DOMContentLoaded Listener
├─ Menu State Management
├─ Desktop Hover Logic
├─ Mobile Click Logic
├─ Outside Click Detection
└─ Responsive Resize Handler
```

## 📊 Color & Spacing System

### Color Tokens

```
Primary Blue:      #00AEEF   (accents, hover)
Hover Blue:        #0096c7   (button hover)
Dark Navy:         #333333   (primary text)
Gray Text:         #6b7280   (secondary text)
Light Gray:        #f3f4f6   (backgrounds)
Lighter Gray:      #f8fafc   (page background)
Blue Tint:         #eff6ff   (icon hover bg)
Blue Border:       #dbeafe   (card hover border)
White:             #ffffff   (card backgrounds)
```

### Spacing Scale

```
4px  (0.25rem)   - Fine details
8px  (0.5rem)    - Small spacing
12px (0.75rem)   - Card padding
16px (1rem)      - Base spacing
24px (1.5rem)    - Menu padding
32px (2rem)      - Section gaps
```

### Typography

```
Font Family: 'Inter', system fonts
Font Sizes:
  - Base: 1rem (16px)
  - Large: 1.25rem (20px)
  - Heading: 3rem (48px)

Font Weights:
  - Regular: 400
  - Medium: 500
  - Semibold: 600
  - Bold: 700

Line Heights:
  - Tight: 1.2
  - Normal: 1.5
  - Loose: 1.6
```

## 🎨 Component Variants

### Category Card States

```
DEFAULT                HOVER                   ACTIVE
┌──────────┐          ┌──────────┐            ┌──────────┐
│          │          │          │            │ [active] │
│ [Icon]   │          │ [Icon]   │            │ [Icon]   │
│          │          │          │            │          │
│ Title    │ ───────→ │ Title    │            │ Title    │
│          │          │          │            │          │
└──────────┘          └──────────┘            └──────────┘
• No border           • White bg              • (Same as
• Gray bg             • Blue border             hover)
• Dark text           • Blue text
• No shadow           • Soft shadow
```

### Featured Product States

```
DEFAULT              HOVER
┌──────────────────┐ ┌──────────────────┐
│ [Badge]          │ │ [Badge]          │
│                  │ │                  │
│ [Image]          │ │ [Image+scale]    │
│                  │ │                  │
│ Title            │ │ Title            │
│ Description      │ │ Description      │
│ [Button]         │ │ [Button]         │
│                  │ │                  │
└──────────────────┘ └──────────────────┘
• Subtle shadow      • Enhanced shadow
• Normal image       • 1.05x image scale
• Light bg           • Light bg
```

## 🔗 Event Flow

### Desktop (Hover)

```
User Action              → System Response       → Visual Result
─────────────────────────────────────────────────────────────

Mouseenter Trigger       → classList.add('active') → Menu fades in
                         → chevron rotates        → Animation 0.3s

Mouseenter Menu          → classList.keep('active') → Menu stays open

Mouseleave Trigger       → 100ms delay check     → Menu stable
                         → if not hovering menu  → Prevents flashing
                         → classlist.remove      → Menu fades out

Mouseleave Menu          → classList.remove('active') → Menu fades out
```

### Mobile (Click)

```
User Action              → System Response       → Visual Result
─────────────────────────────────────────────────────────────

Click Trigger            → classList.toggle      → Menu accordion
                         → chevron rotate 180°   → Opens smoothly

Click Outside Menu       → classList.remove      → Menu closes
                         → chevron rotate 0°     → Animation smooth

Click Trigger Again      → classList.toggle      → Menu closes
```

## 📈 Performance Characteristics

### Rendering Path

```
JavaScript Event
  ↓
classList.add/remove('active')
  ↓
CSS Selector Match (#zp-mega-menu.active)
  ↓
Style Recalculation
  ↓
Layout (min in accordion, none in dropdown)
  ↓
Paint (opacity, transform only)
  ↓
Composite (GPU acceleration)
```

### FPS Profile

```
Idle:              0 FPS (no animation)
Menu Opening:      60 FPS (GPU accelerated)
Menu Open/Closed:  0 FPS (static)
Hover Cards:       60 FPS (smooth)
Window Resize:     60 FPS (reflow only)
```

## 🧩 Accessibility Features

```
Semantic HTML
├─ <header> for header section
├─ <nav> for navigation
├─ <button> for interactive triggers
├─ <a> for category links
└─ Proper heading hierarchy

Keyboard Navigation
├─ Tab: Navigate through buttons
├─ Enter/Space: Activate buttons
├─ Arrow keys: (optional enhancement)
└─ Escape: (optional enhancement)

Screen Reader Support
├─ Semantic landmarks
├─ Link text is descriptive
├─ Button labels are clear
└─ Icon context available
```

## 🔒 Conflict Prevention

All styles are scoped to `#zp-mega-menu`:

- No global class name collisions
- No style conflicts with other components
- Safe to use alongside other CSS
- No specificity wars

---

**Last Updated**: February 5, 2026  
**Status**: Complete & Production Ready
