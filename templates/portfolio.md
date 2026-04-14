# Portfolio Landing Page Template

Complete template for personal portfolios, agencies, and creative professionals.

---

## Page Structure

```tsx
// Portfolio Landing - Key Sections
// 1. Header (minimal, name-focused)
// 2. Hero (intro + profile)
// 3. Work/Projects Showcase
// 4. Skills/Services
// 5. About Section
// 6. Testimonials
// 7. Contact CTA
// 8. Footer
```

---

## Hero - Personal Introduction

```tsx
import { SparklesText } from "@/components/magicui/sparkles-text"
import { DotPattern } from "@/components/magicui/dot-pattern"
import { AvatarCircles } from "@/components/magicui/avatar-circles"

export function PortfolioHero() {
  return (
    <section className="relative min-h-screen flex items-center pt-20">
      <DotPattern className="[mask-image:radial-gradient(600px_circle_at_center,white,transparent)]" />
      
      <div className="container mx-auto px-4 relative z-10">
        <div className="max-w-3xl">
          {/* Status Badge */}
          <div className="inline-flex items-center gap-2 px-3 py-1 rounded-full border bg-green-50 text-green-700 text-sm mb-6">
            <span className="relative flex h-2 w-2">
              <span className="animate-ping absolute h-full w-full rounded-full bg-green-400 opacity-75" />
              <span className="relative rounded-full h-2 w-2 bg-green-500" />
            </span>
            Available for freelance work
          </div>

          {/* Main Headline */}
          <h1 className="text-5xl md:text-7xl font-bold mb-6">
            Hi, I'm Alex 👋
            <br />
            I design & build{" "}
            <SparklesText>digital products</SparklesText>
          </h1>

          <p className="text-xl text-muted-foreground mb-8 max-w-xl">
            Full-stack developer and UI/UX designer with 8+ years of experience 
            crafting beautiful, functional web applications.
          </p>

          {/* CTAs */}
          <div className="flex flex-wrap gap-4 mb-12">
            <a href="#work" className="h-12 px-6 bg-primary text-primary-foreground rounded-full font-semibold flex items-center">
              View My Work →
            </a>
            <a href="#contact" className="h-12 px-6 border rounded-full font-semibold flex items-center hover:bg-muted">
              Get in Touch
            </a>
          </div>

          {/* Social Proof */}
          <div className="flex items-center gap-4">
            <AvatarCircles
              avatarUrls={[
                "https://avatar.vercel.sh/stripe",
                "https://avatar.vercel.sh/vercel", 
                "https://avatar.vercel.sh/linear",
                "https://avatar.vercel.sh/notion",
              ]}
            />
            <span className="text-sm text-muted-foreground">
              Trusted by teams at Stripe, Vercel, Linear & more
            </span>
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## Projects Showcase - BentoGrid

```tsx
import { BentoGrid, BentoCard } from "@/components/magicui/bento-grid"
import { BorderBeam } from "@/components/magicui/border-beam"
import { Safari } from "@/components/magicui/safari"

const projects = [
  {
    title: "E-commerce Platform",
    description: "Full-stack e-commerce solution with AI-powered recommendations",
    image: "/projects/ecommerce.png",
    tags: ["Next.js", "Stripe", "AI"],
    link: "#",
    className: "md:col-span-2",
  },
  {
    title: "SaaS Dashboard",
    description: "Analytics dashboard for a fintech startup",
    image: "/projects/dashboard.png",
    tags: ["React", "D3.js", "TypeScript"],
    link: "#",
    className: "md:col-span-1",
  },
  {
    title: "Mobile App",
    description: "Cross-platform fitness tracking application",
    image: "/projects/mobile.png",
    tags: ["React Native", "Firebase"],
    link: "#",
    className: "md:col-span-1",
  },
  {
    title: "Design System",
    description: "Comprehensive component library for enterprise",
    image: "/projects/design-system.png",
    tags: ["Figma", "Storybook", "Tailwind"],
    link: "#",
    className: "md:col-span-2",
  },
]

export function ProjectsShowcase() {
  return (
    <section id="work" className="py-24">
      <div className="container mx-auto px-4">
        <div className="mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">Selected Work</h2>
          <p className="text-lg text-muted-foreground">
            A collection of projects I'm proud of
          </p>
        </div>

        <div className="grid md:grid-cols-3 gap-6">
          {projects.map((project) => (
            <a
              key={project.title}
              href={project.link}
              className={`group relative rounded-2xl border bg-background overflow-hidden ${project.className}`}
            >
              <BorderBeam size={200} duration={15} className="opacity-0 group-hover:opacity-100" />
              
              {/* Image */}
              <div className="aspect-video overflow-hidden">
                <img
                  src={project.image}
                  alt={project.title}
                  className="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105"
                />
              </div>
              
              {/* Content */}
              <div className="p-6">
                <h3 className="text-xl font-bold mb-2 group-hover:text-primary transition-colors">
                  {project.title}
                </h3>
                <p className="text-muted-foreground mb-4">{project.description}</p>
                <div className="flex flex-wrap gap-2">
                  {project.tags.map((tag) => (
                    <span key={tag} className="px-2 py-1 text-xs bg-muted rounded-full">
                      {tag}
                    </span>
                  ))}
                </div>
              </div>
            </a>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## Skills/Services Section

```tsx
import { MagicCard } from "@/components/magicui/magic-card"
import { Code, Palette, Smartphone, Zap } from "lucide-react"

const services = [
  {
    icon: Code,
    title: "Web Development",
    description: "Full-stack applications built with modern technologies. React, Next.js, Node.js, and more.",
  },
  {
    icon: Palette,
    title: "UI/UX Design",
    description: "User-centered design that looks beautiful and converts. From wireframes to high-fidelity mockups.",
  },
  {
    icon: Smartphone,
    title: "Mobile Apps",
    description: "Cross-platform mobile applications with React Native. iOS and Android from a single codebase.",
  },
  {
    icon: Zap,
    title: "Performance",
    description: "Optimization and audits to make your existing applications faster and more efficient.",
  },
]

export function ServicesSection() {
  return (
    <section className="py-24 bg-muted/30">
      <div className="container mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">What I Do</h2>
          <p className="text-lg text-muted-foreground">
            Services I offer to help bring your ideas to life
          </p>
        </div>

        <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-6 max-w-5xl mx-auto">
          {services.map((service) => (
            <MagicCard key={service.title} className="p-6 text-center">
              <service.icon className="h-10 w-10 text-primary mx-auto mb-4" />
              <h3 className="text-lg font-bold mb-2">{service.title}</h3>
              <p className="text-sm text-muted-foreground">{service.description}</p>
            </MagicCard>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## About Section

```tsx
import { NumberTicker } from "@/components/magicui/number-ticker"

export function AboutSection() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="grid lg:grid-cols-2 gap-12 items-center max-w-5xl mx-auto">
          {/* Image */}
          <div className="relative">
            <div className="aspect-square rounded-2xl overflow-hidden">
              <img
                src="/about-photo.jpg"
                alt="Profile"
                className="w-full h-full object-cover"
              />
            </div>
            {/* Floating Card */}
            <div className="absolute -bottom-6 -right-6 p-4 rounded-xl bg-background border shadow-lg">
              <div className="text-3xl font-bold">
                <NumberTicker value={8} />+ years
              </div>
              <div className="text-sm text-muted-foreground">of experience</div>
            </div>
          </div>

          {/* Content */}
          <div>
            <h2 className="text-3xl md:text-4xl font-bold mb-6">About Me</h2>
            <p className="text-lg text-muted-foreground mb-6">
              I'm a designer and developer based in San Francisco. I specialize in 
              creating digital experiences that are both beautiful and functional.
            </p>
            <p className="text-lg text-muted-foreground mb-8">
              When I'm not coding, you'll find me hiking, reading, or experimenting 
              with new coffee brewing methods. I believe great design should feel 
              invisible — it should just work.
            </p>

            {/* Stats */}
            <div className="grid grid-cols-3 gap-6">
              <div>
                <div className="text-3xl font-bold"><NumberTicker value={50} />+</div>
                <div className="text-sm text-muted-foreground">Projects</div>
              </div>
              <div>
                <div className="text-3xl font-bold"><NumberTicker value={30} />+</div>
                <div className="text-sm text-muted-foreground">Clients</div>
              </div>
              <div>
                <div className="text-3xl font-bold"><NumberTicker value={5} /></div>
                <div className="text-sm text-muted-foreground">Awards</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## Contact CTA

```tsx
import { Particles } from "@/components/magicui/particles"
import { BorderBeam } from "@/components/magicui/border-beam"
import { ShimmerButton } from "@/components/magicui/shimmer-button"

export function ContactCTA() {
  return (
    <section id="contact" className="py-24 relative overflow-hidden">
      <Particles className="absolute inset-0" quantity={30} />
      
      <div className="container mx-auto px-4 relative z-10">
        <div className="relative max-w-2xl mx-auto rounded-3xl border bg-background p-12 text-center overflow-hidden">
          <BorderBeam size={300} duration={15} />
          
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            Let's work together
          </h2>
          <p className="text-lg text-muted-foreground mb-8">
            Have a project in mind? I'd love to hear about it. 
            Send me a message and let's create something amazing.
          </p>

          <div className="flex flex-col sm:flex-row gap-4 justify-center">
            <ShimmerButton className="h-12 px-8">
              <span className="font-semibold">hello@alex.dev</span>
            </ShimmerButton>
            <a
              href="/resume.pdf"
              className="h-12 px-8 border rounded-full font-semibold flex items-center justify-center hover:bg-muted"
            >
              Download Resume
            </a>
          </div>

          {/* Social Links */}
          <div className="flex justify-center gap-6 mt-8">
            {["Twitter", "GitHub", "LinkedIn", "Dribbble"].map((social) => (
              <a
                key={social}
                href="#"
                className="text-sm text-muted-foreground hover:text-foreground transition"
              >
                {social}
              </a>
            ))}
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## Complete Portfolio Template (Artifact-Ready)

```jsx
export default function PortfolioLanding() {
  const projects = [
    { title: "E-commerce Platform", desc: "Full-stack shop with AI recommendations", tags: ["Next.js", "Stripe"], span: 2 },
    { title: "SaaS Dashboard", desc: "Analytics for fintech", tags: ["React", "D3.js"], span: 1 },
    { title: "Mobile App", desc: "Fitness tracking app", tags: ["React Native"], span: 1 },
    { title: "Design System", desc: "Enterprise component library", tags: ["Figma", "Tailwind"], span: 2 },
  ]

  return (
    <div className="min-h-screen bg-white">
      <style>{`
        @keyframes sparkle { 0%, 100% { opacity: 1; } 50% { opacity: 0.5; } }
      `}</style>

      {/* Header */}
      <header className="fixed top-0 z-50 w-full bg-white/80 backdrop-blur-lg border-b">
        <div className="max-w-6xl mx-auto px-4 h-16 flex items-center justify-between">
          <span className="text-xl font-bold">Alex.dev</span>
          <nav className="hidden md:flex gap-8 text-sm text-gray-600">
            <a href="#work">Work</a>
            <a href="#about">About</a>
            <a href="#contact">Contact</a>
          </nav>
          <a href="#contact" className="px-4 py-2 bg-black text-white text-sm rounded-full">Hire Me</a>
        </div>
      </header>

      {/* Hero */}
      <section className="min-h-screen flex items-center pt-16 px-4">
        <div className="max-w-3xl mx-auto">
          <div className="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-green-50 text-green-700 text-sm mb-6">
            <span className="relative flex h-2 w-2">
              <span className="animate-ping absolute h-full w-full rounded-full bg-green-400 opacity-75" />
              <span className="relative rounded-full h-2 w-2 bg-green-500" />
            </span>
            Available for freelance
          </div>

          <h1 className="text-5xl md:text-7xl font-bold mb-6">
            Hi, I'm Alex 👋<br />
            I build{" "}
            <span className="bg-gradient-to-r from-purple-600 to-pink-600 bg-clip-text text-transparent">
              digital products
            </span>
          </h1>

          <p className="text-xl text-gray-600 mb-8">
            Full-stack developer & designer with 8+ years crafting beautiful web apps.
          </p>

          <div className="flex gap-4">
            <a href="#work" className="h-12 px-6 bg-black text-white rounded-full font-medium flex items-center">
              View My Work →
            </a>
            <a href="#contact" className="h-12 px-6 border rounded-full font-medium flex items-center hover:bg-gray-50">
              Get in Touch
            </a>
          </div>
        </div>
      </section>

      {/* Projects */}
      <section id="work" className="py-24 px-4 bg-gray-50">
        <div className="max-w-6xl mx-auto">
          <h2 className="text-3xl font-bold mb-4">Selected Work</h2>
          <p className="text-gray-600 mb-12">Projects I'm proud of</p>

          <div className="grid md:grid-cols-3 gap-6">
            {projects.map((p) => (
              <div
                key={p.title}
                className={`group bg-white rounded-2xl border overflow-hidden hover:shadow-lg transition ${
                  p.span === 2 ? 'md:col-span-2' : ''
                }`}
              >
                <div className="aspect-video bg-gradient-to-br from-purple-100 to-pink-100 flex items-center justify-center">
                  <span className="text-4xl">🖼️</span>
                </div>
                <div className="p-6">
                  <h3 className="font-bold text-lg mb-2 group-hover:text-purple-600 transition">{p.title}</h3>
                  <p className="text-gray-600 text-sm mb-4">{p.desc}</p>
                  <div className="flex gap-2">
                    {p.tags.map((t) => (
                      <span key={t} className="px-2 py-1 text-xs bg-gray-100 rounded-full">{t}</span>
                    ))}
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Services */}
      <section className="py-24 px-4">
        <div className="max-w-4xl mx-auto text-center">
          <h2 className="text-3xl font-bold mb-12">What I Do</h2>
          <div className="grid md:grid-cols-3 gap-8">
            {[
              { icon: "💻", title: "Development", desc: "React, Next.js, Node.js" },
              { icon: "🎨", title: "Design", desc: "UI/UX, Figma, Prototyping" },
              { icon: "📱", title: "Mobile", desc: "React Native, iOS, Android" },
            ].map((s) => (
              <div key={s.title} className="p-6 rounded-2xl border hover:shadow-md transition">
                <span className="text-4xl mb-4 block">{s.icon}</span>
                <h3 className="font-bold mb-2">{s.title}</h3>
                <p className="text-sm text-gray-600">{s.desc}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Contact */}
      <section id="contact" className="py-24 px-4">
        <div className="max-w-2xl mx-auto bg-gradient-to-br from-purple-600 to-pink-600 rounded-3xl p-12 text-center text-white">
          <h2 className="text-4xl font-bold mb-4">Let's work together</h2>
          <p className="text-lg opacity-90 mb-8">Have a project? Let's create something amazing.</p>
          <a href="mailto:hello@alex.dev" className="inline-block h-14 px-10 bg-white text-purple-600 rounded-full font-semibold leading-[56px]">
            hello@alex.dev
          </a>
          <div className="flex justify-center gap-6 mt-8 text-sm opacity-80">
            {["Twitter", "GitHub", "LinkedIn"].map((s) => (
              <a key={s} href="#" className="hover:opacity-100">{s}</a>
            ))}
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="py-8 border-t px-4">
        <div className="max-w-6xl mx-auto flex justify-between items-center text-sm text-gray-500">
          <span>© 2024 Alex. All rights reserved.</span>
          <span>Made with ❤️</span>
        </div>
      </footer>
    </div>
  )
}
```
