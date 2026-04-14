# Testimonials Sections Reference

Multiple testimonial section variants for social proof.

---

## 1. Testimonials - Double Marquee

Two rows scrolling in opposite directions (Magic UI signature).

```tsx
import { Marquee } from "@/components/magicui/marquee"
import { cn } from "@/lib/utils"

const testimonials = [
  { name: "Sarah Chen", role: "CEO at TechCorp", content: "This tool has transformed how our team works. We've cut our deployment time by 80%.", avatar: "https://avatar.vercel.sh/sarah" },
  { name: "Mike Johnson", role: "CTO at StartupXYZ", content: "The best developer experience I've ever had. It just works.", avatar: "https://avatar.vercel.sh/mike" },
  { name: "Emily Davis", role: "Lead Engineer at BigCo", content: "We migrated our entire infrastructure in a weekend. Incredible.", avatar: "https://avatar.vercel.sh/emily" },
  { name: "Alex Kim", role: "Founder at DevTools", content: "Finally, a tool that understands what developers actually need.", avatar: "https://avatar.vercel.sh/alex" },
  { name: "Jessica Lee", role: "VP Engineering", content: "Our team productivity has increased 3x since switching.", avatar: "https://avatar.vercel.sh/jessica" },
  { name: "David Brown", role: "Senior Developer", content: "I recommend this to every developer I know. It's that good.", avatar: "https://avatar.vercel.sh/david" },
]

const firstRow = testimonials.slice(0, testimonials.length / 2)
const secondRow = testimonials.slice(testimonials.length / 2)

function TestimonialCard({ name, role, content, avatar }: typeof testimonials[0]) {
  return (
    <div className="w-80 p-6 rounded-2xl border bg-background shadow-sm mx-3">
      <p className="text-muted-foreground mb-4">"{content}"</p>
      <div className="flex items-center gap-3">
        <img src={avatar} alt={name} className="w-10 h-10 rounded-full" />
        <div>
          <div className="font-semibold">{name}</div>
          <div className="text-sm text-muted-foreground">{role}</div>
        </div>
      </div>
    </div>
  )
}

export function TestimonialsMarquee() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4 mb-12">
        <h2 className="text-3xl md:text-4xl font-bold text-center mb-4">
          Loved by developers worldwide
        </h2>
        <p className="text-lg text-muted-foreground text-center">
          Join thousands of happy customers
        </p>
      </div>

      <div className="space-y-4">
        <Marquee pauseOnHover className="[--duration:40s]">
          {firstRow.map((t) => <TestimonialCard key={t.name} {...t} />)}
        </Marquee>
        <Marquee pauseOnHover reverse className="[--duration:40s]">
          {secondRow.map((t) => <TestimonialCard key={t.name} {...t} />)}
        </Marquee>
      </div>
    </section>
  )
}
```

---

## 2. Testimonials - Grid Layout

Static 3-column grid with featured testimonial.

```tsx
const testimonials = [
  { name: "Sarah Chen", role: "CEO, TechCorp", content: "This completely changed how we build products. Our team is 10x more productive.", avatar: "👩‍💼", featured: true },
  { name: "Mike Johnson", role: "CTO, StartupXYZ", content: "The best investment we've made this year.", avatar: "👨‍💻" },
  { name: "Emily Davis", role: "Lead Engineer", content: "Incredible developer experience.", avatar: "👩‍🔬" },
  { name: "Alex Kim", role: "Founder", content: "Wish I found this years ago.", avatar: "🧑‍💼" },
  { name: "Jessica Lee", role: "VP Engineering", content: "Our go-to tool for everything.", avatar: "👩‍🚀" },
  { name: "David Brown", role: "Senior Dev", content: "Simply the best in its class.", avatar: "👨‍🎨" },
]

export function TestimonialsGrid() {
  const featured = testimonials.find(t => t.featured)
  const others = testimonials.filter(t => !t.featured)

  return (
    <section className="py-24 bg-muted/30">
      <div className="container mx-auto px-4">
        <h2 className="text-3xl md:text-4xl font-bold text-center mb-16">
          What our customers say
        </h2>

        <div className="max-w-5xl mx-auto">
          {/* Featured */}
          {featured && (
            <div className="mb-8 p-8 rounded-2xl border-2 border-primary bg-background text-center">
              <p className="text-2xl mb-6">"{featured.content}"</p>
              <div className="flex items-center justify-center gap-3">
                <span className="text-4xl">{featured.avatar}</span>
                <div className="text-left">
                  <div className="font-bold">{featured.name}</div>
                  <div className="text-sm text-muted-foreground">{featured.role}</div>
                </div>
              </div>
            </div>
          )}

          {/* Grid */}
          <div className="grid md:grid-cols-3 gap-4">
            {others.map((t) => (
              <div key={t.name} className="p-6 rounded-xl border bg-background">
                <p className="text-muted-foreground mb-4">"{t.content}"</p>
                <div className="flex items-center gap-3">
                  <span className="text-2xl">{t.avatar}</span>
                  <div>
                    <div className="font-semibold text-sm">{t.name}</div>
                    <div className="text-xs text-muted-foreground">{t.role}</div>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>
    </section>
  )
}
```

---

## 3. Testimonials - Video Testimonials

Video testimonials with play buttons.

```tsx
import { Play } from "lucide-react"

const videos = [
  { name: "Sarah Chen", role: "CEO at TechCorp", thumbnail: "/testimonials/sarah.jpg", duration: "2:34" },
  { name: "Mike Johnson", role: "CTO at StartupXYZ", thumbnail: "/testimonials/mike.jpg", duration: "1:45" },
  { name: "Emily Davis", role: "Lead Engineer", thumbnail: "/testimonials/emily.jpg", duration: "3:12" },
]

export function TestimonialsVideo() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <h2 className="text-3xl md:text-4xl font-bold text-center mb-4">
          Hear from our customers
        </h2>
        <p className="text-lg text-muted-foreground text-center mb-16">
          Real stories from real people
        </p>

        <div className="grid md:grid-cols-3 gap-6 max-w-5xl mx-auto">
          {videos.map((video) => (
            <div key={video.name} className="group cursor-pointer">
              <div className="relative aspect-video rounded-xl overflow-hidden mb-4">
                <img
                  src={video.thumbnail}
                  alt={video.name}
                  className="w-full h-full object-cover transition-transform group-hover:scale-105"
                />
                <div className="absolute inset-0 bg-black/30 group-hover:bg-black/40 transition" />
                <div className="absolute inset-0 flex items-center justify-center">
                  <div className="w-14 h-14 rounded-full bg-white flex items-center justify-center shadow-lg group-hover:scale-110 transition">
                    <Play className="w-5 h-5 text-black ml-1" fill="black" />
                  </div>
                </div>
                <div className="absolute bottom-2 right-2 px-2 py-1 rounded bg-black/70 text-white text-xs">
                  {video.duration}
                </div>
              </div>
              <h3 className="font-semibold">{video.name}</h3>
              <p className="text-sm text-muted-foreground">{video.role}</p>
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## 4. Testimonials - Tweet Wall

Twitter/X style testimonial wall.

```tsx
const tweets = [
  { name: "Sarah Chen", handle: "@sarahchen", content: "Just shipped our new feature using @magicui in half the time. This thing is incredible 🔥", avatar: "https://avatar.vercel.sh/sarah", likes: 234, retweets: 45 },
  { name: "Mike J", handle: "@mikej_dev", content: "Finally found a component library that doesn't make me want to throw my laptop out the window", avatar: "https://avatar.vercel.sh/mike", likes: 567, retweets: 89 },
  { name: "Emily", handle: "@emily_codes", content: "The animations in @magicui are *chef's kiss* ✨", avatar: "https://avatar.vercel.sh/emily", likes: 123, retweets: 23 },
  { name: "Alex Kim", handle: "@alexkim", content: "Saved us weeks of work. Not exaggerating.", avatar: "https://avatar.vercel.sh/alex", likes: 345, retweets: 67 },
]

export function TestimonialsTweets() {
  return (
    <section className="py-24 bg-muted/30">
      <div className="container mx-auto px-4">
        <h2 className="text-3xl md:text-4xl font-bold text-center mb-16">
          What people are saying
        </h2>

        <div className="columns-1 md:columns-2 lg:columns-3 gap-4 max-w-5xl mx-auto">
          {tweets.map((tweet) => (
            <div key={tweet.handle} className="break-inside-avoid mb-4 p-4 rounded-xl border bg-background">
              <div className="flex items-center gap-3 mb-3">
                <img src={tweet.avatar} alt={tweet.name} className="w-10 h-10 rounded-full" />
                <div>
                  <div className="font-semibold">{tweet.name}</div>
                  <div className="text-sm text-muted-foreground">{tweet.handle}</div>
                </div>
                <svg className="w-5 h-5 ml-auto text-[#1DA1F2]" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M23.643 4.937c-.835.37-1.732.62-2.675.733.962-.576 1.7-1.49 2.048-2.578-.9.534-1.897.922-2.958 1.13-.85-.904-2.06-1.47-3.4-1.47-2.572 0-4.658 2.086-4.658 4.66 0 .364.042.718.12 1.06-3.873-.195-7.304-2.05-9.602-4.868-.4.69-.63 1.49-.63 2.342 0 1.616.823 3.043 2.072 3.878-.764-.025-1.482-.234-2.11-.583v.06c0 2.257 1.605 4.14 3.737 4.568-.392.106-.803.162-1.227.162-.3 0-.593-.028-.877-.082.593 1.85 2.313 3.198 4.352 3.234-1.595 1.25-3.604 1.995-5.786 1.995-.376 0-.747-.022-1.112-.065 2.062 1.323 4.51 2.093 7.14 2.093 8.57 0 13.255-7.098 13.255-13.254 0-.2-.005-.402-.014-.602.91-.658 1.7-1.477 2.323-2.41z" />
                </svg>
              </div>
              <p className="mb-3">{tweet.content}</p>
              <div className="flex gap-4 text-sm text-muted-foreground">
                <span>❤️ {tweet.likes}</span>
                <span>🔁 {tweet.retweets}</span>
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

## 5. Testimonials - Logo + Quote

Company logos with executive quotes.

```tsx
const testimonials = [
  { company: "Vercel", logo: "/logos/vercel.svg", quote: "The best component library we've used.", author: "CEO" },
  { company: "Stripe", logo: "/logos/stripe.svg", quote: "Transformed our development workflow.", author: "CTO" },
  { company: "Linear", logo: "/logos/linear.svg", quote: "Finally, components that look good by default.", author: "Head of Design" },
]

export function TestimonialsLogos() {
  return (
    <section className="py-24">
      <div className="container mx-auto px-4">
        <h2 className="text-3xl font-bold text-center mb-16">
          Trusted by industry leaders
        </h2>

        <div className="grid md:grid-cols-3 gap-8 max-w-4xl mx-auto">
          {testimonials.map((t) => (
            <div key={t.company} className="text-center p-8 rounded-2xl border bg-background">
              <img src={t.logo} alt={t.company} className="h-8 mx-auto mb-6 opacity-70" />
              <p className="text-lg mb-4">"{t.quote}"</p>
              <p className="text-sm text-muted-foreground">{t.author}, {t.company}</p>
            </div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## Artifact-Ready Testimonials

```jsx
export default function TestimonialsDemo() {
  const testimonials = [
    { name: "Sarah Chen", role: "CEO, TechCorp", text: "This tool transformed how we work. 10x more productive.", avatar: "👩‍💼" },
    { name: "Mike Johnson", role: "CTO, StartupXYZ", text: "Best investment we made this year.", avatar: "👨‍💻" },
    { name: "Emily Davis", role: "Lead Engineer", text: "Incredible developer experience.", avatar: "👩‍🔬" },
    { name: "Alex Kim", role: "Founder", text: "Wish I found this years ago.", avatar: "🧑‍💼" },
    { name: "Jessica Lee", role: "VP Engineering", text: "Our go-to for everything.", avatar: "👩‍🚀" },
    { name: "David Brown", role: "Senior Dev", text: "Simply the best.", avatar: "👨‍🎨" },
  ]

  const row1 = testimonials.slice(0, 3)
  const row2 = testimonials.slice(3)

  return (
    <div className="min-h-screen bg-gray-950 text-white py-24 overflow-hidden">
      <style>{`
        @keyframes marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }
        @keyframes marquee-reverse { from { transform: translateX(-50%); } to { transform: translateX(0); } }
      `}</style>

      <div className="text-center mb-12 px-4">
        <h2 className="text-4xl font-bold mb-4">Loved by developers</h2>
        <p className="text-gray-400">Join thousands of happy customers</p>
      </div>

      {/* Row 1 - Left */}
      <div className="mb-4 overflow-hidden">
        <div className="flex" style={{ animation: 'marquee 30s linear infinite', width: 'max-content' }}>
          {[...row1, ...row1, ...row1, ...row1].map((t, i) => (
            <div key={i} className="w-80 flex-shrink-0 mx-3 p-6 rounded-2xl border border-gray-800 bg-gray-900">
              <p className="text-gray-300 mb-4">"{t.text}"</p>
              <div className="flex items-center gap-3">
                <span className="text-2xl">{t.avatar}</span>
                <div>
                  <div className="font-semibold">{t.name}</div>
                  <div className="text-sm text-gray-500">{t.role}</div>
                </div>
              </div>
            </div>
          ))}
        </div>
      </div>

      {/* Row 2 - Right (reverse) */}
      <div className="overflow-hidden">
        <div className="flex" style={{ animation: 'marquee-reverse 30s linear infinite', width: 'max-content' }}>
          {[...row2, ...row2, ...row2, ...row2].map((t, i) => (
            <div key={i} className="w-80 flex-shrink-0 mx-3 p-6 rounded-2xl border border-gray-800 bg-gray-900">
              <p className="text-gray-300 mb-4">"{t.text}"</p>
              <div className="flex items-center gap-3">
                <span className="text-2xl">{t.avatar}</span>
                <div>
                  <div className="font-semibold">{t.name}</div>
                  <div className="text-sm text-gray-500">{t.role}</div>
                </div>
              </div>
            </div>
          ))}
        </div>
      </div>
    </div>
  )
}
```
