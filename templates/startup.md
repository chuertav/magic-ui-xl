# Startup Landing Page Template

Complete template optimized for startup launches and fundraising.

---

## Page Structure

```tsx
// Startup Landing Page - Key Sections
// 1. Header (sticky, minimal)
// 2. Hero (problem statement + solution)
// 3. Logo Cloud (investors/partners)
// 4. Problem Section (pain points)
// 5. Solution Section (your product)
// 6. Features (key differentiators)
// 7. How It Works (3 steps)
// 8. Testimonials
// 9. Team Section
// 10. Pricing/CTA
// 11. FAQ
// 12. Footer
```

---

## Hero Section - Problem/Solution Focus

```tsx
import { WordRotate } from "@/components/magicui/word-rotate"
import { ShimmerButton } from "@/components/magicui/shimmer-button"
import { RetroGrid } from "@/components/magicui/retro-grid"
import { AvatarCircles } from "@/components/magicui/avatar-circles"

export function StartupHero() {
  return (
    <section className="relative min-h-screen flex items-center pt-20 overflow-hidden">
      <RetroGrid className="opacity-30" />
      
      <div className="container mx-auto px-4 relative z-10">
        <div className="max-w-4xl mx-auto text-center">
          {/* Funding Badge */}
          <div className="inline-flex items-center gap-2 px-4 py-2 rounded-full border bg-green-50 text-green-700 text-sm mb-8">
            <span>🚀</span>
            <span className="font-medium">Backed by Y Combinator</span>
          </div>

          {/* Main Headline */}
          <h1 className="text-4xl md:text-6xl lg:text-7xl font-bold mb-6 leading-tight">
            Stop wasting time on{" "}
            <WordRotate
              words={["spreadsheets", "meetings", "emails", "busywork"]}
              className="text-primary"
            />
          </h1>

          <p className="text-xl text-muted-foreground mb-8 max-w-2xl mx-auto">
            The all-in-one platform that helps startups move 10x faster.
            Automate the boring stuff and focus on what matters.
          </p>

          {/* CTAs */}
          <div className="flex flex-col sm:flex-row gap-4 justify-center mb-8">
            <ShimmerButton className="h-14 px-8">
              <span className="font-semibold text-lg">Start Free Trial</span>
            </ShimmerButton>
            <button className="h-14 px-8 border rounded-full font-semibold text-lg hover:bg-muted transition">
              Book a Demo →
            </button>
          </div>

          {/* Social Proof */}
          <div className="flex items-center justify-center gap-4">
            <AvatarCircles
              avatarUrls={Array.from({ length: 5 }, (_, i) => `https://avatar.vercel.sh/${i}`)}
            />
            <div className="text-left">
              <div className="font-semibold">500+ teams</div>
              <div className="text-sm text-muted-foreground">already shipping faster</div>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## Problem Section

```tsx
import { MagicCard } from "@/components/magicui/magic-card"

const problems = [
  {
    icon: "😤",
    title: "Context switching kills productivity",
    description: "Your team uses 10+ tools. They spend more time switching than working.",
    stat: "2.5 hours",
    statLabel: "lost per day per person",
  },
  {
    icon: "📊",
    title: "No single source of truth",
    description: "Information scattered across Slack, email, docs. Nothing is ever up to date.",
    stat: "40%",
    statLabel: "of time spent searching",
  },
  {
    icon: "🔥",
    title: "Burnout from busywork",
    description: "Your best people are drowning in status updates and admin tasks.",
    stat: "60%",
    statLabel: "time on non-core work",
  },
]

export function ProblemSection() {
  return (
    <section className="py-24 bg-muted/30">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Sound familiar?
          </h2>
          <p className="text-lg text-muted-foreground">
            Every startup faces these challenges
          </p>
        </div>

        <div className="grid md:grid-cols-3 gap-6 max-w-5xl mx-auto">
          {problems.map((problem) => (
            <MagicCard key={problem.title} className="p-6">
              <span className="text-4xl mb-4 block">{problem.icon}</span>
              <h3 className="text-xl font-bold mb-2">{problem.title}</h3>
              <p className="text-muted-foreground mb-4">{problem.description}</p>
              <div className="pt-4 border-t">
                <div className="text-3xl font-bold text-red-500">{problem.stat}</div>
                <div className="text-sm text-muted-foreground">{problem.statLabel}</div>
              </div>
            </MagicCard>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## Solution Section

```tsx
import { Safari } from "@/components/magicui/safari"
import { BorderBeam } from "@/components/magicui/border-beam"
import { AnimatedBeam } from "@/components/magicui/animated-beam"

export function SolutionSection() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="grid lg:grid-cols-2 gap-12 items-center">
          {/* Content */}
          <div>
            <div className="inline-block px-3 py-1 rounded-full bg-primary/10 text-primary text-sm font-medium mb-6">
              The Solution
            </div>
            
            <h2 className="text-3xl md:text-4xl font-bold mb-6">
              One platform to replace them all
            </h2>
            
            <p className="text-lg text-muted-foreground mb-8">
              We've combined project management, docs, communication, and automation
              into a single unified workspace. No more tool sprawl.
            </p>

            <ul className="space-y-4">
              {[
                "Replace 10 tools with 1",
                "AI-powered automation",
                "Real-time collaboration",
                "Works where you work (Slack, email, etc.)",
              ].map((item) => (
                <li key={item} className="flex items-center gap-3">
                  <span className="w-6 h-6 rounded-full bg-green-100 text-green-600 flex items-center justify-center text-sm">
                    ✓
                  </span>
                  <span>{item}</span>
                </li>
              ))}
            </ul>
          </div>

          {/* Demo */}
          <div className="relative">
            <div className="relative rounded-xl shadow-2xl overflow-hidden">
              <BorderBeam size={300} duration={10} />
              <Safari url="app.startup.com" src="/dashboard.png" />
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## How It Works - 3 Steps

```tsx
import { NumberTicker } from "@/components/magicui/number-ticker"

const steps = [
  {
    number: 1,
    title: "Connect your tools",
    description: "Link your existing apps in one click. We support 100+ integrations.",
    icon: "🔗",
  },
  {
    number: 2,
    title: "Set up automations",
    description: "Use our AI to create workflows in plain English. No coding required.",
    icon: "⚡",
  },
  {
    number: 3,
    title: "Watch productivity soar",
    description: "Your team gets hours back every week. Focus on what matters.",
    icon: "🚀",
  },
]

export function HowItWorks() {
  return (
    <section className="py-24 bg-muted/30">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Get started in minutes
          </h2>
          <p className="text-lg text-muted-foreground">
            Three simple steps to transform how your team works
          </p>
        </div>

        <div className="grid md:grid-cols-3 gap-8 max-w-4xl mx-auto">
          {steps.map((step, i) => (
            <div key={step.number} className="relative text-center">
              {/* Connector Line */}
              {i < steps.length - 1 && (
                <div className="hidden md:block absolute top-8 left-[60%] w-[80%] h-[2px] bg-border" />
              )}
              
              {/* Step Number */}
              <div className="w-16 h-16 rounded-full bg-primary text-primary-foreground text-2xl font-bold flex items-center justify-center mx-auto mb-4 relative z-10">
                {step.number}
              </div>
              
              <span className="text-4xl mb-4 block">{step.icon}</span>
              <h3 className="text-xl font-bold mb-2">{step.title}</h3>
              <p className="text-muted-foreground">{step.description}</p>
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## Team Section

```tsx
const team = [
  { name: "Sarah Chen", role: "CEO & Co-founder", bio: "Ex-Stripe, Stanford CS", avatar: "https://avatar.vercel.sh/sarah" },
  { name: "Mike Johnson", role: "CTO & Co-founder", bio: "Ex-Google, MIT", avatar: "https://avatar.vercel.sh/mike" },
  { name: "Emily Rodriguez", role: "Head of Product", bio: "Ex-Notion, Berkeley", avatar: "https://avatar.vercel.sh/emily" },
  { name: "David Kim", role: "Head of Engineering", bio: "Ex-Meta, CMU", avatar: "https://avatar.vercel.sh/david" },
]

export function TeamSection() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Built by operators, for operators
          </h2>
          <p className="text-lg text-muted-foreground">
            Our team has scaled companies from 0 to IPO
          </p>
        </div>

        <div className="grid md:grid-cols-4 gap-8 max-w-4xl mx-auto">
          {team.map((person) => (
            <div key={person.name} className="text-center">
              <img
                src={person.avatar}
                alt={person.name}
                className="w-24 h-24 rounded-full mx-auto mb-4 border-4 border-background shadow-lg"
              />
              <h3 className="font-bold">{person.name}</h3>
              <p className="text-sm text-primary mb-1">{person.role}</p>
              <p className="text-sm text-muted-foreground">{person.bio}</p>
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## Investor/Backer Logos

```tsx
import { Marquee } from "@/components/magicui/marquee"

export function InvestorLogos() {
  const investors = [
    "Y Combinator", "Sequoia", "a16z", "Accel", "Index", "Founders Fund"
  ]

  return (
    <section className="py-12 border-y">
      <div className="container mx-auto px-4">
        <p className="text-center text-sm text-muted-foreground mb-6">
          BACKED BY THE BEST
        </p>
        <Marquee pauseOnHover className="[--duration:30s]">
          {investors.map((name) => (
            <span key={name} className="mx-8 text-2xl font-bold text-muted-foreground/50 hover:text-muted-foreground transition">
              {name}
            </span>
          ))}
        </Marquee>
      </div>
    </section>
  )
}
```

---

## Complete Startup Template (Artifact-Ready)

```jsx
export default function StartupLanding() {
  const [wordIndex, setWordIndex] = React.useState(0)
  const words = ["spreadsheets", "meetings", "busywork", "chaos"]

  React.useEffect(() => {
    const interval = setInterval(() => setWordIndex(i => (i + 1) % words.length), 2500)
    return () => clearInterval(interval)
  }, [])

  return (
    <div className="min-h-screen bg-white">
      <style>{`
        @keyframes grid-scroll { 0% { transform: translateY(-50%); } 100% { transform: translateY(0); } }
        @keyframes word-swap { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
      `}</style>

      {/* Header */}
      <header className="fixed top-0 z-50 w-full bg-white/80 backdrop-blur-lg border-b">
        <div className="max-w-6xl mx-auto px-4 h-16 flex items-center justify-between">
          <span className="text-xl font-bold">🚀 StartupKit</span>
          <nav className="hidden md:flex gap-8 text-sm text-gray-600">
            <a href="#">Features</a>
            <a href="#">Pricing</a>
            <a href="#">About</a>
          </nav>
          <button className="px-4 py-2 bg-black text-white text-sm rounded-full">Get Started</button>
        </div>
      </header>

      {/* Hero */}
      <section className="pt-32 pb-20 px-4 relative overflow-hidden">
        <div className="absolute inset-0 opacity-10" style={{ perspective: '200px' }}>
          <div style={{ transform: 'rotateX(65deg)', position: 'absolute', inset: 0 }}>
            <div style={{
              backgroundImage: 'linear-gradient(to right, #0001 1px, transparent 0), linear-gradient(to bottom, #0001 1px, transparent 0)',
              backgroundSize: '50px 50px',
              width: '200%', height: '200%',
              animation: 'grid-scroll 20s linear infinite',
            }} />
          </div>
        </div>

        <div className="max-w-4xl mx-auto text-center relative z-10">
          <div className="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-green-50 text-green-700 text-sm mb-8">
            🎉 Backed by Y Combinator
          </div>

          <h1 className="text-5xl md:text-7xl font-bold mb-6">
            Stop wasting time on{" "}
            <span key={wordIndex} className="text-purple-600 inline-block" style={{ animation: 'word-swap 0.3s ease-out' }}>
              {words[wordIndex]}
            </span>
          </h1>

          <p className="text-xl text-gray-600 mb-10 max-w-2xl mx-auto">
            The all-in-one platform that helps startups move 10x faster.
          </p>

          <div className="flex gap-4 justify-center mb-8">
            <button className="h-14 px-8 bg-black text-white rounded-full font-semibold">Start Free Trial</button>
            <button className="h-14 px-8 border rounded-full font-semibold">Book Demo →</button>
          </div>

          <div className="flex items-center justify-center gap-3">
            <div className="flex -space-x-2">
              {[1,2,3,4,5].map(i => (
                <div key={i} className="w-8 h-8 rounded-full bg-gradient-to-br from-purple-400 to-pink-400 border-2 border-white" />
              ))}
            </div>
            <span className="text-sm text-gray-600">500+ teams shipping faster</span>
          </div>
        </div>
      </section>

      {/* Problem Cards */}
      <section className="py-20 bg-gray-50 px-4">
        <h2 className="text-3xl font-bold text-center mb-12">Sound familiar?</h2>
        <div className="grid md:grid-cols-3 gap-6 max-w-5xl mx-auto">
          {[
            { icon: "😤", title: "Tool overload", stat: "10+", label: "tools to manage" },
            { icon: "🔍", title: "Info scattered", stat: "40%", label: "time searching" },
            { icon: "🔥", title: "Burnout", stat: "60%", label: "on busywork" },
          ].map(p => (
            <div key={p.title} className="bg-white p-6 rounded-2xl border shadow-sm">
              <span className="text-4xl">{p.icon}</span>
              <h3 className="text-xl font-bold mt-4 mb-2">{p.title}</h3>
              <div className="text-3xl font-bold text-red-500">{p.stat}</div>
              <div className="text-sm text-gray-500">{p.label}</div>
            </div>
          ))}
        </div>
      </section>

      {/* Solution */}
      <section className="py-20 px-4">
        <div className="max-w-5xl mx-auto grid md:grid-cols-2 gap-12 items-center">
          <div>
            <span className="text-purple-600 font-medium">The Solution</span>
            <h2 className="text-4xl font-bold mt-2 mb-6">One platform to rule them all</h2>
            <ul className="space-y-3">
              {["Replace 10 tools with 1", "AI-powered automation", "Real-time collaboration"].map(f => (
                <li key={f} className="flex items-center gap-3">
                  <span className="w-6 h-6 bg-green-100 text-green-600 rounded-full flex items-center justify-center text-sm">✓</span>
                  {f}
                </li>
              ))}
            </ul>
          </div>
          <div className="bg-gray-100 rounded-xl p-4">
            <div className="bg-white rounded-lg shadow-lg p-8 text-center">
              <span className="text-6xl">📊</span>
              <p className="mt-4 text-gray-500">Dashboard Preview</p>
            </div>
          </div>
        </div>
      </section>

      {/* CTA */}
      <section className="py-20 px-4">
        <div className="max-w-3xl mx-auto bg-gradient-to-br from-purple-600 to-pink-600 rounded-3xl p-12 text-center text-white">
          <h2 className="text-4xl font-bold mb-4">Ready to 10x your team?</h2>
          <p className="text-lg opacity-90 mb-8">Join 500+ startups already shipping faster.</p>
          <button className="h-14 px-10 bg-white text-purple-600 rounded-full font-semibold text-lg">
            Start Free Trial →
          </button>
        </div>
      </section>

      {/* Footer */}
      <footer className="py-12 border-t px-4">
        <div className="max-w-6xl mx-auto flex justify-between items-center">
          <span className="font-bold">🚀 StartupKit</span>
          <span className="text-sm text-gray-500">© 2024 All rights reserved</span>
        </div>
      </footer>
    </div>
  )
}
```
