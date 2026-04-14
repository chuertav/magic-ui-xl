# ✨ Magic UI XL v3.0

> A comprehensive Claude skill with 80+ animated React components, 27 section variants, and 4 complete landing page templates. Open source and free to use.

![Version](https://img.shields.io/badge/version-3.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Components](https://img.shields.io/badge/components-80%2B-purple)

---

## ☕ Support This Project

If this skill saves you time, consider buying me a coffee! Every $1 helps keep this project maintained and growing.

<a href="https://buymeacoffee.com/magicuixl" target="_blank">
  <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" height="50">
</a>

[![PayPal](https://img.shields.io/badge/PayPal-Donate_$1-blue?logo=paypal)](https://paypal.me/magicuixl)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-Support-ff5f5f?logo=ko-fi)](https://ko-fi.com/magicuixl)

**Other ways to support:**
- ⭐ Star this repo
- 🐛 Report bugs
- 🔀 Submit PRs
- 📣 Share with friends

---

## 🎯 What is this?

Magic UI XL is a **Claude skill** that enables Claude to generate beautiful, production-ready React components and landing pages inspired by [Magic UI](https://magicui.design). 

Instead of writing boilerplate code, just ask Claude:
- *"Create a SaaS landing page with animated hero and pricing"*
- *"Build a portfolio site with project showcase"*
- *"Add a shimmer button with rainbow border effect"*

Claude will generate complete, working code using the patterns in this skill.

## 📦 What's Included

### Component References (55+ components)

| File | Components | Examples |
|------|------------|----------|
| `text-animations.md` | 12 | TypingAnimation, WordRotate, NumberTicker, SparklesText, AnimatedGradientText |
| `buttons.md` | 6 | ShimmerButton, RainbowButton, RippleButton, PulsatingButton |
| `backgrounds.md` | 7 | DotPattern, GridPattern, RetroGrid, Particles, FlickeringGrid |
| `effects.md` | 8 | BorderBeam, AnimatedBeam, MagicCard, Meteors, Confetti |
| `layout.md` | 7 | Marquee, BentoGrid, Dock, AnimatedList, OrbitingCircles |
| `advanced-components.md` | 9 | Globe, IconCloud, Lens, FileTree, HeroVideoDialog, NeonGradientCard |
| `device-mocks.md` | 6 | Safari, iPhone, Android, Laptop frames |

### Section Variants (27 variants)

| File | Variants | Styles |
|------|----------|--------|
| `hero.md` | 6 | Centered, Split, Video, ProductHunt, Dashboard, MobileApp |
| `features.md` | 6 | BentoGrid, IconGrid, Alternating, Cards, Tabs, Comparison |
| `pricing.md` | 4 | ThreeColumn, Toggle, ComparisonTable, LifetimeDeal |
| `testimonials.md` | 5 | DoubleMarquee, Grid, Video, TweetWall, LogoQuote |
| `common.md` | 6 | Header, Footer, CTA, FAQ, Stats, FeatureGrid |

### Complete Templates (4 landing pages)

| Template | Best For | Sections |
|----------|----------|----------|
| `saas.md` | SaaS products | Hero, LogoCloud, Features, Testimonials, Pricing, FAQ, CTA |
| `startup.md` | Startup launches | Problem/Solution, HowItWorks, Team, Investors |
| `mobile.md` | Mobile apps | AppStore badges, Phone mockups, Reviews, Download CTA |
| `portfolio.md` | Personal/Agency | Projects showcase, Services, About, Contact |

## 🚀 Installation

### For Claude.ai (Recommended)

1. Download the skill:
```bash
git clone https://github.com/YOUR_USERNAME/magic-ui-xl.git
```

2. Copy to your Claude skills directory:
```bash
# For user skills (personal use)
cp -r magic-ui-xl /path/to/skills/user/

# For project skills (team use)
cp -r magic-ui-xl /path/to/your-project/skills/
```

3. The skill auto-triggers when you ask for:
   - Landing pages
   - Animated components
   - Magic UI-style effects
   - Any component mentioned in the catalog

### Manual Usage

You can also just reference the files directly in your prompts:
```
Read magic-ui-xl/references/buttons.md and create a ShimmerButton
```

## 💬 Example Prompts

### Landing Pages
```
"Create a SaaS landing page for my AI writing tool"
"Build a mobile app landing page with iPhone mockup"
"Make a portfolio site showcasing my web development projects"
"Design a startup landing page with problem/solution sections"
```

### Components
```
"Add a hero section with WordRotate animated headline"
"Create a pricing section with monthly/annual toggle"
"Build a testimonials section with double marquee like Magic UI"
"Add a BentoGrid features section with hover effects"
```

### Specific Effects
```
"Add BorderBeam effect to my pricing card"
"Create an animated gradient text headline"
"Add particles background to my hero section"
"Make a button with shimmer animation"
```

## 📁 File Structure

```
magic-ui-xl/
├── SKILL.md                 # Main entry point + component catalog
├── README.md                # This file
├── LICENSE                  # MIT License
├── CHANGELOG.md             # Version history
│
├── references/              # Individual component implementations
│   ├── text-animations.md   # Text animation components
│   ├── buttons.md           # Button variants
│   ├── backgrounds.md       # Background effects
│   ├── effects.md           # Special effects
│   ├── layout.md            # Layout components
│   ├── advanced-components.md # Complex components
│   └── device-mocks.md      # Device frame components
│
├── sections/                # Reusable section variants
│   ├── hero.md              # Hero section variants
│   ├── features.md          # Feature section variants
│   ├── pricing.md           # Pricing section variants
│   ├── testimonials.md      # Testimonial variants
│   └── common.md            # Header, Footer, CTA, FAQ
│
└── templates/               # Complete landing page templates
    ├── saas.md              # SaaS template
    ├── startup.md           # Startup template
    ├── mobile.md            # Mobile app template
    └── portfolio.md         # Portfolio template
```

## 🛠 Tech Stack Support

The skill generates code for:

| Stack | When to Use |
|-------|-------------|
| **React + TypeScript + Tailwind + Framer Motion** | Production Next.js projects |
| **React + Tailwind** | Simpler React projects |
| **Claude Artifacts (JSX)** | Quick demos in chat |
| **HTML + CSS + JS** | Maximum compatibility |

Just specify your preference:
```
"Create a landing page using vanilla HTML/CSS"
"Build this component for my Next.js 15 project with TypeScript"
```

## 🎨 Design Philosophy

Components follow these principles:
- **Dark mode ready** - All components work in light/dark themes
- **Responsive** - Mobile-first, works on all screen sizes
- **Accessible** - Semantic HTML, keyboard navigation
- **Performant** - Optimized animations, lazy loading ready
- **Customizable** - CSS variables for easy theming

## 📝 Required Dependencies

For full functionality in your project:

```json
{
  "dependencies": {
    "react": "^18.0.0",
    "tailwindcss": "^3.4.0",
    "framer-motion": "^11.0.0",
    "lucide-react": "^0.300.0",
    "clsx": "^2.0.0",
    "tailwind-merge": "^2.0.0"
  }
}
```

Optional for specific components:
- `cobe` - For Globe component
- `react-icon-cloud` - For IconCloud component

## 🔧 Utility Function

Most components use this helper:

```typescript
// lib/utils.ts
import { clsx, type ClassValue } from "clsx"
import { twMerge } from "tailwind-merge"

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}
```

## 🤝 Contributing

Contributions welcome! Feel free to:
- Add new components
- Improve existing implementations
- Add more templates
- Fix bugs or typos

## 📄 License

MIT License - free for personal and commercial use.

## 🙏 Credits

- Inspired by [Magic UI](https://magicui.design)
- Built for use with [Claude](https://claude.ai) by Anthropic
- Created by the community

---

**Made with ❤️ for developers who want beautiful UIs without the hassle**
