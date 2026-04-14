# Mobile App Landing Page Template

Complete template optimized for mobile app launches (iOS/Android).

---

## Page Structure

```tsx
// Mobile App Landing - Key Sections
// 1. Header (minimal, app-focused)
// 2. Hero (phone mockup + app store badges)
// 3. Feature Showcase (phone screenshots)
// 4. App Screens Carousel
// 5. Key Features Grid
// 6. Testimonials/Reviews
// 7. Download CTA
// 8. FAQ
// 9. Footer
```

---

## Hero - Phone Mockup Center Stage

```tsx
import { IPhone } from "@/components/magicui/iphone"
import { SparklesText } from "@/components/magicui/sparkles-text"
import { Particles } from "@/components/magicui/particles"

export function MobileHero() {
  return (
    <section className="relative min-h-screen flex items-center pt-20 overflow-hidden bg-gradient-to-b from-background to-primary/5">
      <Particles className="absolute inset-0" quantity={30} />
      
      <div className="container mx-auto px-4 relative z-10">
        <div className="grid lg:grid-cols-2 gap-12 items-center">
          {/* Content */}
          <div className="text-center lg:text-left order-2 lg:order-1">
            <div className="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-primary/10 text-primary text-sm font-medium mb-6">
              📱 Now on iOS & Android
            </div>

            <h1 className="text-4xl md:text-5xl lg:text-6xl font-bold mb-6">
              Your life,{" "}
              <SparklesText>beautifully organized</SparklesText>
            </h1>

            <p className="text-lg text-muted-foreground mb-8 max-w-lg mx-auto lg:mx-0">
              The #1 productivity app that helps you manage tasks, build habits, 
              and achieve your goals. Join 2 million happy users.
            </p>

            {/* App Store Badges */}
            <div className="flex flex-wrap gap-4 justify-center lg:justify-start mb-8">
              <AppStoreBadge store="ios" />
              <AppStoreBadge store="android" />
            </div>

            {/* Rating */}
            <div className="flex items-center gap-3 justify-center lg:justify-start">
              <div className="flex text-yellow-500">
                {"★★★★★".split("").map((s, i) => <span key={i}>{s}</span>)}
              </div>
              <span className="text-sm text-muted-foreground">
                4.9 rating • 50,000+ reviews
              </span>
            </div>
          </div>

          {/* Phone Mockup */}
          <div className="order-1 lg:order-2 flex justify-center">
            <div className="relative">
              <IPhone src="/app-home-screen.png" />
              
              {/* Floating badges */}
              <div className="absolute -left-8 top-1/4 px-3 py-2 rounded-lg bg-background border shadow-lg animate-float">
                <div className="flex items-center gap-2">
                  <span className="text-green-500">✓</span>
                  <span className="text-sm font-medium">Task completed!</span>
                </div>
              </div>
              
              <div className="absolute -right-8 top-1/2 px-3 py-2 rounded-lg bg-background border shadow-lg animate-float-delayed">
                <div className="flex items-center gap-2">
                  <span className="text-2xl">🔥</span>
                  <span className="text-sm font-medium">7 day streak!</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}

function AppStoreBadge({ store }: { store: "ios" | "android" }) {
  if (store === "ios") {
    return (
      <a href="#" className="h-14 px-6 bg-black text-white rounded-xl flex items-center gap-3 hover:bg-gray-800 transition">
        <svg className="w-8 h-8" viewBox="0 0 24 24" fill="currentColor">
          <path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z"/>
        </svg>
        <div className="text-left">
          <div className="text-[10px] opacity-80">Download on the</div>
          <div className="text-lg font-semibold -mt-1">App Store</div>
        </div>
      </a>
    )
  }
  
  return (
    <a href="#" className="h-14 px-6 bg-black text-white rounded-xl flex items-center gap-3 hover:bg-gray-800 transition">
      <svg className="w-7 h-7" viewBox="0 0 24 24" fill="currentColor">
        <path d="M3,20.5V3.5C3,2.91 3.34,2.39 3.84,2.15L13.69,12L3.84,21.85C3.34,21.6 3,21.09 3,20.5M16.81,15.12L6.05,21.34L14.54,12.85L16.81,15.12M20.16,10.81C20.5,11.08 20.75,11.5 20.75,12C20.75,12.5 20.53,12.9 20.18,13.18L17.89,14.5L15.39,12L17.89,9.5L20.16,10.81M6.05,2.66L16.81,8.88L14.54,11.15L6.05,2.66Z"/>
      </svg>
      <div className="text-left">
        <div className="text-[10px] opacity-80">GET IT ON</div>
        <div className="text-lg font-semibold -mt-1">Google Play</div>
      </div>
    </a>
  )
}
```

---

## App Screenshots Carousel

```tsx
import { IPhone } from "@/components/magicui/iphone"
import { Marquee } from "@/components/magicui/marquee"

const screens = [
  { title: "Dashboard", image: "/screens/dashboard.png" },
  { title: "Tasks", image: "/screens/tasks.png" },
  { title: "Calendar", image: "/screens/calendar.png" },
  { title: "Analytics", image: "/screens/analytics.png" },
  { title: "Settings", image: "/screens/settings.png" },
]

export function ScreensCarousel() {
  return (
    <section className="py-24 overflow-hidden">
      <div className="container mx-auto px-4 mb-12">
        <h2 className="text-3xl md:text-4xl font-bold text-center mb-4">
          Beautifully designed screens
        </h2>
        <p className="text-lg text-muted-foreground text-center">
          Every pixel crafted with care
        </p>
      </div>

      <Marquee pauseOnHover className="[--duration:40s]">
        {screens.map((screen) => (
          <div key={screen.title} className="mx-4">
            <IPhone src={screen.image} className="scale-90" />
            <p className="text-center mt-4 font-medium">{screen.title}</p>
          </div>
        ))}
      </Marquee>
    </section>
  )
}
```

---

## Feature Showcase - Phone + Text

```tsx
import { IPhone } from "@/components/magicui/iphone"
import { BorderBeam } from "@/components/magicui/border-beam"

const features = [
  {
    title: "Smart Task Management",
    description: "AI-powered task prioritization that learns your habits and helps you focus on what matters most.",
    screen: "/screens/tasks.png",
    benefits: ["Auto-prioritization", "Smart reminders", "Natural language input"],
  },
  {
    title: "Habit Tracking",
    description: "Build lasting habits with streaks, insights, and gentle nudges to keep you on track.",
    screen: "/screens/habits.png",
    benefits: ["Visual streaks", "Daily insights", "Flexible scheduling"],
    reverse: true,
  },
  {
    title: "Goal Planning",
    description: "Break down big goals into achievable milestones. Track progress and celebrate wins.",
    screen: "/screens/goals.png",
    benefits: ["Milestone tracking", "Progress visualization", "Achievement badges"],
  },
]

export function FeatureShowcase() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <div className="space-y-32">
          {features.map((feature, i) => (
            <div
              key={feature.title}
              className={`grid lg:grid-cols-2 gap-12 items-center ${
                feature.reverse ? "lg:flex-row-reverse" : ""
              }`}
            >
              {/* Phone */}
              <div className={`flex justify-center ${feature.reverse ? "lg:order-2" : ""}`}>
                <div className="relative">
                  <IPhone src={feature.screen} />
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
                  {feature.benefits.map((benefit) => (
                    <li key={benefit} className="flex items-center gap-3">
                      <span className="w-6 h-6 rounded-full bg-primary/10 text-primary flex items-center justify-center text-sm">
                        ✓
                      </span>
                      <span>{benefit}</span>
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

## App Reviews Section

```tsx
import { Marquee } from "@/components/magicui/marquee"

const reviews = [
  { name: "Sarah M.", rating: 5, text: "This app changed my life! I'm so much more productive now.", avatar: "👩" },
  { name: "John D.", rating: 5, text: "Finally an app that actually helps me stay organized.", avatar: "👨" },
  { name: "Emily R.", rating: 5, text: "The habit tracking is amazing. 50 day streak and counting!", avatar: "👩‍🦰" },
  { name: "Mike T.", rating: 5, text: "Best productivity app I've ever used. Worth every penny.", avatar: "🧔" },
  { name: "Lisa W.", rating: 5, text: "Beautiful design and so intuitive. Highly recommend!", avatar: "👩‍💼" },
  { name: "Alex K.", rating: 5, text: "The AI features are game-changing. It knows what I need.", avatar: "🧑‍💻" },
]

export function AppReviews() {
  return (
    <section className="py-24 bg-muted/30">
      <div className="container mx-auto px-4 mb-12">
        <h2 className="text-3xl md:text-4xl font-bold text-center mb-4">
          Loved by millions
        </h2>
        <p className="text-lg text-muted-foreground text-center">
          See what our users are saying
        </p>
      </div>

      <Marquee pauseOnHover className="[--duration:50s]">
        {reviews.map((review) => (
          <div
            key={review.name}
            className="w-80 p-6 mx-3 rounded-2xl border bg-background shadow-sm"
          >
            <div className="flex items-center gap-3 mb-3">
              <span className="text-3xl">{review.avatar}</span>
              <div>
                <div className="font-semibold">{review.name}</div>
                <div className="text-yellow-500 text-sm">
                  {"★".repeat(review.rating)}
                </div>
              </div>
            </div>
            <p className="text-muted-foreground">"{review.text}"</p>
          </div>
        ))}
      </Marquee>
    </section>
  )
}
```

---

## Download CTA Section

```tsx
import { IPhone } from "@/components/magicui/iphone"
import { BorderBeam } from "@/components/magicui/border-beam"
import { Particles } from "@/components/magicui/particles"

export function DownloadCTA() {
  return (
    <section className="py-24 relative overflow-hidden">
      <Particles className="absolute inset-0" quantity={50} />
      
      <div className="container mx-auto px-4 relative z-10">
        <div className="relative max-w-5xl mx-auto rounded-3xl bg-gradient-to-br from-primary via-primary to-purple-600 p-12 md:p-16 overflow-hidden">
          <BorderBeam size={400} duration={20} colorFrom="#fff" colorTo="#fff" />
          
          <div className="grid md:grid-cols-2 gap-8 items-center">
            {/* Content */}
            <div className="text-white">
              <h2 className="text-3xl md:text-4xl font-bold mb-4">
                Download now and start your journey
              </h2>
              <p className="text-lg opacity-90 mb-8">
                Join 2 million users who have transformed their productivity. 
                Free to download, premium features available.
              </p>
              
              <div className="flex flex-wrap gap-4">
                <a href="#" className="h-14 px-6 bg-white text-black rounded-xl flex items-center gap-3 hover:bg-gray-100 transition">
                  <span className="text-2xl">🍎</span>
                  <div className="text-left">
                    <div className="text-[10px]">Download on</div>
                    <div className="font-semibold -mt-1">App Store</div>
                  </div>
                </a>
                <a href="#" className="h-14 px-6 bg-white text-black rounded-xl flex items-center gap-3 hover:bg-gray-100 transition">
                  <span className="text-2xl">🤖</span>
                  <div className="text-left">
                    <div className="text-[10px]">Get it on</div>
                    <div className="font-semibold -mt-1">Google Play</div>
                  </div>
                </a>
              </div>
            </div>

            {/* Phone */}
            <div className="hidden md:flex justify-center">
              <div className="relative -mb-32">
                <IPhone src="/app-home-screen.png" />
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

## Complete Mobile App Template (Artifact-Ready)

```jsx
export default function MobileAppLanding() {
  const reviews = [
    { name: "Sarah", text: "Changed my life!", avatar: "👩", rating: 5 },
    { name: "Mike", text: "Best app ever!", avatar: "👨", rating: 5 },
    { name: "Emily", text: "50 day streak!", avatar: "👩‍🦰", rating: 5 },
    { name: "Alex", text: "AI is amazing!", avatar: "🧑‍💻", rating: 5 },
  ]

  return (
    <div className="min-h-screen bg-gradient-to-b from-purple-50 to-white">
      <style>{`
        @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
        @keyframes marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }
      `}</style>

      {/* Header */}
      <header className="fixed top-0 z-50 w-full bg-white/80 backdrop-blur-lg border-b">
        <div className="max-w-6xl mx-auto px-4 h-16 flex items-center justify-between">
          <span className="text-xl font-bold">📱 LifeOS</span>
          <button className="px-4 py-2 bg-purple-600 text-white text-sm rounded-full">Download</button>
        </div>
      </header>

      {/* Hero */}
      <section className="pt-32 pb-20 px-4">
        <div className="max-w-6xl mx-auto grid lg:grid-cols-2 gap-12 items-center">
          {/* Content */}
          <div className="text-center lg:text-left">
            <div className="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-purple-100 text-purple-700 text-sm mb-6">
              📱 Now on iOS & Android
            </div>
            
            <h1 className="text-5xl font-bold mb-6">
              Your life, <span className="text-purple-600">beautifully organized</span>
            </h1>
            
            <p className="text-xl text-gray-600 mb-8">
              The #1 productivity app. Join 2 million happy users.
            </p>

            {/* App Store Buttons */}
            <div className="flex flex-wrap gap-4 justify-center lg:justify-start mb-6">
              <button className="h-14 px-6 bg-black text-white rounded-xl flex items-center gap-3">
                <span className="text-2xl">🍎</span>
                <div className="text-left">
                  <div className="text-[10px] opacity-80">Download on</div>
                  <div className="font-semibold">App Store</div>
                </div>
              </button>
              <button className="h-14 px-6 bg-black text-white rounded-xl flex items-center gap-3">
                <span className="text-2xl">▶️</span>
                <div className="text-left">
                  <div className="text-[10px] opacity-80">Get it on</div>
                  <div className="font-semibold">Google Play</div>
                </div>
              </button>
            </div>

            <div className="flex items-center gap-2 justify-center lg:justify-start">
              <span className="text-yellow-500">★★★★★</span>
              <span className="text-sm text-gray-600">4.9 • 50K+ reviews</span>
            </div>
          </div>

          {/* Phone Mockup */}
          <div className="flex justify-center">
            <div className="relative">
              {/* Phone Frame */}
              <div className="relative w-64 h-[520px] rounded-[45px] border-[10px] border-gray-900 bg-gray-900 shadow-2xl overflow-hidden">
                <div className="absolute left-1/2 top-2 w-20 h-5 -translate-x-1/2 bg-black rounded-full" />
                <div className="h-full w-full rounded-[35px] bg-gradient-to-b from-purple-500 to-pink-500 flex items-center justify-center">
                  <div className="text-white text-center">
                    <span className="text-6xl">✨</span>
                    <p className="mt-4 font-medium">App Preview</p>
                  </div>
                </div>
                <div className="absolute bottom-2 left-1/2 w-24 h-1 -translate-x-1/2 bg-white rounded-full" />
              </div>

              {/* Floating Badges */}
              <div className="absolute -left-16 top-1/4 px-3 py-2 bg-white rounded-lg shadow-lg border" style={{ animation: 'float 3s ease-in-out infinite' }}>
                <span className="text-green-500">✓</span> Task done!
              </div>
              <div className="absolute -right-16 top-1/2 px-3 py-2 bg-white rounded-lg shadow-lg border" style={{ animation: 'float 3s ease-in-out infinite 1s' }}>
                🔥 7 day streak!
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Features */}
      <section className="py-20 px-4">
        <h2 className="text-3xl font-bold text-center mb-12">Everything you need</h2>
        <div className="grid md:grid-cols-3 gap-6 max-w-4xl mx-auto">
          {[
            { icon: "✅", title: "Smart Tasks", desc: "AI-powered prioritization" },
            { icon: "🔥", title: "Habit Tracking", desc: "Build lasting habits" },
            { icon: "🎯", title: "Goal Planning", desc: "Achieve your dreams" },
          ].map(f => (
            <div key={f.title} className="text-center p-6 rounded-2xl bg-white border shadow-sm">
              <span className="text-4xl">{f.icon}</span>
              <h3 className="font-bold text-xl mt-4 mb-2">{f.title}</h3>
              <p className="text-gray-600">{f.desc}</p>
            </div>
          ))}
        </div>
      </section>

      {/* Reviews Marquee */}
      <section className="py-20 bg-gray-50 overflow-hidden">
        <h2 className="text-3xl font-bold text-center mb-12">Loved by millions</h2>
        <div className="flex" style={{ animation: 'marquee 30s linear infinite' }}>
          {[...reviews, ...reviews, ...reviews].map((r, i) => (
            <div key={i} className="flex-shrink-0 w-72 mx-3 p-6 bg-white rounded-2xl border shadow-sm">
              <div className="flex items-center gap-3 mb-3">
                <span className="text-3xl">{r.avatar}</span>
                <div>
                  <div className="font-semibold">{r.name}</div>
                  <div className="text-yellow-500 text-sm">{"★".repeat(r.rating)}</div>
                </div>
              </div>
              <p className="text-gray-600">"{r.text}"</p>
            </div>
          ))}
        </div>
      </section>

      {/* CTA */}
      <section className="py-20 px-4">
        <div className="max-w-4xl mx-auto bg-gradient-to-r from-purple-600 to-pink-600 rounded-3xl p-12 text-center text-white">
          <h2 className="text-4xl font-bold mb-4">Download now</h2>
          <p className="text-lg opacity-90 mb-8">Join 2 million users today. Free to start.</p>
          <div className="flex gap-4 justify-center">
            <button className="h-14 px-8 bg-white text-purple-600 rounded-xl font-semibold">
              🍎 App Store
            </button>
            <button className="h-14 px-8 bg-white text-purple-600 rounded-xl font-semibold">
              ▶️ Google Play
            </button>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="py-12 border-t px-4">
        <div className="max-w-6xl mx-auto flex justify-between items-center">
          <span className="font-bold">📱 LifeOS</span>
          <span className="text-sm text-gray-500">© 2024 All rights reserved</span>
        </div>
      </footer>
    </div>
  )
}
```
