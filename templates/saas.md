# SaaS Landing Page Template

Complete template combining all Magic UI components into a production-ready landing page.

---

## Full Page Structure

```tsx
// app/page.tsx
import { Header } from "@/components/sections/header"
import { Hero } from "@/components/sections/hero"
import { LogoCloud } from "@/components/sections/logo-cloud"
import { Features } from "@/components/sections/features"
import { HowItWorks } from "@/components/sections/how-it-works"
import { Testimonials } from "@/components/sections/testimonials"
import { Pricing } from "@/components/sections/pricing"
import { FAQ } from "@/components/sections/faq"
import { CTA } from "@/components/sections/cta"
import { Footer } from "@/components/sections/footer"

export default function LandingPage() {
  return (
    <div className="min-h-screen bg-background">
      <Header />
      <main>
        <Hero />
        <LogoCloud />
        <Features />
        <HowItWorks />
        <Testimonials />
        <Pricing />
        <FAQ />
        <CTA />
      </main>
      <Footer />
    </div>
  )
}
```

---

## 1. Header Section

```tsx
"use client"
import { useState } from "react"
import { motion, AnimatePresence } from "framer-motion"
import { Menu, X } from "lucide-react"
import { ShimmerButton } from "@/components/magicui/shimmer-button"

const navItems = [
  { label: "Features", href: "#features" },
  { label: "Pricing", href: "#pricing" },
  { label: "Testimonials", href: "#testimonials" },
  { label: "FAQ", href: "#faq" },
]

export function Header() {
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false)

  return (
    <header className="fixed top-0 z-50 w-full border-b bg-background/80 backdrop-blur-lg">
      <div className="container mx-auto flex h-16 items-center justify-between px-4">
        {/* Logo */}
        <a href="/" className="flex items-center gap-2">
          <span className="text-xl font-bold">✨ MagicSaaS</span>
        </a>

        {/* Desktop Navigation */}
        <nav className="hidden md:flex items-center gap-8">
          {navItems.map((item) => (
            <a
              key={item.href}
              href={item.href}
              className="text-sm font-medium text-muted-foreground hover:text-foreground transition-colors"
            >
              {item.label}
            </a>
          ))}
        </nav>

        {/* CTA Buttons */}
        <div className="hidden md:flex items-center gap-4">
          <a href="/login" className="text-sm font-medium hover:underline">
            Log in
          </a>
          <ShimmerButton className="h-9 px-4">
            <span className="text-sm">Get Started</span>
          </ShimmerButton>
        </div>

        {/* Mobile Menu Button */}
        <button
          className="md:hidden p-2"
          onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
        >
          {mobileMenuOpen ? <X /> : <Menu />}
        </button>
      </div>

      {/* Mobile Menu */}
      <AnimatePresence>
        {mobileMenuOpen && (
          <motion.div
            initial={{ opacity: 0, height: 0 }}
            animate={{ opacity: 1, height: "auto" }}
            exit={{ opacity: 0, height: 0 }}
            className="md:hidden border-t bg-background"
          >
            <nav className="container mx-auto px-4 py-4 flex flex-col gap-4">
              {navItems.map((item) => (
                <a
                  key={item.href}
                  href={item.href}
                  className="text-sm font-medium py-2"
                  onClick={() => setMobileMenuOpen(false)}
                >
                  {item.label}
                </a>
              ))}
              <ShimmerButton className="w-full mt-4">
                Get Started
              </ShimmerButton>
            </nav>
          </motion.div>
        )}
      </AnimatePresence>
    </header>
  )
}
```

---

## 2. Hero Section

```tsx
import { AnimatedGradientText } from "@/components/magicui/animated-gradient-text"
import { WordRotate } from "@/components/magicui/word-rotate"
import { ShimmerButton } from "@/components/magicui/shimmer-button"
import { RainbowButton } from "@/components/magicui/rainbow-button"
import { BorderBeam } from "@/components/magicui/border-beam"
import { DotPattern } from "@/components/magicui/dot-pattern"
import { Safari } from "@/components/magicui/safari"

export function Hero() {
  return (
    <section className="relative min-h-screen pt-32 pb-20 overflow-hidden">
      {/* Background */}
      <DotPattern className="[mask-image:radial-gradient(600px_circle_at_center,white,transparent)]" />
      
      <div className="container mx-auto px-4 text-center relative z-10">
        {/* Announcement Badge */}
        <AnimatedGradientText className="mb-8">
          🎉 <span className="mx-1">Introducing v2.0</span> →
        </AnimatedGradientText>

        {/* Main Headline */}
        <h1 className="text-4xl md:text-6xl lg:text-7xl font-bold tracking-tight max-w-4xl mx-auto">
          Build{" "}
          <WordRotate
            words={["faster", "better", "smarter"]}
            className="text-primary"
          />{" "}
          products with Magic UI
        </h1>

        {/* Subheadline */}
        <p className="mt-6 text-lg md:text-xl text-muted-foreground max-w-2xl mx-auto">
          150+ beautifully designed components. Copy, paste, customize.
          Built with React, Tailwind CSS, and Framer Motion.
        </p>

        {/* CTA Buttons */}
        <div className="mt-10 flex flex-col sm:flex-row gap-4 justify-center">
          <ShimmerButton className="h-12 px-8">
            <span className="text-base font-semibold">Get Started Free</span>
          </ShimmerButton>
          <RainbowButton className="h-12 px-8">
            <span className="text-base font-semibold">View Components</span>
          </RainbowButton>
        </div>

        {/* Social Proof */}
        <p className="mt-8 text-sm text-muted-foreground">
          Trusted by 10,000+ developers worldwide
        </p>

        {/* Hero Image/Demo */}
        <div className="mt-16 relative max-w-5xl mx-auto">
          <div className="relative rounded-xl border bg-background shadow-2xl overflow-hidden">
            <BorderBeam size={250} duration={12} />
            <Safari url="magicui.design" className="w-full">
              <img 
                src="/dashboard-preview.png" 
                alt="Product preview"
                className="w-full"
              />
            </Safari>
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## 3. Logo Cloud Section

```tsx
import { Marquee } from "@/components/magicui/marquee"

const logos = [
  { name: "Vercel", src: "/logos/vercel.svg" },
  { name: "Stripe", src: "/logos/stripe.svg" },
  { name: "GitHub", src: "/logos/github.svg" },
  { name: "Notion", src: "/logos/notion.svg" },
  { name: "Linear", src: "/logos/linear.svg" },
  { name: "Figma", src: "/logos/figma.svg" },
]

export function LogoCloud() {
  return (
    <section className="py-16 border-y bg-muted/30">
      <div className="container mx-auto px-4">
        <p className="text-center text-sm font-medium text-muted-foreground mb-8">
          TRUSTED BY TEAMS AT
        </p>
        
        <Marquee pauseOnHover className="[--duration:30s]">
          {logos.map((logo) => (
            <img
              key={logo.name}
              src={logo.src}
              alt={logo.name}
              className="h-8 w-auto mx-8 opacity-60 hover:opacity-100 transition-opacity grayscale hover:grayscale-0"
            />
          ))}
        </Marquee>
      </div>
    </section>
  )
}
```

---

## 4. Features Section (Bento Grid)

```tsx
import { BentoGrid, BentoCard } from "@/components/magicui/bento-grid"
import { Marquee } from "@/components/magicui/marquee"
import { AnimatedBeam } from "@/components/magicui/animated-beam"
import { Globe } from "@/components/magicui/globe"
import { 
  Sparkles, 
  Zap, 
  Shield, 
  BarChart, 
  Puzzle 
} from "lucide-react"

export function Features() {
  return (
    <section id="features" className="py-24">
      <div className="container mx-auto px-4">
        {/* Section Header */}
        <div className="text-center max-w-3xl mx-auto mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Everything you need to build faster
          </h2>
          <p className="text-lg text-muted-foreground">
            Powerful components, beautiful animations, production-ready code.
          </p>
        </div>

        {/* Bento Grid */}
        <BentoGrid className="max-w-6xl mx-auto">
          <BentoCard
            name="150+ Components"
            className="col-span-3 lg:col-span-2"
            Icon={Sparkles}
            description="From buttons to complex layouts, everything you need."
            href="/components"
            cta="Browse components"
            background={
              <Marquee className="absolute top-10 [--duration:20s] opacity-30">
                {["Button", "Card", "Modal", "Toast", "Menu"].map((c) => (
                  <span key={c} className="mx-4 text-2xl font-mono">{c}</span>
                ))}
              </Marquee>
            }
          />
          
          <BentoCard
            name="Lightning Fast"
            className="col-span-3 lg:col-span-1"
            Icon={Zap}
            description="Optimized for performance. No bloat."
            href="/docs/performance"
            cta="Learn more"
          />
          
          <BentoCard
            name="Enterprise Security"
            className="col-span-3 lg:col-span-1"
            Icon={Shield}
            description="Built with security best practices."
            href="/docs/security"
            cta="View security"
          />
          
          <BentoCard
            name="Analytics Built-in"
            className="col-span-3 lg:col-span-2"
            Icon={BarChart}
            description="Track everything with our analytics dashboard."
            href="/docs/analytics"
            cta="See analytics"
            background={
              <Globe className="absolute -right-10 -bottom-10 opacity-30" />
            }
          />
        </BentoGrid>
      </div>
    </section>
  )
}
```

---

## 5. Testimonials Section

```tsx
import { Marquee } from "@/components/magicui/marquee"
import { cn } from "@/lib/utils"

const testimonials = [
  {
    name: "Sarah Chen",
    role: "CTO at TechCorp",
    content: "Magic UI has transformed how we build products. The components are beautiful and the DX is incredible.",
    avatar: "https://avatar.vercel.sh/sarah"
  },
  {
    name: "Michael Park",
    role: "Founder at Startup",
    content: "Saved us hundreds of hours. Our landing page went from idea to launch in a single day.",
    avatar: "https://avatar.vercel.sh/michael"
  },
  {
    name: "Emily Rodriguez",
    role: "Design Lead at Agency",
    content: "The attention to detail in every animation is remarkable. Our clients love it.",
    avatar: "https://avatar.vercel.sh/emily"
  },
  {
    name: "David Kim",
    role: "Senior Developer",
    content: "Finally, a component library that looks good out of the box. No more fighting with CSS.",
    avatar: "https://avatar.vercel.sh/david"
  },
  {
    name: "Lisa Thompson",
    role: "Product Manager",
    content: "The ROI on Magic UI Pro was immediate. We shipped our redesign weeks ahead of schedule.",
    avatar: "https://avatar.vercel.sh/lisa"
  },
  {
    name: "James Wilson",
    role: "Indie Hacker",
    content: "As a solo founder, Magic UI lets me punch way above my weight. Highly recommended!",
    avatar: "https://avatar.vercel.sh/james"
  },
]

function TestimonialCard({ name, role, content, avatar }) {
  return (
    <figure className={cn(
      "relative w-80 cursor-pointer overflow-hidden rounded-xl border p-6",
      "border-gray-950/[.1] bg-gray-950/[.01] hover:bg-gray-950/[.05]",
      "dark:border-gray-50/[.1] dark:bg-gray-50/[.10] dark:hover:bg-gray-50/[.15]"
    )}>
      <div className="flex items-center gap-3 mb-4">
        <img className="rounded-full" width="40" height="40" alt={name} src={avatar} />
        <div>
          <figcaption className="font-semibold">{name}</figcaption>
          <p className="text-sm text-muted-foreground">{role}</p>
        </div>
      </div>
      <blockquote className="text-sm leading-relaxed">{content}</blockquote>
    </figure>
  )
}

export function Testimonials() {
  const firstRow = testimonials.slice(0, testimonials.length / 2)
  const secondRow = testimonials.slice(testimonials.length / 2)

  return (
    <section id="testimonials" className="py-24 bg-muted/30">
      <div className="container mx-auto px-4">
        <div className="text-center max-w-3xl mx-auto mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Loved by developers worldwide
          </h2>
          <p className="text-lg text-muted-foreground">
            Join thousands of teams building better products with Magic UI.
          </p>
        </div>

        <div className="relative">
          <Marquee pauseOnHover className="[--duration:40s] mb-4">
            {firstRow.map((t) => <TestimonialCard key={t.name} {...t} />)}
          </Marquee>
          <Marquee reverse pauseOnHover className="[--duration:40s]">
            {secondRow.map((t) => <TestimonialCard key={t.name} {...t} />)}
          </Marquee>
          
          {/* Gradient overlays */}
          <div className="pointer-events-none absolute inset-y-0 left-0 w-1/4 bg-gradient-to-r from-background" />
          <div className="pointer-events-none absolute inset-y-0 right-0 w-1/4 bg-gradient-to-l from-background" />
        </div>
      </div>
    </section>
  )
}
```

---

## 6. Pricing Section

```tsx
import { cn } from "@/lib/utils"
import { ShimmerButton } from "@/components/magicui/shimmer-button"
import { BorderBeam } from "@/components/magicui/border-beam"
import { Check } from "lucide-react"

const plans = [
  {
    name: "Free",
    price: "$0",
    description: "Perfect for trying out Magic UI",
    features: [
      "50+ free components",
      "Community support",
      "MIT License",
      "Basic documentation",
    ],
    cta: "Get Started",
    highlighted: false,
  },
  {
    name: "Pro",
    price: "$199",
    description: "Everything you need to ship faster",
    features: [
      "150+ premium components",
      "9 landing page templates",
      "Priority support",
      "Lifetime updates",
      "Commercial license",
      "Figma file included",
    ],
    cta: "Get Unlimited Access",
    highlighted: true,
  },
  {
    name: "Team",
    price: "$499",
    description: "For teams building at scale",
    features: [
      "Everything in Pro",
      "Team license (up to 10)",
      "Private Slack channel",
      "Custom components",
      "Design consultation",
    ],
    cta: "Contact Sales",
    highlighted: false,
  },
]

export function Pricing() {
  return (
    <section id="pricing" className="py-24">
      <div className="container mx-auto px-4">
        <div className="text-center max-w-3xl mx-auto mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Simple, transparent pricing
          </h2>
          <p className="text-lg text-muted-foreground">
            Choose the plan that's right for you. No hidden fees.
          </p>
        </div>

        <div className="grid md:grid-cols-3 gap-8 max-w-5xl mx-auto">
          {plans.map((plan) => (
            <div
              key={plan.name}
              className={cn(
                "relative rounded-2xl border p-8",
                plan.highlighted 
                  ? "border-primary bg-primary/5" 
                  : "border-border"
              )}
            >
              {plan.highlighted && <BorderBeam size={200} duration={10} />}
              
              <div className="mb-6">
                <h3 className="text-xl font-bold">{plan.name}</h3>
                <div className="mt-2">
                  <span className="text-4xl font-bold">{plan.price}</span>
                  {plan.price !== "$0" && (
                    <span className="text-muted-foreground ml-1">one-time</span>
                  )}
                </div>
                <p className="mt-2 text-sm text-muted-foreground">
                  {plan.description}
                </p>
              </div>

              <ul className="space-y-3 mb-8">
                {plan.features.map((feature) => (
                  <li key={feature} className="flex items-center gap-2 text-sm">
                    <Check className="h-4 w-4 text-primary" />
                    {feature}
                  </li>
                ))}
              </ul>

              {plan.highlighted ? (
                <ShimmerButton className="w-full h-11">
                  {plan.cta}
                </ShimmerButton>
              ) : (
                <button className="w-full h-11 rounded-lg border font-medium hover:bg-muted transition-colors">
                  {plan.cta}
                </button>
              )}
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## 7. FAQ Section

```tsx
"use client"
import { useState } from "react"
import { motion, AnimatePresence } from "framer-motion"
import { ChevronDown } from "lucide-react"
import { cn } from "@/lib/utils"

const faqs = [
  {
    question: "What's included in the Pro plan?",
    answer: "The Pro plan includes access to all 150+ components, 9 landing page templates, lifetime updates, priority support, and a commercial license for unlimited projects."
  },
  {
    question: "Can I use Magic UI for client projects?",
    answer: "Yes! The Pro and Team licenses allow you to use Magic UI in unlimited client projects. The free components are MIT licensed and can be used in any project."
  },
  {
    question: "Do you offer refunds?",
    answer: "Yes, we offer a 14-day money-back guarantee. If you're not satisfied, contact us for a full refund."
  },
  {
    question: "How do I get updates?",
    answer: "All updates are delivered through our npm package and GitHub repository. Pro users get lifetime access to all future updates at no additional cost."
  },
  {
    question: "Is there a discount for students?",
    answer: "Yes! We offer 50% off for students and educators. Contact us with your .edu email to get your discount code."
  },
]

function FAQItem({ question, answer, isOpen, onClick }) {
  return (
    <div className="border-b">
      <button
        className="flex w-full items-center justify-between py-4 text-left"
        onClick={onClick}
      >
        <span className="font-medium">{question}</span>
        <ChevronDown
          className={cn(
            "h-5 w-5 text-muted-foreground transition-transform",
            isOpen && "rotate-180"
          )}
        />
      </button>
      <AnimatePresence>
        {isOpen && (
          <motion.div
            initial={{ height: 0, opacity: 0 }}
            animate={{ height: "auto", opacity: 1 }}
            exit={{ height: 0, opacity: 0 }}
            className="overflow-hidden"
          >
            <p className="pb-4 text-muted-foreground">{answer}</p>
          </motion.div>
        )}
      </AnimatePresence>
    </div>
  )
}

export function FAQ() {
  const [openIndex, setOpenIndex] = useState<number | null>(0)

  return (
    <section id="faq" className="py-24 bg-muted/30">
      <div className="container mx-auto px-4">
        <div className="text-center max-w-3xl mx-auto mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Frequently asked questions
          </h2>
          <p className="text-lg text-muted-foreground">
            Everything you need to know about Magic UI.
          </p>
        </div>

        <div className="max-w-2xl mx-auto">
          {faqs.map((faq, index) => (
            <FAQItem
              key={index}
              question={faq.question}
              answer={faq.answer}
              isOpen={openIndex === index}
              onClick={() => setOpenIndex(openIndex === index ? null : index)}
            />
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## 8. CTA Section

```tsx
import { ShimmerButton } from "@/components/magicui/shimmer-button"
import { Particles } from "@/components/magicui/particles"
import { BorderBeam } from "@/components/magicui/border-beam"

export function CTA() {
  return (
    <section className="py-24 relative overflow-hidden">
      <Particles className="absolute inset-0" quantity={50} />
      
      <div className="container mx-auto px-4 relative z-10">
        <div className="relative rounded-3xl border bg-gradient-to-b from-primary/10 to-transparent p-12 md:p-16 text-center overflow-hidden">
          <BorderBeam size={300} duration={15} />
          
          <h2 className="text-3xl md:text-4xl lg:text-5xl font-bold mb-4">
            Ready to ship faster?
          </h2>
          <p className="text-lg text-muted-foreground mb-8 max-w-2xl mx-auto">
            Join 10,000+ developers building beautiful products with Magic UI.
            Get started in minutes.
          </p>
          
          <div className="flex flex-col sm:flex-row gap-4 justify-center">
            <ShimmerButton className="h-12 px-8">
              <span className="text-base font-semibold">Get Started Free</span>
            </ShimmerButton>
            <button className="h-12 px-8 rounded-full border font-semibold hover:bg-muted transition-colors">
              Schedule Demo
            </button>
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## 9. Footer Section

```tsx
export function Footer() {
  const links = {
    Product: ["Components", "Templates", "Pricing", "Changelog"],
    Resources: ["Documentation", "Blog", "Community", "Support"],
    Company: ["About", "Careers", "Contact", "Legal"],
    Social: ["Twitter", "GitHub", "Discord", "YouTube"],
  }

  return (
    <footer className="border-t py-16">
      <div className="container mx-auto px-4">
        <div className="grid grid-cols-2 md:grid-cols-5 gap-8">
          {/* Logo & Description */}
          <div className="col-span-2 md:col-span-1">
            <span className="text-xl font-bold">✨ MagicUI</span>
            <p className="mt-4 text-sm text-muted-foreground">
              Beautiful components for modern web applications.
            </p>
          </div>

          {/* Links */}
          {Object.entries(links).map(([title, items]) => (
            <div key={title}>
              <h3 className="font-semibold mb-4">{title}</h3>
              <ul className="space-y-2">
                {items.map((item) => (
                  <li key={item}>
                    <a
                      href="#"
                      className="text-sm text-muted-foreground hover:text-foreground transition-colors"
                    >
                      {item}
                    </a>
                  </li>
                ))}
              </ul>
            </div>
          ))}
        </div>

        <div className="mt-16 pt-8 border-t flex flex-col md:flex-row justify-between items-center gap-4">
          <p className="text-sm text-muted-foreground">
            © 2024 MagicUI. All rights reserved.
          </p>
          <div className="flex gap-4">
            <a href="#" className="text-sm text-muted-foreground hover:text-foreground">
              Privacy Policy
            </a>
            <a href="#" className="text-sm text-muted-foreground hover:text-foreground">
              Terms of Service
            </a>
          </div>
        </div>
      </div>
    </footer>
  )
}
```

---

## Artifact-Ready Complete Landing Page

For Claude artifacts, here's a self-contained version:

```jsx
export default function MagicUILanding() {
  const [mobileMenu, setMobileMenu] = React.useState(false)
  const [activeWord, setActiveWord] = React.useState(0)
  const words = ["faster", "better", "smarter"]

  React.useEffect(() => {
    const interval = setInterval(() => {
      setActiveWord((i) => (i + 1) % words.length)
    }, 2000)
    return () => clearInterval(interval)
  }, [])

  return (
    <div className="min-h-screen bg-white text-gray-900">
      <style>{`
        @keyframes marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }
        @keyframes shimmer { to { transform: translate(calc(100cqw - 100%), calc(100cqh - 100%)); } }
        @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
      `}</style>

      {/* Header */}
      <header className="fixed top-0 z-50 w-full border-b bg-white/80 backdrop-blur-lg">
        <div className="max-w-6xl mx-auto px-4 h-16 flex items-center justify-between">
          <span className="text-xl font-bold">✨ MagicUI</span>
          <nav className="hidden md:flex gap-8">
            {["Features", "Pricing", "Docs"].map(item => (
              <a key={item} href="#" className="text-sm text-gray-600 hover:text-gray-900">{item}</a>
            ))}
          </nav>
          <button className="relative px-4 py-2 bg-black text-white text-sm rounded-full overflow-hidden">
            Get Started
          </button>
        </div>
      </header>

      {/* Hero */}
      <section className="pt-32 pb-20 px-4 text-center relative overflow-hidden">
        {/* Dot pattern */}
        <svg className="absolute inset-0 w-full h-full opacity-30" style={{ mask: 'radial-gradient(400px at center, white, transparent)' }}>
          <pattern id="dots" width="16" height="16" patternUnits="userSpaceOnUse">
            <circle cx="1" cy="1" r="1" fill="#6b7280" />
          </pattern>
          <rect width="100%" height="100%" fill="url(#dots)" />
        </svg>

        <div className="relative z-10 max-w-4xl mx-auto">
          <div className="inline-flex items-center gap-2 px-4 py-1 rounded-full bg-gray-100 text-sm mb-8">
            🎉 Introducing v2.0 →
          </div>

          <h1 className="text-5xl md:text-7xl font-bold mb-6">
            Build{" "}
            <span className="text-purple-600">{words[activeWord]}</span>
            <br />products with Magic UI
          </h1>

          <p className="text-xl text-gray-600 mb-10 max-w-2xl mx-auto">
            150+ beautifully designed components. Copy, paste, customize.
          </p>

          <div className="flex gap-4 justify-center">
            <button className="px-6 py-3 bg-black text-white rounded-full font-semibold">
              Get Started Free
            </button>
            <button className="px-6 py-3 border rounded-full font-semibold">
              View Components
            </button>
          </div>
        </div>
      </section>

      {/* Logo marquee */}
      <section className="py-12 border-y bg-gray-50 overflow-hidden">
        <p className="text-center text-sm text-gray-500 mb-6">TRUSTED BY TEAMS AT</p>
        <div className="flex" style={{ animation: 'marquee 20s linear infinite' }}>
          {[...Array(2)].map((_, i) => (
            <div key={i} className="flex shrink-0">
              {["Vercel", "Stripe", "GitHub", "Notion", "Linear"].map(logo => (
                <span key={logo} className="mx-8 text-xl font-semibold text-gray-400">{logo}</span>
              ))}
            </div>
          ))}
        </div>
      </section>

      {/* Features Bento */}
      <section className="py-24 px-4">
        <div className="max-w-6xl mx-auto">
          <h2 className="text-3xl font-bold text-center mb-4">Everything you need</h2>
          <p className="text-gray-600 text-center mb-16">Powerful components, beautiful animations.</p>

          <div className="grid md:grid-cols-3 gap-4 auto-rows-[200px]">
            <div className="md:col-span-2 rounded-2xl border bg-gradient-to-br from-purple-50 to-white p-6 flex flex-col justify-end">
              <span className="text-3xl mb-2">✨</span>
              <h3 className="font-bold text-xl">150+ Components</h3>
              <p className="text-gray-600">From buttons to complex layouts</p>
            </div>
            <div className="rounded-2xl border p-6 flex flex-col justify-end bg-yellow-50">
              <span className="text-3xl mb-2">⚡</span>
              <h3 className="font-bold text-xl">Lightning Fast</h3>
              <p className="text-gray-600">Optimized for performance</p>
            </div>
            <div className="rounded-2xl border p-6 flex flex-col justify-end bg-green-50">
              <span className="text-3xl mb-2">🔒</span>
              <h3 className="font-bold text-xl">Secure</h3>
              <p className="text-gray-600">Enterprise-grade security</p>
            </div>
            <div className="md:col-span-2 rounded-2xl border p-6 flex flex-col justify-end bg-blue-50">
              <span className="text-3xl mb-2">📊</span>
              <h3 className="font-bold text-xl">Analytics Built-in</h3>
              <p className="text-gray-600">Track everything in real-time</p>
            </div>
          </div>
        </div>
      </section>

      {/* CTA */}
      <section className="py-24 px-4">
        <div className="max-w-4xl mx-auto text-center bg-gradient-to-b from-purple-100 to-white rounded-3xl border p-12">
          <h2 className="text-4xl font-bold mb-4">Ready to ship faster?</h2>
          <p className="text-gray-600 mb-8">Join 10,000+ developers building with Magic UI.</p>
          <button className="px-8 py-4 bg-black text-white rounded-full font-semibold text-lg">
            Get Started Free
          </button>
        </div>
      </section>

      {/* Footer */}
      <footer className="border-t py-12 px-4">
        <div className="max-w-6xl mx-auto flex justify-between items-center">
          <span className="text-xl font-bold">✨ MagicUI</span>
          <p className="text-sm text-gray-500">© 2024 MagicUI. All rights reserved.</p>
        </div>
      </footer>
    </div>
  )
}
```
