# Pricing Sections Reference

Multiple pricing section variants for different business models.

---

## 1. Pricing - Three Column Classic

Standard 3-tier pricing with highlighted recommended plan.

```tsx
import { cn } from "@/lib/utils"
import { Check } from "lucide-react"
import { ShimmerButton } from "@/components/magicui/shimmer-button"
import { BorderBeam } from "@/components/magicui/border-beam"

const plans = [
  {
    name: "Starter",
    price: "$9",
    period: "/month",
    description: "Perfect for side projects",
    features: [
      "Up to 3 projects",
      "Basic analytics",
      "48-hour support response",
      "1GB storage",
    ],
    cta: "Start Free Trial",
    highlighted: false,
  },
  {
    name: "Pro",
    price: "$29",
    period: "/month",
    description: "For growing businesses",
    features: [
      "Unlimited projects",
      "Advanced analytics",
      "24-hour support response",
      "10GB storage",
      "Custom domains",
      "Team collaboration",
    ],
    cta: "Get Started",
    highlighted: true,
    badge: "Most Popular",
  },
  {
    name: "Enterprise",
    price: "$99",
    period: "/month",
    description: "For large organizations",
    features: [
      "Everything in Pro",
      "Unlimited storage",
      "Priority support",
      "SSO & SAML",
      "Custom integrations",
      "Dedicated account manager",
    ],
    cta: "Contact Sales",
    highlighted: false,
  },
]

export function PricingThreeColumn() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-4xl font-bold mb-4">Simple, transparent pricing</h2>
          <p className="text-xl text-muted-foreground">
            Choose the plan that's right for you
          </p>
        </div>

        <div className="grid md:grid-cols-3 gap-8 max-w-6xl mx-auto">
          {plans.map((plan) => (
            <div
              key={plan.name}
              className={cn(
                "relative rounded-2xl p-8 flex flex-col",
                plan.highlighted
                  ? "border-2 border-primary bg-primary/5"
                  : "border bg-background"
              )}
            >
              {plan.highlighted && <BorderBeam size={200} duration={10} />}
              
              {plan.badge && (
                <div className="absolute -top-3 left-1/2 -translate-x-1/2 px-3 py-1 bg-primary text-primary-foreground text-sm font-medium rounded-full">
                  {plan.badge}
                </div>
              )}

              <div className="mb-6">
                <h3 className="text-xl font-bold mb-2">{plan.name}</h3>
                <p className="text-sm text-muted-foreground">{plan.description}</p>
              </div>

              <div className="mb-6">
                <span className="text-5xl font-bold">{plan.price}</span>
                <span className="text-muted-foreground">{plan.period}</span>
              </div>

              <ul className="space-y-3 mb-8 flex-1">
                {plan.features.map((feature) => (
                  <li key={feature} className="flex items-center gap-2 text-sm">
                    <Check className="h-4 w-4 text-primary shrink-0" />
                    {feature}
                  </li>
                ))}
              </ul>

              {plan.highlighted ? (
                <ShimmerButton className="w-full h-11">
                  {plan.cta}
                </ShimmerButton>
              ) : (
                <button className="w-full h-11 border rounded-lg font-medium hover:bg-muted transition-colors">
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

## 2. Pricing - With Toggle (Monthly/Annual)

Pricing with billing period toggle and savings badge.

```tsx
"use client"
import { useState } from "react"
import { cn } from "@/lib/utils"
import { Check } from "lucide-react"

export function PricingWithToggle() {
  const [annual, setAnnual] = useState(true)

  const plans = [
    {
      name: "Basic",
      monthlyPrice: 12,
      annualPrice: 9,
      features: ["5 projects", "10GB storage", "Basic support"],
    },
    {
      name: "Pro",
      monthlyPrice: 29,
      annualPrice: 24,
      features: ["Unlimited projects", "100GB storage", "Priority support", "API access"],
      popular: true,
    },
    {
      name: "Team",
      monthlyPrice: 79,
      annualPrice: 59,
      features: ["Everything in Pro", "Unlimited storage", "SSO", "Dedicated support"],
    },
  ]

  return (
    <section className="py-24 bg-muted/30">
      <div className="container mx-auto px-4">
        <div className="text-center mb-12">
          <h2 className="text-4xl font-bold mb-4">Pricing Plans</h2>
          
          {/* Toggle */}
          <div className="inline-flex items-center gap-4 mt-6">
            <span className={cn("text-sm", !annual && "text-muted-foreground")}>Monthly</span>
            <button
              onClick={() => setAnnual(!annual)}
              className={cn(
                "relative h-7 w-14 rounded-full transition-colors",
                annual ? "bg-primary" : "bg-muted"
              )}
            >
              <div
                className={cn(
                  "absolute top-1 h-5 w-5 rounded-full bg-white transition-transform",
                  annual ? "translate-x-8" : "translate-x-1"
                )}
              />
            </button>
            <span className={cn("text-sm", annual && "text-muted-foreground")}>
              Annual
              <span className="ml-1 text-xs text-green-600 font-medium">Save 20%</span>
            </span>
          </div>
        </div>

        <div className="grid md:grid-cols-3 gap-6 max-w-5xl mx-auto">
          {plans.map((plan) => (
            <div
              key={plan.name}
              className={cn(
                "rounded-2xl p-6 bg-background",
                plan.popular ? "border-2 border-primary ring-4 ring-primary/10" : "border"
              )}
            >
              {plan.popular && (
                <div className="text-xs font-medium text-primary mb-4">MOST POPULAR</div>
              )}
              
              <h3 className="text-xl font-bold">{plan.name}</h3>
              
              <div className="mt-4 mb-6">
                <span className="text-4xl font-bold">
                  ${annual ? plan.annualPrice : plan.monthlyPrice}
                </span>
                <span className="text-muted-foreground">/mo</span>
                {annual && (
                  <div className="text-sm text-muted-foreground">
                    billed annually
                  </div>
                )}
              </div>

              <ul className="space-y-2 mb-6">
                {plan.features.map((f) => (
                  <li key={f} className="flex items-center gap-2 text-sm">
                    <Check className="h-4 w-4 text-green-500" />
                    {f}
                  </li>
                ))}
              </ul>

              <button
                className={cn(
                  "w-full h-10 rounded-lg font-medium transition-colors",
                  plan.popular
                    ? "bg-primary text-primary-foreground hover:bg-primary/90"
                    : "border hover:bg-muted"
                )}
              >
                Get Started
              </button>
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## 3. Pricing - Comparison Table

Detailed feature comparison table.

```tsx
import { Check, Minus } from "lucide-react"
import { cn } from "@/lib/utils"

const features = [
  { name: "Projects", free: "3", pro: "Unlimited", enterprise: "Unlimited" },
  { name: "Storage", free: "1GB", pro: "50GB", enterprise: "Unlimited" },
  { name: "Team members", free: "1", pro: "10", enterprise: "Unlimited" },
  { name: "API access", free: false, pro: true, enterprise: true },
  { name: "Custom domains", free: false, pro: true, enterprise: true },
  { name: "Analytics", free: "Basic", pro: "Advanced", enterprise: "Advanced" },
  { name: "SSO/SAML", free: false, pro: false, enterprise: true },
  { name: "SLA", free: false, pro: false, enterprise: "99.99%" },
  { name: "Support", free: "Email", pro: "Priority", enterprise: "Dedicated" },
]

export function PricingComparison() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-4xl font-bold mb-4">Compare Plans</h2>
          <p className="text-muted-foreground">See what's included in each plan</p>
        </div>

        <div className="overflow-x-auto">
          <table className="w-full max-w-4xl mx-auto">
            <thead>
              <tr className="border-b">
                <th className="text-left py-4 px-4 font-medium">Features</th>
                <th className="text-center py-4 px-4">
                  <div className="font-bold">Free</div>
                  <div className="text-2xl font-bold">$0</div>
                </th>
                <th className="text-center py-4 px-4 bg-primary/5 rounded-t-lg">
                  <div className="text-primary font-bold">Pro</div>
                  <div className="text-2xl font-bold">$29/mo</div>
                </th>
                <th className="text-center py-4 px-4">
                  <div className="font-bold">Enterprise</div>
                  <div className="text-2xl font-bold">Custom</div>
                </th>
              </tr>
            </thead>
            <tbody>
              {features.map((feature, i) => (
                <tr key={feature.name} className={cn("border-b", i % 2 === 0 && "bg-muted/30")}>
                  <td className="py-4 px-4 font-medium">{feature.name}</td>
                  <td className="text-center py-4 px-4">
                    <FeatureValue value={feature.free} />
                  </td>
                  <td className="text-center py-4 px-4 bg-primary/5">
                    <FeatureValue value={feature.pro} />
                  </td>
                  <td className="text-center py-4 px-4">
                    <FeatureValue value={feature.enterprise} />
                  </td>
                </tr>
              ))}
            </tbody>
            <tfoot>
              <tr>
                <td className="py-6 px-4" />
                <td className="text-center py-6 px-4">
                  <button className="h-10 px-6 border rounded-lg font-medium hover:bg-muted">
                    Get Started
                  </button>
                </td>
                <td className="text-center py-6 px-4 bg-primary/5 rounded-b-lg">
                  <button className="h-10 px-6 bg-primary text-primary-foreground rounded-lg font-medium">
                    Upgrade to Pro
                  </button>
                </td>
                <td className="text-center py-6 px-4">
                  <button className="h-10 px-6 border rounded-lg font-medium hover:bg-muted">
                    Contact Sales
                  </button>
                </td>
              </tr>
            </tfoot>
          </table>
        </div>
      </div>
    </section>
  )
}

function FeatureValue({ value }: { value: boolean | string }) {
  if (value === true) return <Check className="h-5 w-5 text-green-500 mx-auto" />
  if (value === false) return <Minus className="h-5 w-5 text-muted-foreground mx-auto" />
  return <span>{value}</span>
}
```

---

## 4. Pricing - One-Time Payment (LTD)

Lifetime deal pricing for products like Magic UI Pro.

```tsx
import { Check, Sparkles } from "lucide-react"
import { ShimmerButton } from "@/components/magicui/shimmer-button"
import { BorderBeam } from "@/components/magicui/border-beam"

export function PricingLifetime() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="max-w-2xl mx-auto">
          <div className="relative rounded-3xl border-2 border-primary bg-gradient-to-b from-primary/10 to-transparent p-8 md:p-12">
            <BorderBeam size={300} duration={15} />
            
            {/* Badge */}
            <div className="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-primary text-primary-foreground text-sm font-medium mb-6">
              <Sparkles className="h-4 w-4" />
              Limited Time Offer
            </div>

            <h2 className="text-3xl md:text-4xl font-bold mb-2">
              Magic UI Pro
            </h2>
            <p className="text-muted-foreground mb-6">
              Get lifetime access to all components and templates
            </p>

            {/* Price */}
            <div className="flex items-baseline gap-2 mb-8">
              <span className="text-5xl md:text-6xl font-bold">$199</span>
              <span className="text-muted-foreground line-through">$399</span>
              <span className="px-2 py-1 bg-green-100 text-green-700 text-sm font-medium rounded">
                50% OFF
              </span>
            </div>

            {/* Features */}
            <ul className="grid md:grid-cols-2 gap-3 mb-8">
              {[
                "150+ premium components",
                "9 landing page templates",
                "Lifetime updates",
                "Commercial license",
                "Priority support",
                "Figma file included",
                "Next.js 15 ready",
                "Dark mode support",
              ].map((feature) => (
                <li key={feature} className="flex items-center gap-2">
                  <Check className="h-5 w-5 text-green-500 shrink-0" />
                  <span>{feature}</span>
                </li>
              ))}
            </ul>

            {/* CTA */}
            <ShimmerButton className="w-full h-14 text-lg">
              Get Lifetime Access →
            </ShimmerButton>

            <p className="text-center text-sm text-muted-foreground mt-4">
              30-day money-back guarantee • One-time payment
            </p>
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## Artifact-Ready Pricing Section

```jsx
export default function PricingDemo() {
  const [annual, setAnnual] = React.useState(true)

  const plans = [
    { name: "Starter", monthly: 9, annual: 7, features: ["3 projects", "1GB storage", "Basic support"], cta: "Start Free" },
    { name: "Pro", monthly: 29, annual: 24, features: ["Unlimited projects", "50GB storage", "Priority support", "API access", "Custom domains"], cta: "Get Started", popular: true },
    { name: "Enterprise", monthly: 99, annual: 79, features: ["Everything in Pro", "Unlimited storage", "SSO", "Dedicated support", "SLA"], cta: "Contact Sales" },
  ]

  return (
    <div className="min-h-screen bg-gray-950 text-white py-24 px-4">
      <div className="max-w-6xl mx-auto">
        {/* Header */}
        <div className="text-center mb-12">
          <h2 className="text-4xl font-bold mb-4">Simple, transparent pricing</h2>
          <p className="text-gray-400 mb-8">Choose the plan that's right for you</p>
          
          {/* Toggle */}
          <div className="inline-flex items-center gap-3 p-1 rounded-full bg-gray-800">
            <button
              onClick={() => setAnnual(false)}
              className={`px-4 py-2 rounded-full text-sm font-medium transition ${!annual ? 'bg-white text-black' : 'text-gray-400'}`}
            >
              Monthly
            </button>
            <button
              onClick={() => setAnnual(true)}
              className={`px-4 py-2 rounded-full text-sm font-medium transition ${annual ? 'bg-white text-black' : 'text-gray-400'}`}
            >
              Annual <span className="text-green-500 ml-1">-20%</span>
            </button>
          </div>
        </div>

        {/* Plans */}
        <div className="grid md:grid-cols-3 gap-6">
          {plans.map((plan) => (
            <div
              key={plan.name}
              className={`rounded-2xl p-8 ${plan.popular ? 'bg-gradient-to-b from-purple-900/50 to-gray-900 border-2 border-purple-500 ring-4 ring-purple-500/20' : 'bg-gray-900 border border-gray-800'}`}
            >
              {plan.popular && (
                <div className="text-purple-400 text-sm font-medium mb-4">✨ MOST POPULAR</div>
              )}
              
              <h3 className="text-xl font-bold mb-2">{plan.name}</h3>
              
              <div className="mb-6">
                <span className="text-4xl font-bold">${annual ? plan.annual : plan.monthly}</span>
                <span className="text-gray-400">/mo</span>
                {annual && <div className="text-sm text-gray-500">billed annually</div>}
              </div>

              <ul className="space-y-3 mb-8">
                {plan.features.map((f) => (
                  <li key={f} className="flex items-center gap-2 text-sm text-gray-300">
                    <span className="text-green-500">✓</span>
                    {f}
                  </li>
                ))}
              </ul>

              <button
                className={`w-full h-12 rounded-xl font-semibold transition ${
                  plan.popular
                    ? 'bg-white text-black hover:bg-gray-100'
                    : 'border border-gray-700 hover:bg-gray-800'
                }`}
              >
                {plan.cta}
              </button>
            </div>
          ))}
        </div>

        {/* Trust */}
        <p className="text-center text-gray-500 text-sm mt-12">
          🔒 Secure payments • Cancel anytime • 14-day free trial
        </p>
      </div>
    </div>
  )
}
```
