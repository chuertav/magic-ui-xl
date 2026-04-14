# Hero Sections Reference

Multiple hero section variants for different use cases.

---

## 1. Hero - Centered with Gradient Text

Classic centered hero with animated gradient headline.

```tsx
import { WordRotate } from "@/components/magicui/word-rotate"
import { ShimmerButton } from "@/components/magicui/shimmer-button"
import { DotPattern } from "@/components/magicui/dot-pattern"
import { AnimatedGradientText } from "@/components/magicui/animated-gradient-text"

export function HeroCentered() {
  return (
    <section className="relative min-h-screen flex items-center justify-center overflow-hidden">
      <DotPattern className="[mask-image:radial-gradient(500px_circle_at_center,white,transparent)]" />
      
      <div className="relative z-10 text-center px-4 max-w-4xl mx-auto">
        <AnimatedGradientText className="mb-6">
          ✨ Announcing our Series A
        </AnimatedGradientText>
        
        <h1 className="text-5xl md:text-7xl font-bold mb-6">
          Build{" "}
          <WordRotate
            words={["faster", "better", "smarter"]}
            className="text-primary"
          />
          <br />
          with our platform
        </h1>
        
        <p className="text-xl text-muted-foreground mb-10 max-w-2xl mx-auto">
          The modern way to build, deploy, and scale your applications.
          Trusted by thousands of developers worldwide.
        </p>
        
        <div className="flex flex-col sm:flex-row gap-4 justify-center">
          <ShimmerButton className="h-12 px-8">
            <span className="font-semibold">Get Started Free</span>
          </ShimmerButton>
          <button className="h-12 px-8 border rounded-full font-semibold hover:bg-muted">
            Watch Demo →
          </button>
        </div>
        
        <p className="mt-8 text-sm text-muted-foreground">
          No credit card required • Free 14-day trial
        </p>
      </div>
    </section>
  )
}
```

---

## 2. Hero - Split with Device Mockup

Hero with text on left, device mockup on right.

```tsx
import { Safari } from "@/components/magicui/safari"
import { BorderBeam } from "@/components/magicui/border-beam"
import { NumberTicker } from "@/components/magicui/number-ticker"

export function HeroSplit() {
  return (
    <section className="min-h-screen flex items-center py-20">
      <div className="container mx-auto px-4">
        <div className="grid lg:grid-cols-2 gap-12 items-center">
          {/* Left - Content */}
          <div>
            <div className="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-primary/10 text-primary text-sm mb-6">
              <span className="relative flex h-2 w-2">
                <span className="animate-ping absolute h-full w-full rounded-full bg-primary opacity-75" />
                <span className="relative rounded-full h-2 w-2 bg-primary" />
              </span>
              Now in Public Beta
            </div>
            
            <h1 className="text-4xl md:text-6xl font-bold mb-6 leading-tight">
              The Developer Platform for the Modern Web
            </h1>
            
            <p className="text-lg text-muted-foreground mb-8">
              Ship faster with our integrated development environment, 
              automated deployments, and real-time collaboration tools.
            </p>
            
            <div className="flex flex-wrap gap-4 mb-10">
              <button className="h-12 px-6 bg-primary text-primary-foreground rounded-lg font-semibold">
                Start Building
              </button>
              <button className="h-12 px-6 border rounded-lg font-semibold hover:bg-muted">
                Book a Demo
              </button>
            </div>
            
            {/* Stats */}
            <div className="flex gap-8">
              <div>
                <div className="text-3xl font-bold">
                  <NumberTicker value={50000} />+
                </div>
                <div className="text-sm text-muted-foreground">Developers</div>
              </div>
              <div>
                <div className="text-3xl font-bold">
                  <NumberTicker value={99.9} decimalPlaces={1} />%
                </div>
                <div className="text-sm text-muted-foreground">Uptime</div>
              </div>
              <div>
                <div className="text-3xl font-bold">
                  <NumberTicker value={500} />ms
                </div>
                <div className="text-sm text-muted-foreground">Avg Deploy</div>
              </div>
            </div>
          </div>
          
          {/* Right - Device Mockup */}
          <div className="relative">
            <div className="relative rounded-xl overflow-hidden shadow-2xl">
              <BorderBeam size={300} duration={10} />
              <Safari url="app.myplatform.com" src="/dashboard.png" />
            </div>
            
            {/* Floating elements */}
            <div className="absolute -top-4 -left-4 p-4 rounded-lg bg-background border shadow-lg">
              <div className="text-green-500 font-mono text-sm">✓ Deployed</div>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## 3. Hero - With Video Background

Immersive hero with video background.

```tsx
export function HeroVideo() {
  return (
    <section className="relative min-h-screen flex items-center justify-center overflow-hidden">
      {/* Video Background */}
      <video
        autoPlay
        loop
        muted
        playsInline
        className="absolute inset-0 w-full h-full object-cover"
      >
        <source src="/hero-video.mp4" type="video/mp4" />
      </video>
      
      {/* Overlay */}
      <div className="absolute inset-0 bg-black/60" />
      
      {/* Content */}
      <div className="relative z-10 text-center px-4 max-w-4xl mx-auto text-white">
        <h1 className="text-5xl md:text-7xl font-bold mb-6">
          Experience the Future
        </h1>
        
        <p className="text-xl opacity-90 mb-10 max-w-2xl mx-auto">
          Immersive experiences that transform how you work, play, and connect.
        </p>
        
        <div className="flex gap-4 justify-center">
          <button className="h-14 px-8 bg-white text-black rounded-full font-semibold hover:bg-gray-100">
            Get Early Access
          </button>
          <button className="h-14 px-8 border border-white rounded-full font-semibold hover:bg-white/10">
            Learn More
          </button>
        </div>
      </div>
      
      {/* Scroll indicator */}
      <div className="absolute bottom-8 left-1/2 -translate-x-1/2 animate-bounce">
        <svg className="w-6 h-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M19 14l-7 7m0 0l-7-7m7 7V3" />
        </svg>
      </div>
    </section>
  )
}
```

---

## 4. Hero - Product Hunt Style

Minimalist hero like Product Hunt launches.

```tsx
import { AvatarCircles } from "@/components/magicui/avatar-circles"
import { RainbowButton } from "@/components/magicui/rainbow-button"

export function HeroProductHunt() {
  return (
    <section className="min-h-[80vh] flex items-center py-20">
      <div className="container mx-auto px-4 max-w-3xl text-center">
        {/* Product Hunt Badge */}
        <a href="#" className="inline-flex items-center gap-2 px-4 py-2 rounded-full border bg-orange-50 text-orange-600 mb-8 hover:bg-orange-100">
          <span className="text-xl">🏆</span>
          <span className="font-medium">#1 Product of the Day</span>
        </a>
        
        <h1 className="text-4xl md:text-6xl font-bold mb-6">
          The simplest way to build your SaaS
        </h1>
        
        <p className="text-xl text-muted-foreground mb-8">
          Launch your product in days, not months. 
          Everything you need to go from idea to revenue.
        </p>
        
        <RainbowButton className="h-14 px-10 text-lg mb-8">
          Start for free →
        </RainbowButton>
        
        {/* Social Proof */}
        <div className="flex items-center justify-center gap-4">
          <AvatarCircles
            avatarUrls={[
              "https://avatar.vercel.sh/1",
              "https://avatar.vercel.sh/2",
              "https://avatar.vercel.sh/3",
              "https://avatar.vercel.sh/4",
              "https://avatar.vercel.sh/5",
            ]}
          />
          <div className="text-left">
            <div className="font-semibold">Join 5,000+ makers</div>
            <div className="text-sm text-muted-foreground">★★★★★ 4.9/5 rating</div>
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## 5. Hero - SaaS Dashboard Preview

Hero showcasing a dashboard with floating UI elements.

```tsx
import { Particles } from "@/components/magicui/particles"
import { MagicCard } from "@/components/magicui/magic-card"

export function HeroDashboard() {
  return (
    <section className="relative min-h-screen pt-32 pb-20 overflow-hidden bg-gradient-to-b from-background to-muted/30">
      <Particles className="absolute inset-0" quantity={30} />
      
      <div className="container mx-auto px-4 relative z-10">
        <div className="text-center mb-16">
          <h1 className="text-5xl md:text-7xl font-bold mb-6">
            Your command center<br />for everything
          </h1>
          <p className="text-xl text-muted-foreground max-w-2xl mx-auto">
            One dashboard to manage all your projects, teams, and workflows.
          </p>
        </div>
        
        {/* Dashboard Preview */}
        <div className="relative max-w-6xl mx-auto">
          {/* Main Dashboard Card */}
          <MagicCard className="p-0 overflow-hidden">
            <img src="/dashboard-full.png" alt="Dashboard" className="w-full" />
          </MagicCard>
          
          {/* Floating Cards */}
          <div className="absolute -left-8 top-1/4 p-4 rounded-xl bg-background border shadow-2xl animate-float">
            <div className="flex items-center gap-3">
              <div className="w-10 h-10 rounded-full bg-green-100 flex items-center justify-center">
                <span className="text-green-600">📈</span>
              </div>
              <div>
                <div className="text-sm text-muted-foreground">Revenue</div>
                <div className="font-bold">$48,239</div>
              </div>
            </div>
          </div>
          
          <div className="absolute -right-8 top-1/3 p-4 rounded-xl bg-background border shadow-2xl animate-float-delayed">
            <div className="flex items-center gap-3">
              <div className="w-10 h-10 rounded-full bg-blue-100 flex items-center justify-center">
                <span className="text-blue-600">👥</span>
              </div>
              <div>
                <div className="text-sm text-muted-foreground">Users</div>
                <div className="font-bold">12,847</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
```

**Required CSS:**
```css
@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
}

.animate-float {
  animation: float 3s ease-in-out infinite;
}

.animate-float-delayed {
  animation: float 3s ease-in-out infinite 1.5s;
}
```

---

## 6. Hero - Mobile App Launch

Hero optimized for mobile app launches.

```tsx
import { IPhone } from "@/components/magicui/iphone"
import { SparklesText } from "@/components/magicui/sparkles-text"

export function HeroMobileApp() {
  return (
    <section className="min-h-screen flex items-center py-20 bg-gradient-to-b from-background to-primary/5">
      <div className="container mx-auto px-4">
        <div className="grid lg:grid-cols-2 gap-12 items-center">
          {/* Content */}
          <div className="order-2 lg:order-1 text-center lg:text-left">
            <div className="inline-block px-4 py-1 rounded-full bg-primary/10 text-primary text-sm font-medium mb-6">
              📱 Now Available on iOS & Android
            </div>
            
            <h1 className="text-4xl md:text-6xl font-bold mb-6">
              Your life,{" "}
              <SparklesText>organized</SparklesText>
            </h1>
            
            <p className="text-lg text-muted-foreground mb-8 max-w-md mx-auto lg:mx-0">
              The all-in-one app that helps you manage tasks, habits, and goals. 
              Join 2 million users living their best lives.
            </p>
            
            {/* App Store Buttons */}
            <div className="flex flex-wrap gap-4 justify-center lg:justify-start mb-8">
              <a href="#" className="h-14 px-6 bg-black text-white rounded-xl flex items-center gap-3 hover:bg-gray-800">
                <svg className="w-8 h-8" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z"/>
                </svg>
                <div className="text-left">
                  <div className="text-[10px] opacity-80">Download on the</div>
                  <div className="text-lg font-semibold -mt-1">App Store</div>
                </div>
              </a>
              
              <a href="#" className="h-14 px-6 bg-black text-white rounded-xl flex items-center gap-3 hover:bg-gray-800">
                <svg className="w-7 h-7" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M3,20.5V3.5C3,2.91 3.34,2.39 3.84,2.15L13.69,12L3.84,21.85C3.34,21.6 3,21.09 3,20.5M16.81,15.12L6.05,21.34L14.54,12.85L16.81,15.12M20.16,10.81C20.5,11.08 20.75,11.5 20.75,12C20.75,12.5 20.53,12.9 20.18,13.18L17.89,14.5L15.39,12L17.89,9.5L20.16,10.81M6.05,2.66L16.81,8.88L14.54,11.15L6.05,2.66Z"/>
                </svg>
                <div className="text-left">
                  <div className="text-[10px] opacity-80">GET IT ON</div>
                  <div className="text-lg font-semibold -mt-1">Google Play</div>
                </div>
              </a>
            </div>
            
            {/* Rating */}
            <div className="flex items-center gap-2 justify-center lg:justify-start text-sm text-muted-foreground">
              <span className="text-yellow-500">★★★★★</span>
              <span>4.9 rating • 50K+ reviews</span>
            </div>
          </div>
          
          {/* Phone Mockup */}
          <div className="order-1 lg:order-2 flex justify-center">
            <IPhone src="/app-screenshot.png" />
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## Artifact-Ready Hero Section

```jsx
export default function HeroDemo() {
  const [wordIndex, setWordIndex] = React.useState(0)
  const words = ["faster", "better", "smarter", "easier"]

  React.useEffect(() => {
    const interval = setInterval(() => {
      setWordIndex((i) => (i + 1) % words.length)
    }, 2500)
    return () => clearInterval(interval)
  }, [])

  return (
    <div className="min-h-screen bg-black text-white overflow-hidden">
      <style>{`
        @keyframes gradient-shift {
          0%, 100% { background-position: 0% 50%; }
          50% { background-position: 100% 50%; }
        }
        @keyframes word-swap {
          0% { opacity: 0; transform: translateY(20px); }
          100% { opacity: 1; transform: translateY(0); }
        }
      `}</style>

      {/* Dot Pattern */}
      <div className="absolute inset-0 opacity-20">
        <svg className="w-full h-full">
          <defs>
            <pattern id="dots" width="20" height="20" patternUnits="userSpaceOnUse">
              <circle cx="2" cy="2" r="1" fill="white" />
            </pattern>
            <radialGradient id="mask" cx="50%" cy="50%" r="50%">
              <stop offset="0%" stopColor="white" />
              <stop offset="100%" stopColor="black" />
            </radialGradient>
          </defs>
          <rect width="100%" height="100%" fill="url(#dots)" mask="url(#mask)" />
        </svg>
      </div>

      <div className="relative z-10 min-h-screen flex items-center justify-center px-4">
        <div className="text-center max-w-4xl">
          {/* Badge */}
          <div 
            className="inline-flex items-center gap-2 px-4 py-2 rounded-full mb-8 text-sm"
            style={{
              background: 'linear-gradient(90deg, rgba(147,51,234,0.2), rgba(236,72,153,0.2))',
              border: '1px solid rgba(147,51,234,0.3)',
            }}
          >
            <span className="relative flex h-2 w-2">
              <span className="animate-ping absolute h-full w-full rounded-full bg-purple-400 opacity-75" />
              <span className="relative rounded-full h-2 w-2 bg-purple-500" />
            </span>
            <span className="text-purple-300">Introducing v2.0</span>
          </div>

          {/* Headline */}
          <h1 className="text-5xl md:text-7xl font-bold mb-6 leading-tight">
            Build products{" "}
            <span
              key={wordIndex}
              className="inline-block"
              style={{
                background: 'linear-gradient(90deg, #9333ea, #ec4899, #9333ea)',
                backgroundSize: '200% auto',
                WebkitBackgroundClip: 'text',
                WebkitTextFillColor: 'transparent',
                animation: 'gradient-shift 3s linear infinite, word-swap 0.3s ease-out',
              }}
            >
              {words[wordIndex]}
            </span>
            <br />
            <span className="text-gray-500">with Magic UI</span>
          </h1>

          {/* Subheadline */}
          <p className="text-xl text-gray-400 mb-10 max-w-2xl mx-auto">
            150+ beautifully designed, animated components. Copy, paste, customize.
            Built with React, Tailwind CSS, and Framer Motion.
          </p>

          {/* CTAs */}
          <div className="flex flex-col sm:flex-row gap-4 justify-center mb-8">
            <button className="h-14 px-8 bg-white text-black rounded-full font-semibold text-lg hover:bg-gray-100 transition">
              Get Started Free
            </button>
            <button className="h-14 px-8 border border-white/20 rounded-full font-semibold text-lg hover:bg-white/5 transition">
              View Components →
            </button>
          </div>

          {/* Trust */}
          <p className="text-sm text-gray-500">
            Trusted by 10,000+ developers • No credit card required
          </p>
        </div>
      </div>
    </div>
  )
}
```
