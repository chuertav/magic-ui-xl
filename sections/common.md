# Common Sections Reference

Reusable sections: Header, Footer, CTA, FAQ, and more.

---

## 1. Header - Sticky with Blur

Modern sticky header with backdrop blur.

```tsx
"use client"
import { useState, useEffect } from "react"
import { motion, AnimatePresence } from "framer-motion"
import { Menu, X } from "lucide-react"
import { cn } from "@/lib/utils"
import { ShimmerButton } from "@/components/magicui/shimmer-button"

const navItems = [
  { label: "Features", href: "#features" },
  { label: "Pricing", href: "#pricing" },
  { label: "Docs", href: "/docs" },
  { label: "Blog", href: "/blog" },
]

export function Header() {
  const [scrolled, setScrolled] = useState(false)
  const [mobileOpen, setMobileOpen] = useState(false)

  useEffect(() => {
    const handleScroll = () => setScrolled(window.scrollY > 20)
    window.addEventListener("scroll", handleScroll)
    return () => window.removeEventListener("scroll", handleScroll)
  }, [])

  return (
    <header
      className={cn(
        "fixed top-0 z-50 w-full transition-all duration-300",
        scrolled
          ? "bg-background/80 backdrop-blur-lg border-b shadow-sm"
          : "bg-transparent"
      )}
    >
      <div className="container mx-auto px-4">
        <div className="flex h-16 items-center justify-between">
          {/* Logo */}
          <a href="/" className="flex items-center gap-2 font-bold text-xl">
            <span className="text-2xl">✨</span>
            <span>MagicUI</span>
          </a>

          {/* Desktop Nav */}
          <nav className="hidden md:flex items-center gap-8">
            {navItems.map((item) => (
              <a
                key={item.href}
                href={item.href}
                className="text-sm text-muted-foreground hover:text-foreground transition-colors"
              >
                {item.label}
              </a>
            ))}
          </nav>

          {/* Desktop CTA */}
          <div className="hidden md:flex items-center gap-4">
            <a href="/login" className="text-sm font-medium hover:underline">
              Sign in
            </a>
            <ShimmerButton className="h-9 px-4">
              <span className="text-sm font-medium">Get Started</span>
            </ShimmerButton>
          </div>

          {/* Mobile Menu Button */}
          <button
            className="md:hidden p-2"
            onClick={() => setMobileOpen(!mobileOpen)}
          >
            {mobileOpen ? <X className="h-6 w-6" /> : <Menu className="h-6 w-6" />}
          </button>
        </div>
      </div>

      {/* Mobile Menu */}
      <AnimatePresence>
        {mobileOpen && (
          <motion.div
            initial={{ opacity: 0, height: 0 }}
            animate={{ opacity: 1, height: "auto" }}
            exit={{ opacity: 0, height: 0 }}
            className="md:hidden border-t bg-background"
          >
            <nav className="container mx-auto px-4 py-4 flex flex-col gap-2">
              {navItems.map((item) => (
                <a
                  key={item.href}
                  href={item.href}
                  className="py-2 text-sm font-medium"
                  onClick={() => setMobileOpen(false)}
                >
                  {item.label}
                </a>
              ))}
              <hr className="my-2" />
              <a href="/login" className="py-2 text-sm">Sign in</a>
              <ShimmerButton className="w-full mt-2">Get Started</ShimmerButton>
            </nav>
          </motion.div>
        )}
      </AnimatePresence>
    </header>
  )
}
```

---

## 2. Footer - Multi-Column

Standard multi-column footer with newsletter.

```tsx
export function Footer() {
  const links = {
    Product: [
      { label: "Features", href: "#features" },
      { label: "Pricing", href: "#pricing" },
      { label: "Changelog", href: "/changelog" },
      { label: "Roadmap", href: "/roadmap" },
    ],
    Resources: [
      { label: "Documentation", href: "/docs" },
      { label: "API Reference", href: "/api" },
      { label: "Blog", href: "/blog" },
      { label: "Community", href: "/community" },
    ],
    Company: [
      { label: "About", href: "/about" },
      { label: "Careers", href: "/careers" },
      { label: "Contact", href: "/contact" },
      { label: "Press", href: "/press" },
    ],
    Legal: [
      { label: "Privacy", href: "/privacy" },
      { label: "Terms", href: "/terms" },
      { label: "Cookies", href: "/cookies" },
    ],
  }

  return (
    <footer className="border-t bg-muted/30">
      <div className="container mx-auto px-4 py-16">
        <div className="grid grid-cols-2 md:grid-cols-6 gap-8">
          {/* Logo & Description */}
          <div className="col-span-2">
            <a href="/" className="flex items-center gap-2 font-bold text-xl mb-4">
              <span className="text-2xl">✨</span>
              <span>MagicUI</span>
            </a>
            <p className="text-sm text-muted-foreground mb-6 max-w-xs">
              Beautiful components for modern web applications. Built with React and Tailwind CSS.
            </p>
            
            {/* Newsletter */}
            <div className="flex gap-2">
              <input
                type="email"
                placeholder="Enter your email"
                className="flex-1 h-10 px-3 rounded-lg border bg-background text-sm"
              />
              <button className="h-10 px-4 bg-primary text-primary-foreground rounded-lg text-sm font-medium">
                Subscribe
              </button>
            </div>
          </div>

          {/* Link Columns */}
          {Object.entries(links).map(([title, items]) => (
            <div key={title}>
              <h4 className="font-semibold mb-4">{title}</h4>
              <ul className="space-y-2">
                {items.map((item) => (
                  <li key={item.href}>
                    <a
                      href={item.href}
                      className="text-sm text-muted-foreground hover:text-foreground transition-colors"
                    >
                      {item.label}
                    </a>
                  </li>
                ))}
              </ul>
            </div>
          ))}
        </div>

        {/* Bottom */}
        <div className="mt-16 pt-8 border-t flex flex-col md:flex-row justify-between items-center gap-4">
          <p className="text-sm text-muted-foreground">
            © {new Date().getFullYear()} MagicUI. All rights reserved.
          </p>
          
          {/* Social Links */}
          <div className="flex gap-4">
            {["Twitter", "GitHub", "Discord", "YouTube"].map((social) => (
              <a
                key={social}
                href="#"
                className="text-sm text-muted-foreground hover:text-foreground transition-colors"
              >
                {social}
              </a>
            ))}
          </div>
        </div>
      </div>
    </footer>
  )
}
```

---

## 3. CTA Section - With Background Effect

Call-to-action section with particles or gradient background.

```tsx
import { Particles } from "@/components/magicui/particles"
import { BorderBeam } from "@/components/magicui/border-beam"
import { ShimmerButton } from "@/components/magicui/shimmer-button"

export function CTASection() {
  return (
    <section className="py-24 relative overflow-hidden">
      <Particles className="absolute inset-0" quantity={40} color="#8b5cf6" />
      
      <div className="container mx-auto px-4 relative z-10">
        <div className="relative max-w-4xl mx-auto rounded-3xl border bg-gradient-to-b from-primary/10 via-primary/5 to-transparent p-12 md:p-16 text-center overflow-hidden">
          <BorderBeam size={300} duration={15} />
          
          <h2 className="text-3xl md:text-5xl font-bold mb-4">
            Ready to get started?
          </h2>
          <p className="text-lg text-muted-foreground mb-8 max-w-xl mx-auto">
            Join thousands of developers building amazing products with our platform.
            Start your free trial today.
          </p>
          
          <div className="flex flex-col sm:flex-row gap-4 justify-center">
            <ShimmerButton className="h-12 px-8">
              <span className="font-semibold">Start Free Trial</span>
            </ShimmerButton>
            <button className="h-12 px-8 border rounded-full font-semibold hover:bg-muted transition-colors">
              Talk to Sales
            </button>
          </div>
          
          <p className="mt-6 text-sm text-muted-foreground">
            No credit card required • 14-day free trial • Cancel anytime
          </p>
        </div>
      </div>
    </section>
  )
}
```

---

## 4. FAQ Section - Accordion

Frequently asked questions with accordion.

```tsx
"use client"
import { useState } from "react"
import { motion, AnimatePresence } from "framer-motion"
import { ChevronDown } from "lucide-react"
import { cn } from "@/lib/utils"

const faqs = [
  {
    question: "How does the free trial work?",
    answer: "You get full access to all features for 14 days. No credit card required. At the end of the trial, you can choose a plan that fits your needs."
  },
  {
    question: "Can I cancel my subscription anytime?",
    answer: "Yes, you can cancel your subscription at any time. Your access will continue until the end of your billing period."
  },
  {
    question: "Do you offer refunds?",
    answer: "Yes, we offer a 30-day money-back guarantee. If you're not satisfied, contact support for a full refund."
  },
  {
    question: "What payment methods do you accept?",
    answer: "We accept all major credit cards (Visa, Mastercard, American Express), PayPal, and bank transfers for enterprise plans."
  },
  {
    question: "Is there a discount for annual billing?",
    answer: "Yes! You save 20% when you choose annual billing compared to monthly billing."
  },
  {
    question: "Do you offer discounts for startups or students?",
    answer: "Yes, we offer 50% off for verified students and early-stage startups. Contact us to learn more."
  },
]

export function FAQSection() {
  const [openIndex, setOpenIndex] = useState<number | null>(0)

  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Frequently Asked Questions
          </h2>
          <p className="text-lg text-muted-foreground">
            Everything you need to know about our product
          </p>
        </div>

        <div className="max-w-2xl mx-auto">
          {faqs.map((faq, index) => (
            <div key={index} className="border-b">
              <button
                className="flex w-full items-center justify-between py-5 text-left"
                onClick={() => setOpenIndex(openIndex === index ? null : index)}
              >
                <span className="font-medium pr-4">{faq.question}</span>
                <ChevronDown
                  className={cn(
                    "h-5 w-5 shrink-0 text-muted-foreground transition-transform duration-200",
                    openIndex === index && "rotate-180"
                  )}
                />
              </button>
              
              <AnimatePresence>
                {openIndex === index && (
                  <motion.div
                    initial={{ height: 0, opacity: 0 }}
                    animate={{ height: "auto", opacity: 1 }}
                    exit={{ height: 0, opacity: 0 }}
                    transition={{ duration: 0.2 }}
                    className="overflow-hidden"
                  >
                    <p className="pb-5 text-muted-foreground">
                      {faq.answer}
                    </p>
                  </motion.div>
                )}
              </AnimatePresence>
            </div>
          ))}
        </div>

        <div className="text-center mt-12">
          <p className="text-muted-foreground mb-4">
            Still have questions?
          </p>
          <a href="/contact" className="text-primary font-medium hover:underline">
            Contact our support team →
          </a>
        </div>
      </div>
    </section>
  )
}
```

---

## 5. Social Proof - Stats Section

Statistics section with animated counters.

```tsx
import { NumberTicker } from "@/components/magicui/number-ticker"

const stats = [
  { value: 10000, suffix: "+", label: "Developers" },
  { value: 500, suffix: "K", label: "Downloads" },
  { value: 99.9, suffix: "%", label: "Uptime", decimals: 1 },
  { value: 150, suffix: "+", label: "Components" },
]

export function StatsSection() {
  return (
    <section className="py-16 bg-muted/30">
      <div className="container mx-auto px-4">
        <div className="grid grid-cols-2 md:grid-cols-4 gap-8">
          {stats.map((stat) => (
            <div key={stat.label} className="text-center">
              <div className="text-4xl md:text-5xl font-bold mb-2">
                <NumberTicker 
                  value={stat.value} 
                  decimalPlaces={stat.decimals || 0}
                />
                {stat.suffix}
              </div>
              <div className="text-muted-foreground">{stat.label}</div>
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## 6. Feature Grid - Simple Icons

Simple feature grid with icons.

```tsx
import { Zap, Shield, Globe, Sparkles, Code, Users } from "lucide-react"

const features = [
  { icon: Zap, title: "Lightning Fast", description: "Optimized for performance with lazy loading and code splitting." },
  { icon: Shield, title: "Secure by Default", description: "Built with security best practices and regular audits." },
  { icon: Globe, title: "Global CDN", description: "Content delivered from edge locations worldwide." },
  { icon: Sparkles, title: "Beautiful UI", description: "Pixel-perfect components with smooth animations." },
  { icon: Code, title: "Developer First", description: "Clean APIs and comprehensive documentation." },
  { icon: Users, title: "Team Ready", description: "Collaboration features for teams of any size." },
]

export function FeatureGrid() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Everything you need
          </h2>
          <p className="text-lg text-muted-foreground">
            Powerful features to help you build faster
          </p>
        </div>

        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-5xl mx-auto">
          {features.map((feature) => (
            <div key={feature.title} className="text-center p-6">
              <div className="w-12 h-12 rounded-xl bg-primary/10 flex items-center justify-center mx-auto mb-4">
                <feature.icon className="h-6 w-6 text-primary" />
              </div>
              <h3 className="font-semibold text-lg mb-2">{feature.title}</h3>
              <p className="text-sm text-muted-foreground">{feature.description}</p>
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## Artifact-Ready FAQ

```jsx
export default function FAQDemo() {
  const [open, setOpen] = React.useState(0)
  
  const faqs = [
    { q: "How does the free trial work?", a: "14 days full access, no credit card required." },
    { q: "Can I cancel anytime?", a: "Yes, cancel anytime. Access continues until billing period ends." },
    { q: "Do you offer refunds?", a: "Yes, 30-day money-back guarantee on all plans." },
    { q: "What payment methods do you accept?", a: "All major credit cards, PayPal, and bank transfers." },
  ]

  return (
    <div className="min-h-screen bg-white py-24 px-4">
      <div className="max-w-2xl mx-auto">
        <h2 className="text-3xl font-bold text-center mb-12">FAQ</h2>
        
        {faqs.map((faq, i) => (
          <div key={i} className="border-b">
            <button
              onClick={() => setOpen(open === i ? -1 : i)}
              className="w-full flex items-center justify-between py-5 text-left font-medium"
            >
              {faq.q}
              <span className={`transition-transform ${open === i ? 'rotate-180' : ''}`}>▼</span>
            </button>
            {open === i && (
              <p className="pb-5 text-gray-600">{faq.a}</p>
            )}
          </div>
        ))}
      </div>
    </div>
  )
}
```
