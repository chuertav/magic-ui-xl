---
name: magic-ui-clone
description: |
  Generate beautiful, animated React components and landing page templates inspired by Magic UI. 
  Use this skill whenever the user asks for: landing pages, animated components, hero sections, 
  pricing sections, testimonials, marquees, animated buttons, text animations, background effects,
  bento grids, device mockups (Safari/iPhone/Android), SaaS templates, startup templates, 
  portfolio sites, or any modern animated UI component. Also trigger for requests like 
  "make it look like Magic UI", "add shimmer effect", "animated gradient text", "orbiting circles",
  "particles background", or any mention of specific Magic UI components. This skill provides
  150+ components across categories: text animations, buttons, backgrounds, effects, layout,
  device mocks, and complete landing page templates.
---

# Magic UI Clone

A comprehensive library of 150+ animated React components and landing page templates, inspired by Magic UI. Built with React, TypeScript, Tailwind CSS, and Framer Motion.

## Quick Reference

### Output Formats

Claude should adapt output based on context:

1. **Claude Artifacts (.jsx)** - For preview/demo in chat
2. **Downloadable Files** - For Next.js projects
3. **Inline Code** - For simple components user will copy

### Tech Stack Options

Adapt based on user request:
- **Full Stack**: Next.js 15 + React 19 + TypeScript + Tailwind CSS + Framer Motion
- **Simple**: React + Tailwind (no TypeScript, no Motion)
- **Vanilla**: HTML + CSS + JS (maximum compatibility)

---

## Component Catalog

### 📝 Text Animations (20 components)
→ Read `references/text-animations.md` for full implementations

| Component | Description | Use Case |
|-----------|-------------|----------|
| `TypingAnimation` | Typewriter effect | Hero headlines |
| `TextAnimate` | Multiple animation presets | Any text |
| `NumberTicker` | Animated counter | Stats, metrics |
| `AnimatedGradientText` | Moving gradient | CTAs, badges |
| `AnimatedShinyText` | Shimmer effect | Announcements |
| `AuroraText` | Aurora borealis gradient | Headlines |
| `HyperText` | Scramble/decode effect | Tech vibes |
| `MorphingText` | Text morphing | Word transitions |
| `SparklesText` | Sparkle particles | Emphasis |
| `WordRotate` | Rotating words | Dynamic headlines |
| `TextReveal` | Scroll-based reveal | Storytelling |
| `ScrollBasedVelocity` | Speed-based scaling | Parallax |
| `SpinningText` | Circular spinning text | Badges, logos |
| `LineShadowText` | 3D shadow effect | Bold headlines |
| `VideoText` | Video inside text | Creative headers |
| `Text3DFlip` | 3D flip animation | Interactions |
| `TextHighlighter` | Highlight animation | Emphasis |
| `ComicText` | Comic book style | Fun UIs |

### 🔘 Buttons (8 components)
→ Read `references/buttons.md` for full implementations

| Component | Description |
|-----------|-------------|
| `ShimmerButton` | Traveling light shimmer |
| `RainbowButton` | Rainbow gradient border |
| `RippleButton` | Click ripple effect |
| `PulsatingButton` | Pulse animation |
| `ShinyButton` | Shiny hover effect |
| `InteractiveHoverButton` | Slide hover effect |

### 🎨 Backgrounds (12 components)
→ Read `references/backgrounds.md` for full implementations

| Component | Description |
|-----------|-------------|
| `DotPattern` | Dot grid background |
| `GridPattern` | Line grid background |
| `RetroGrid` | Perspective retro grid |
| `FlickeringGrid` | Animated flicker grid |
| `AnimatedGridPattern` | Moving grid lines |
| `InteractiveGridPattern` | Mouse-reactive grid |
| `Ripple` | Expanding ripples |
| `Particles` | Floating particles |
| `HexagonPattern` | Hexagonal tiles |
| `StripedPattern` | Diagonal stripes |
| `LightRays` | Radial light beams |
| `NoiseTexture` | Grain/noise overlay |
| `WarpBackground` | Warped mesh effect |

### ✨ Special Effects (10 components)
→ Read `references/effects.md` for full implementations

| Component | Description |
|-----------|-------------|
| `AnimatedBeam` | Flowing beam lines |
| `BorderBeam` | Border light animation |
| `ShineBorder` | Shine effect on borders |
| `MagicCard` | Spotlight hover card |
| `GlareHover` | Glare effect on hover |
| `Meteors` | Falling meteor streaks |
| `Confetti` | Celebration confetti |
| `CoolMode` | Emoji explosion on click |
| `Backlight` | Glow backlight effect |
| `BlurFade` | Blur + fade entrance |

### 📐 Layout Components (15 components)
→ Read `references/layout.md` for full implementations

| Component | Description |
|-----------|-------------|
| `Marquee` | Infinite scroll (horizontal/vertical/3D) |
| `BentoGrid` | Asymmetric grid layout |
| `Dock` | macOS-style dock |
| `Terminal` | Code terminal display |
| `AnimatedList` | Staggered list animation |
| `Globe` | 3D interactive globe |
| `IconCloud` | Floating icon sphere |
| `OrbitingCircles` | Rotating orbital items |
| `AvatarCircles` | Overlapping avatars |
| `TweetCard` | Twitter/X embed card |
| `FileTree` | File explorer tree |
| `CodeComparison` | Side-by-side code diff |
| `HeroVideoDialog` | Video modal with preview |
| `Lens` | Magnifying lens effect |
| `ScrollProgress` | Page scroll indicator |
| `DottedMap` | Interactive dotted world map |
| `ProgressiveBlur` | Gradient blur fade |

### 📱 Device Mocks (3 components)
→ Read `references/device-mocks.md` for full implementations

| Component | Description |
|-----------|-------------|
| `Safari` | Safari browser frame |
| `IPhone` | iPhone device frame |
| `Android` | Android device frame |

---

## Page Sections (50+ variants)
→ Read `sections/` folder for full implementations

### Headers & Navigation
- Sticky header with blur
- Mobile hamburger menu
- Command palette (⌘K)

### Hero Sections (10+ variants)
→ Read `sections/hero.md`
- Centered with gradient text
- Split with device mockup
- Video background
- Animated particles
- 3D perspective

### Feature Sections (15+ variants)
→ Read `sections/features.md`
- Bento grid layout
- Scroll-triggered slideshow
- Card grid with hover
- Feature comparison table
- Animated beam connections

### Social Proof
- Logo marquee
- Testimonial cards
- Twitter/X feed
- Avatar stack
- Stats counters

### Pricing Sections
→ Read `sections/pricing.md`
- 2-3 column cards
- Toggle monthly/annual
- Feature comparison
- Highlighted recommended

### CTA, FAQ, Footer
→ Read `sections/common.md`

---

## Complete Templates
→ Read `templates/` folder for full implementations

| Template | Best For | Key Sections |
|----------|----------|--------------|
| `SaaS` | Software products | Hero, Features, Pricing, Testimonials |
| `Startup` | New ventures | Hero, Problem/Solution, Team, CTA |
| `Mobile` | App launches | Device mockups, App store badges |
| `Portfolio` | Creatives | Projects grid, Skills, Contact |
| `AI Agent` | AI products | Demo, Capabilities, Integration |
| `DevTool` | Developer tools | Code snippets, API docs, Pricing |
| `CodeForge` | Workflow tools | Workflow viz, Integrations |
| `Changelog` | Product updates | Timeline, Version history |
| `Blog` | Content sites | MDX support, Categories |

---

## Implementation Guide

### For Claude Artifacts (Preview in Chat)

When creating artifacts, include all dependencies inline:

```jsx
// Single-file artifact with Tailwind + inline animations
export default function Component() {
  return (
    <div className="relative">
      {/* Use Tailwind classes + CSS custom properties */}
      <style>{`
        @keyframes shimmer {
          0% { transform: translateX(-100%); }
          100% { transform: translateX(100%); }
        }
      `}</style>
      {/* Component JSX */}
    </div>
  )
}
```

### For Next.js Projects

1. Create component in `components/magicui/`
2. Add required CSS to `globals.css` or `tailwind.config.ts`
3. Import and use

### CSS Requirements

Many components need these keyframes in your CSS:

```css
@keyframes marquee {
  from { transform: translateX(0); }
  to { transform: translateX(calc(-100% - var(--gap))); }
}

@keyframes marquee-vertical {
  from { transform: translateY(0); }
  to { transform: translateY(calc(-100% - var(--gap))); }
}

@keyframes shimmer {
  0% { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}

@keyframes pulse-border {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}
```

---

## Utility: cn() helper

All components use this utility for conditional classes:

```typescript
import { clsx, type ClassValue } from "clsx"
import { twMerge } from "tailwind-merge"

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}
```

For artifacts without dependencies, use:
```javascript
const cn = (...classes) => classes.filter(Boolean).join(' ')
```

---

## Decision Tree

When user requests a component/template:

1. **Identify component type** from catalog above
2. **Read the relevant reference file** for implementation details
3. **Determine output format**:
   - Quick demo → Artifact
   - Production use → Downloadable files
   - Learning → Inline code with explanation
4. **Adapt tech stack** to user's stated preferences
5. **Include all required CSS/keyframes** inline or note them

---

## Reference File Index

Read these files for detailed implementations:

### Component References (7 files, 55+ components)
- `references/text-animations.md` - 12 text animations (TypingAnimation, NumberTicker, WordRotate, AnimatedGradientText, SparklesText, etc.)
- `references/buttons.md` - 6 animated buttons (Shimmer, Rainbow, Ripple, Pulsating, Shiny, InteractiveHover)
- `references/backgrounds.md` - 7 background effects (DotPattern, GridPattern, RetroGrid, FlickeringGrid, Ripple, Particles, AnimatedGridPattern)
- `references/effects.md` - 8 special effects (AnimatedBeam, BorderBeam, ShineBorder, MagicCard, Meteors, Confetti, BlurFade, GlareHover)
- `references/layout.md` - 7 layout components (Marquee, BentoGrid, Dock, AnimatedList, OrbitingCircles, AvatarCircles, Terminal)
- `references/advanced-components.md` - 9 advanced (Globe, IconCloud, Lens, FileTree, HeroVideoDialog, ScrollProgress, CodeComparison, NeonGradientCard, CoolMode)
- `references/device-mocks.md` - 6 device frames (Safari, Safari Dark, iPhone, iPhone SVG, Android, Laptop)

### Section References (5 files, 25+ section variants)
- `sections/hero.md` - 6 hero variants (Centered, Split, Video, ProductHunt, Dashboard, MobileApp)
- `sections/features.md` - 6 feature variants (BentoGrid, IconGrid, Alternating, Cards, Tabs, Comparison)
- `sections/pricing.md` - 4 pricing variants (ThreeColumn, Toggle, ComparisonTable, LifetimeDeal)
- `sections/testimonials.md` - 5 testimonial variants (DoubleMarquee, Grid, Video, TweetWall, LogoQuote)
- `sections/common.md` - 6 common sections (Header, Footer, CTA, FAQ, Stats, FeatureGrid)

### Complete Templates (4 files, full landing pages)
- `templates/saas.md` - Full SaaS landing page (9 sections, artifact-ready)
- `templates/startup.md` - Startup launch page (Problem/Solution focus, investors section, artifact-ready)
- `templates/mobile.md` - Mobile app landing (iOS/Android badges, phone mockups, app reviews, artifact-ready)
- `templates/portfolio.md` - Personal/agency portfolio (projects showcase, services, about, contact, artifact-ready)

**Total: 80+ components + 27 section variants + 4 complete templates**
