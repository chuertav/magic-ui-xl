# Features Sections Reference

Multiple feature section variants for showcasing product capabilities.

---

## 1. Features - BentoGrid Layout

Modern asymmetric grid layout (like Apple, Linear).

```tsx
import { BentoGrid, BentoCard } from "@/components/magicui/bento-grid"
import { BorderBeam } from "@/components/magicui/border-beam"
import { Globe, Zap, Shield, Sparkles, Code, Users } from "lucide-react"

const features = [
  {
    name: "Lightning Fast",
    description: "Built on edge infrastructure for sub-50ms response times globally.",
    icon: Zap,
    className: "md:col-span-2",
    background: (
      <div className="absolute inset-0 bg-gradient-to-br from-yellow-100 to-orange-100 dark:from-yellow-900/20 dark:to-orange-900/20" />
    ),
  },
  {
    name: "Secure by Default",
    description: "Enterprise-grade security with SOC 2 Type II compliance.",
    icon: Shield,
    className: "md:col-span-1",
    background: (
      <div className="absolute inset-0 bg-gradient-to-br from-green-100 to-emerald-100 dark:from-green-900/20 dark:to-emerald-900/20" />
    ),
  },
  {
    name: "Global Scale",
    description: "Deploy to 30+ regions worldwide with automatic failover.",
    icon: Globe,
    className: "md:col-span-1",
    background: (
      <div className="absolute inset-0 bg-gradient-to-br from-blue-100 to-cyan-100 dark:from-blue-900/20 dark:to-cyan-900/20" />
    ),
  },
  {
    name: "AI Powered",
    description: "Smart automations that learn and adapt to your workflow.",
    icon: Sparkles,
    className: "md:col-span-2",
    background: (
      <div className="absolute inset-0 bg-gradient-to-br from-purple-100 to-pink-100 dark:from-purple-900/20 dark:to-pink-900/20" />
    ),
  },
]

export function FeaturesBento() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Everything you need to ship faster
          </h2>
          <p className="text-lg text-muted-foreground max-w-2xl mx-auto">
            A complete toolkit designed for modern development teams
          </p>
        </div>

        <BentoGrid className="max-w-5xl mx-auto">
          {features.map((feature) => (
            <BentoCard
              key={feature.name}
              name={feature.name}
              description={feature.description}
              Icon={feature.icon}
              className={feature.className}
              background={feature.background}
            />
          ))}
        </BentoGrid>
      </div>
    </section>
  )
}
```

---

## 2. Features - Icon Grid (3x2)

Simple centered grid with icons.

```tsx
import { Zap, Shield, Globe, Sparkles, Code, Users } from "lucide-react"

const features = [
  { icon: Zap, title: "Lightning Fast", description: "Sub-50ms response times with edge computing." },
  { icon: Shield, title: "Enterprise Security", description: "SOC 2 Type II certified with encryption at rest." },
  { icon: Globe, title: "Global CDN", description: "Content delivered from 200+ edge locations." },
  { icon: Sparkles, title: "AI Automation", description: "Smart workflows that learn your patterns." },
  { icon: Code, title: "Developer First", description: "Beautiful APIs and comprehensive SDKs." },
  { icon: Users, title: "Team Collaboration", description: "Real-time editing with conflict resolution." },
]

export function FeaturesIconGrid() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Powerful features for modern teams
          </h2>
          <p className="text-lg text-muted-foreground">
            Everything you need to build, deploy, and scale
          </p>
        </div>

        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-5xl mx-auto">
          {features.map((feature) => (
            <div key={feature.title} className="text-center p-6">
              <div className="w-14 h-14 rounded-2xl bg-primary/10 flex items-center justify-center mx-auto mb-4">
                <feature.icon className="h-7 w-7 text-primary" />
              </div>
              <h3 className="text-xl font-semibold mb-2">{feature.title}</h3>
              <p className="text-muted-foreground">{feature.description}</p>
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## 3. Features - Alternating Layout

Feature + image alternating sides (like Stripe).

```tsx
import { Safari } from "@/components/magicui/safari"
import { BorderBeam } from "@/components/magicui/border-beam"

const features = [
  {
    title: "Real-time Collaboration",
    description: "Work together seamlessly with your team. See changes instantly, resolve conflicts automatically, and never lose work.",
    bullets: ["Multiplayer cursors", "Version history", "Comments & threads"],
    image: "/features/collaboration.png",
  },
  {
    title: "Powerful Automations",
    description: "Build complex workflows without code. Our visual builder makes it easy to automate repetitive tasks.",
    bullets: ["Visual workflow builder", "100+ integrations", "Custom triggers"],
    image: "/features/automations.png",
    reverse: true,
  },
  {
    title: "Advanced Analytics",
    description: "Understand your data with beautiful dashboards. Track metrics that matter and make data-driven decisions.",
    bullets: ["Custom dashboards", "Real-time metrics", "Export reports"],
    image: "/features/analytics.png",
  },
]

export function FeaturesAlternating() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="text-center mb-20">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Built for the way you work
          </h2>
          <p className="text-lg text-muted-foreground">
            Features that adapt to your workflow, not the other way around
          </p>
        </div>

        <div className="space-y-32 max-w-6xl mx-auto">
          {features.map((feature, i) => (
            <div
              key={feature.title}
              className={`grid lg:grid-cols-2 gap-12 items-center ${
                feature.reverse ? "lg:flex-row-reverse" : ""
              }`}
            >
              {/* Image */}
              <div className={`${feature.reverse ? "lg:order-2" : ""}`}>
                <div className="relative rounded-xl overflow-hidden shadow-2xl">
                  <BorderBeam size={200} duration={10} />
                  <Safari url="app.example.com" src={feature.image} />
                </div>
              </div>

              {/* Content */}
              <div className={feature.reverse ? "lg:order-1" : ""}>
                <span className="text-primary font-medium">Feature {i + 1}</span>
                <h3 className="text-3xl font-bold mt-2 mb-4">{feature.title}</h3>
                <p className="text-lg text-muted-foreground mb-6">
                  {feature.description}
                </p>
                <ul className="space-y-3">
                  {feature.bullets.map((bullet) => (
                    <li key={bullet} className="flex items-center gap-3">
                      <span className="w-6 h-6 rounded-full bg-primary/10 text-primary flex items-center justify-center text-sm">
                        ✓
                      </span>
                      <span>{bullet}</span>
                    </li>
                  ))}
                </ul>
              </div>
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## 4. Features - Cards with Hover Effects

Cards with MagicCard hover spotlight effect.

```tsx
import { MagicCard } from "@/components/magicui/magic-card"
import { Zap, Shield, Globe, Sparkles } from "lucide-react"

const features = [
  { icon: Zap, title: "Instant Deploy", description: "Push to git and your site is live in seconds. Zero configuration required." },
  { icon: Shield, title: "Built-in Security", description: "Automatic SSL, DDoS protection, and firewall rules out of the box." },
  { icon: Globe, title: "Edge Network", description: "Your content served from the location closest to your users." },
  { icon: Sparkles, title: "Smart Caching", description: "Intelligent caching that knows when to refresh automatically." },
]

export function FeaturesCards() {
  return (
    <section className="py-24 bg-muted/30">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Why teams choose us
          </h2>
          <p className="text-lg text-muted-foreground">
            The features that set us apart
          </p>
        </div>

        <div className="grid md:grid-cols-2 gap-6 max-w-4xl mx-auto">
          {features.map((feature) => (
            <MagicCard key={feature.title} className="p-8">
              <feature.icon className="h-10 w-10 text-primary mb-4" />
              <h3 className="text-xl font-bold mb-2">{feature.title}</h3>
              <p className="text-muted-foreground">{feature.description}</p>
            </MagicCard>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## 5. Features - Tabs with Preview

Tabbed feature showcase with live preview.

```tsx
"use client"
import { useState } from "react"
import { cn } from "@/lib/utils"
import { Safari } from "@/components/magicui/safari"

const tabs = [
  { id: "editor", label: "Code Editor", image: "/features/editor.png", description: "Write code with AI-powered autocomplete and intelligent suggestions." },
  { id: "preview", label: "Live Preview", image: "/features/preview.png", description: "See your changes instantly with hot reload and error overlay." },
  { id: "deploy", label: "One-Click Deploy", image: "/features/deploy.png", description: "Deploy to production with a single click. Automatic rollbacks included." },
  { id: "analytics", label: "Analytics", image: "/features/analytics.png", description: "Track performance, errors, and user behavior in real-time." },
]

export function FeaturesTabs() {
  const [activeTab, setActiveTab] = useState(tabs[0].id)
  const activeFeature = tabs.find(t => t.id === activeTab)!

  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="text-center mb-12">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            See it in action
          </h2>
          <p className="text-lg text-muted-foreground">
            Explore our key features
          </p>
        </div>

        {/* Tabs */}
        <div className="flex flex-wrap justify-center gap-2 mb-8">
          {tabs.map((tab) => (
            <button
              key={tab.id}
              onClick={() => setActiveTab(tab.id)}
              className={cn(
                "px-4 py-2 rounded-full text-sm font-medium transition-colors",
                activeTab === tab.id
                  ? "bg-primary text-primary-foreground"
                  : "bg-muted hover:bg-muted/80"
              )}
            >
              {tab.label}
            </button>
          ))}
        </div>

        {/* Content */}
        <div className="max-w-4xl mx-auto">
          <div className="rounded-xl overflow-hidden shadow-2xl mb-6">
            <Safari url="app.example.com" src={activeFeature.image} />
          </div>
          <p className="text-center text-lg text-muted-foreground">
            {activeFeature.description}
          </p>
        </div>
      </div>
    </section>
  )
}
```

---

## 6. Features - Comparison (Us vs Them)

Side-by-side comparison with competitors.

```tsx
import { Check, X } from "lucide-react"

const comparisons = [
  { feature: "Real-time collaboration", us: true, them: false },
  { feature: "Unlimited projects", us: true, them: false },
  { feature: "Custom domains", us: true, them: "Paid add-on" },
  { feature: "API access", us: true, them: true },
  { feature: "24/7 support", us: true, them: false },
  { feature: "SSO/SAML", us: true, them: "Enterprise only" },
  { feature: "99.99% SLA", us: true, them: "99.9%" },
  { feature: "Data export", us: true, them: true },
]

export function FeaturesComparison() {
  return (
    <section className="py-24 bg-muted/30">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Why switch to us?
          </h2>
          <p className="text-lg text-muted-foreground">
            See how we compare to the competition
          </p>
        </div>

        <div className="max-w-2xl mx-auto">
          <div className="grid grid-cols-3 gap-4 mb-4 text-center font-semibold">
            <div>Feature</div>
            <div className="text-primary">Us</div>
            <div className="text-muted-foreground">Others</div>
          </div>

          {comparisons.map((row) => (
            <div
              key={row.feature}
              className="grid grid-cols-3 gap-4 py-4 border-b items-center"
            >
              <div className="font-medium">{row.feature}</div>
              <div className="text-center">
                <ComparisonValue value={row.us} positive />
              </div>
              <div className="text-center">
                <ComparisonValue value={row.them} />
              </div>
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}

function ComparisonValue({ value, positive }: { value: boolean | string; positive?: boolean }) {
  if (value === true) {
    return <Check className={cn("h-5 w-5 mx-auto", positive ? "text-green-500" : "text-muted-foreground")} />
  }
  if (value === false) {
    return <X className="h-5 w-5 mx-auto text-red-500" />
  }
  return <span className="text-sm text-muted-foreground">{value}</span>
}
```

---

## Artifact-Ready Features Section

```jsx
export default function FeaturesDemo() {
  const features = [
    { icon: "⚡", title: "Lightning Fast", desc: "Sub-50ms response times globally", color: "from-yellow-400 to-orange-500" },
    { icon: "🔒", title: "Secure", desc: "Enterprise-grade security built in", color: "from-green-400 to-emerald-500" },
    { icon: "🌍", title: "Global Scale", desc: "30+ regions worldwide", color: "from-blue-400 to-cyan-500" },
    { icon: "✨", title: "AI Powered", desc: "Smart automations that learn", color: "from-purple-400 to-pink-500" },
    { icon: "💻", title: "Developer First", desc: "Beautiful APIs and SDKs", color: "from-gray-400 to-slate-500" },
    { icon: "👥", title: "Team Ready", desc: "Real-time collaboration", color: "from-red-400 to-rose-500" },
  ]

  return (
    <div className="min-h-screen bg-gray-950 text-white py-24 px-4">
      <div className="max-w-6xl mx-auto">
        <div className="text-center mb-16">
          <h2 className="text-4xl font-bold mb-4">Everything you need</h2>
          <p className="text-gray-400 text-lg">Powerful features for modern teams</p>
        </div>

        {/* Bento Grid */}
        <div className="grid md:grid-cols-3 gap-4">
          {features.map((f, i) => (
            <div
              key={f.title}
              className={`relative group rounded-2xl border border-gray-800 bg-gray-900 p-6 overflow-hidden transition-all hover:border-gray-700 ${
                i === 0 || i === 3 ? 'md:col-span-2' : ''
              }`}
            >
              {/* Gradient background on hover */}
              <div className={`absolute inset-0 bg-gradient-to-br ${f.color} opacity-0 group-hover:opacity-10 transition-opacity`} />
              
              <div className="relative z-10">
                <span className="text-4xl mb-4 block">{f.icon}</span>
                <h3 className="text-xl font-bold mb-2">{f.title}</h3>
                <p className="text-gray-400">{f.desc}</p>
              </div>

              {/* Spotlight effect */}
              <div
                className="pointer-events-none absolute -inset-px opacity-0 group-hover:opacity-100 transition-opacity"
                style={{
                  background: 'radial-gradient(600px circle at var(--mouse-x, 50%) var(--mouse-y, 50%), rgba(255,255,255,0.06), transparent 40%)',
                }}
              />
            </div>
          ))}
        </div>

        {/* Simple Grid Alternative */}
        <div className="mt-24">
          <h3 className="text-2xl font-bold text-center mb-12">Or as a simple grid</h3>
          <div className="grid md:grid-cols-3 gap-8">
            {features.map((f) => (
              <div key={f.title} className="text-center">
                <div className={`w-16 h-16 rounded-2xl bg-gradient-to-br ${f.color} flex items-center justify-center mx-auto mb-4 text-2xl`}>
                  {f.icon}
                </div>
                <h4 className="font-bold text-lg mb-2">{f.title}</h4>
                <p className="text-gray-400 text-sm">{f.desc}</p>
              </div>
            ))}
          </div>
        </div>
      </div>
    </div>
  )
}
```
