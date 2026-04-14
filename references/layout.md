# Layout Components Reference

Complete implementations for layout and structural components.

---

## 1. Marquee

Infinite scrolling component for text, images, or cards.

```tsx
import { cn } from "@/lib/utils"
import { ReactNode } from "react"

interface MarqueeProps {
  className?: string
  reverse?: boolean
  pauseOnHover?: boolean
  children?: ReactNode
  vertical?: boolean
  repeat?: number
}

export function Marquee({
  className,
  reverse,
  pauseOnHover = false,
  children,
  vertical = false,
  repeat = 4,
  ...props
}: MarqueeProps) {
  return (
    <div
      {...props}
      className={cn(
        "group flex overflow-hidden p-2 [--duration:40s] [--gap:1rem] [gap:var(--gap)]",
        vertical ? "flex-col" : "flex-row",
        className
      )}
    >
      {Array.from({ length: repeat }).map((_, i) => (
        <div
          key={i}
          className={cn(
            "flex shrink-0 justify-around [gap:var(--gap)]",
            vertical ? "animate-marquee-vertical flex-col" : "animate-marquee flex-row",
            pauseOnHover && "group-hover:[animation-play-state:paused]",
            reverse && "[animation-direction:reverse]"
          )}
        >
          {children}
        </div>
      ))}
    </div>
  )
}
```

**Required CSS:**
```css
@keyframes marquee {
  from { transform: translateX(0); }
  to { transform: translateX(calc(-100% - var(--gap))); }
}

@keyframes marquee-vertical {
  from { transform: translateY(0); }
  to { transform: translateY(calc(-100% - var(--gap))); }
}

.animate-marquee {
  animation: marquee var(--duration) linear infinite;
}

.animate-marquee-vertical {
  animation: marquee-vertical var(--duration) linear infinite;
}
```

**Usage - Horizontal with Review Cards:**
```tsx
const reviews = [
  { name: "Jack", username: "@jack", body: "Amazing product!", img: "https://avatar.vercel.sh/jack" },
  { name: "Jill", username: "@jill", body: "Love it!", img: "https://avatar.vercel.sh/jill" },
  // ...more reviews
]

function ReviewCard({ img, name, username, body }) {
  return (
    <figure className="relative w-64 cursor-pointer overflow-hidden rounded-xl border p-4 border-gray-950/[.1] bg-gray-950/[.01] hover:bg-gray-950/[.05]">
      <div className="flex items-center gap-2">
        <img className="rounded-full" width="32" height="32" src={img} alt="" />
        <div className="flex flex-col">
          <figcaption className="text-sm font-medium">{name}</figcaption>
          <p className="text-xs text-gray-500">{username}</p>
        </div>
      </div>
      <blockquote className="mt-2 text-sm">{body}</blockquote>
    </figure>
  )
}

export function MarqueeDemo() {
  const firstRow = reviews.slice(0, reviews.length / 2)
  const secondRow = reviews.slice(reviews.length / 2)

  return (
    <div className="relative flex w-full flex-col items-center overflow-hidden">
      <Marquee pauseOnHover className="[--duration:20s]">
        {firstRow.map((review) => <ReviewCard key={review.username} {...review} />)}
      </Marquee>
      <Marquee reverse pauseOnHover className="[--duration:20s]">
        {secondRow.map((review) => <ReviewCard key={review.username} {...review} />)}
      </Marquee>
      {/* Gradient overlays */}
      <div className="pointer-events-none absolute inset-y-0 left-0 w-1/3 bg-gradient-to-r from-white" />
      <div className="pointer-events-none absolute inset-y-0 right-0 w-1/3 bg-gradient-to-l from-white" />
    </div>
  )
}
```

**Usage - Vertical:**
```tsx
<Marquee vertical pauseOnHover className="h-[400px] [--duration:20s]">
  {reviews.map((review) => <ReviewCard key={review.username} {...review} />)}
</Marquee>
```

**Usage - Logo Marquee:**
```tsx
<Marquee className="[--duration:30s]">
  {logos.map((logo, i) => (
    <img key={i} src={logo.src} alt={logo.alt} className="h-12 w-auto opacity-70 hover:opacity-100" />
  ))}
</Marquee>
```

---

## 2. BentoGrid

Asymmetric grid layout for feature cards.

```tsx
import { cn } from "@/lib/utils"
import { ReactNode } from "react"

interface BentoGridProps {
  className?: string
  children?: ReactNode
}

export function BentoGrid({ className, children }: BentoGridProps) {
  return (
    <div
      className={cn(
        "grid w-full auto-rows-[22rem] grid-cols-3 gap-4",
        className
      )}
    >
      {children}
    </div>
  )
}

interface BentoCardProps {
  name: string
  className?: string
  background?: ReactNode
  Icon?: any
  description?: string
  href?: string
  cta?: string
}

export function BentoCard({
  name,
  className,
  background,
  Icon,
  description,
  href,
  cta,
}: BentoCardProps) {
  return (
    <div
      className={cn(
        "group relative col-span-3 flex flex-col justify-between overflow-hidden rounded-xl",
        "bg-white [box-shadow:0_0_0_1px_rgba(0,0,0,.03),0_2px_4px_rgba(0,0,0,.05),0_12px_24px_rgba(0,0,0,.05)]",
        "transform-gpu dark:bg-black dark:[border:1px_solid_rgba(255,255,255,.1)] dark:[box-shadow:0_-20px_80px_-20px_#ffffff1f_inset]",
        className
      )}
    >
      <div>{background}</div>
      <div className="pointer-events-none z-10 flex transform-gpu flex-col gap-1 p-6 transition-all duration-300 group-hover:-translate-y-10">
        {Icon && <Icon className="h-12 w-12 origin-left transform-gpu text-neutral-700 transition-all duration-300 ease-in-out group-hover:scale-75" />}
        <h3 className="text-xl font-semibold text-neutral-700 dark:text-neutral-300">
          {name}
        </h3>
        <p className="max-w-lg text-neutral-400">{description}</p>
      </div>

      <div
        className={cn(
          "pointer-events-none absolute bottom-0 flex w-full translate-y-10 transform-gpu flex-row items-center p-4 opacity-0 transition-all duration-300 group-hover:translate-y-0 group-hover:opacity-100"
        )}
      >
        {href && (
          <a href={href} className="pointer-events-auto inline-flex gap-1 items-center text-sm font-medium text-blue-500">
            {cta}
            <svg className="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M9 5l7 7-7 7" />
            </svg>
          </a>
        )}
      </div>
      <div className="pointer-events-none absolute inset-0 transform-gpu transition-all duration-300 group-hover:bg-black/[.03] group-hover:dark:bg-neutral-800/10" />
    </div>
  )
}
```

**Usage:**
```tsx
<BentoGrid className="lg:grid-rows-3">
  <BentoCard
    name="Feature One"
    className="lg:row-start-1 lg:row-end-4 lg:col-start-2 lg:col-end-3"
    Icon={SparklesIcon}
    description="Main feature description"
    href="#"
    cta="Learn more"
    background={<img className="absolute -right-20 -top-20 opacity-60" src="/feature1.png" />}
  />
  <BentoCard
    name="Feature Two"
    className="lg:col-start-1 lg:col-end-2 lg:row-start-1 lg:row-end-3"
    Icon={BoltIcon}
    description="Secondary feature"
    href="#"
    cta="Get started"
  />
  {/* ...more cards */}
</BentoGrid>
```

---

## 3. Dock

macOS-style dock with hover magnification.

```tsx
"use client"
import { cn } from "@/lib/utils"
import { cva, type VariantProps } from "class-variance-authority"
import { motion, useMotionValue, useSpring, useTransform } from "framer-motion"
import { useRef, PropsWithChildren, ReactNode } from "react"

const dockVariants = cva(
  "mx-auto w-max h-[58px] p-2 flex items-end gap-2 rounded-2xl border dark:border-[#707070]"
)

interface DockProps extends VariantProps<typeof dockVariants> {
  className?: string
  magnification?: number
  distance?: number
  children: ReactNode
}

export function Dock({
  className,
  children,
  magnification = 60,
  distance = 140,
  ...props
}: DockProps) {
  const mouseX = useMotionValue(Infinity)

  return (
    <motion.div
      onMouseMove={(e) => mouseX.set(e.pageX)}
      onMouseLeave={() => mouseX.set(Infinity)}
      {...props}
      className={cn(dockVariants(), className)}
    >
      {children}
    </motion.div>
  )
}

interface DockIconProps {
  magnification?: number
  distance?: number
  mouseX?: any
  className?: string
  children?: ReactNode
}

export function DockIcon({
  magnification = 60,
  distance = 140,
  mouseX,
  className,
  children,
  ...props
}: DockIconProps) {
  const ref = useRef<HTMLDivElement>(null)

  const distanceCalc = useTransform(mouseX, (val: number) => {
    const bounds = ref.current?.getBoundingClientRect() ?? { x: 0, width: 0 }
    return val - bounds.x - bounds.width / 2
  })

  const widthSync = useTransform(
    distanceCalc,
    [-distance, 0, distance],
    [40, magnification, 40]
  )

  const width = useSpring(widthSync, {
    mass: 0.1,
    stiffness: 150,
    damping: 12,
  })

  return (
    <motion.div
      ref={ref}
      style={{ width }}
      className={cn(
        "flex aspect-square cursor-pointer items-center justify-center rounded-full bg-neutral-400/40",
        className
      )}
      {...props}
    >
      {children}
    </motion.div>
  )
}
```

**Usage:**
```tsx
<Dock>
  <DockIcon><HomeIcon className="size-full" /></DockIcon>
  <DockIcon><MailIcon className="size-full" /></DockIcon>
  <DockIcon><CalendarIcon className="size-full" /></DockIcon>
</Dock>
```

---

## 4. AnimatedList

Staggered list animation for notifications/items.

```tsx
"use client"
import { cn } from "@/lib/utils"
import { AnimatePresence, motion } from "framer-motion"
import { ReactNode, useEffect, useMemo, useState } from "react"

interface AnimatedListProps {
  className?: string
  children: ReactNode
  delay?: number
}

export function AnimatedList({ className, children, delay = 1000 }: AnimatedListProps) {
  const [index, setIndex] = useState(0)
  const childrenArray = useMemo(() => React.Children.toArray(children), [children])

  useEffect(() => {
    const interval = setInterval(() => {
      setIndex((prevIndex) => (prevIndex + 1) % childrenArray.length)
    }, delay)
    return () => clearInterval(interval)
  }, [childrenArray.length, delay])

  const itemsToShow = useMemo(
    () => childrenArray.slice(0, index + 1).reverse(),
    [index, childrenArray]
  )

  return (
    <div className={cn("flex flex-col items-center gap-4", className)}>
      <AnimatePresence>
        {itemsToShow.map((item) => (
          <AnimatedListItem key={(item as any).key}>
            {item}
          </AnimatedListItem>
        ))}
      </AnimatePresence>
    </div>
  )
}

function AnimatedListItem({ children }: { children: ReactNode }) {
  const animations = {
    initial: { scale: 0, opacity: 0 },
    animate: { scale: 1, opacity: 1, originY: 0 },
    exit: { scale: 0, opacity: 0 },
    transition: { type: "spring", stiffness: 350, damping: 40 },
  }

  return (
    <motion.div {...animations} layout className="mx-auto w-full">
      {children}
    </motion.div>
  )
}
```

**Usage:**
```tsx
const notifications = [
  { name: "Payment received", time: "15m ago", icon: "💸" },
  { name: "User signed up", time: "10m ago", icon: "👤" },
  // ...
]

<AnimatedList>
  {notifications.map((item, idx) => (
    <Notification key={idx} {...item} />
  ))}
</AnimatedList>
```

---

## 5. OrbitingCircles

Items rotating in orbital paths.

```tsx
import { cn } from "@/lib/utils"
import { ReactNode } from "react"

interface OrbitingCirclesProps {
  className?: string
  children?: ReactNode
  reverse?: boolean
  duration?: number
  delay?: number
  radius?: number
  path?: boolean
}

export function OrbitingCircles({
  className,
  children,
  reverse,
  duration = 20,
  delay = 10,
  radius = 50,
  path = true,
}: OrbitingCirclesProps) {
  return (
    <>
      {path && (
        <svg
          xmlns="http://www.w3.org/2000/svg"
          version="1.1"
          className="pointer-events-none absolute inset-0 size-full"
        >
          <circle
            className="stroke-black/10 stroke-1 dark:stroke-white/10"
            cx="50%"
            cy="50%"
            r={radius}
            fill="none"
          />
        </svg>
      )}
      <div
        style={
          {
            "--duration": duration,
            "--radius": radius,
            "--delay": -delay,
          } as React.CSSProperties
        }
        className={cn(
          "absolute flex size-full transform-gpu animate-orbit items-center justify-center rounded-full border bg-black/10 [animation-delay:calc(var(--delay)*1000ms)] dark:bg-white/10",
          reverse && "[animation-direction:reverse]",
          className
        )}
      >
        {children}
      </div>
    </>
  )
}
```

**Required CSS:**
```css
@keyframes orbit {
  0% { transform: rotate(0deg) translateY(calc(var(--radius) * 1px)) rotate(0deg); }
  100% { transform: rotate(360deg) translateY(calc(var(--radius) * 1px)) rotate(-360deg); }
}

.animate-orbit {
  animation: orbit calc(var(--duration) * 1s) linear infinite;
}
```

**Usage:**
```tsx
<div className="relative flex h-[500px] w-full items-center justify-center">
  <span className="text-4xl">🌍</span>
  
  <OrbitingCircles radius={80} duration={20}>
    <span className="text-2xl">🚀</span>
  </OrbitingCircles>
  
  <OrbitingCircles radius={140} duration={30} reverse>
    <span className="text-2xl">🛸</span>
  </OrbitingCircles>
</div>
```

---

## 6. AvatarCircles

Overlapping avatar stack.

```tsx
import { cn } from "@/lib/utils"

interface AvatarCirclesProps {
  className?: string
  numPeople?: number
  avatarUrls: string[]
}

export function AvatarCircles({
  numPeople,
  className,
  avatarUrls,
}: AvatarCirclesProps) {
  return (
    <div className={cn("z-10 flex -space-x-4 rtl:space-x-reverse", className)}>
      {avatarUrls.map((url, index) => (
        <img
          key={index}
          className="h-10 w-10 rounded-full border-2 border-white dark:border-gray-800"
          src={url}
          width={40}
          height={40}
          alt={`Avatar ${index + 1}`}
        />
      ))}
      {numPeople && (
        <a
          className="flex h-10 w-10 items-center justify-center rounded-full border-2 border-white bg-black text-center text-xs font-medium text-white hover:bg-gray-600 dark:border-gray-800"
          href="#"
        >
          +{numPeople}
        </a>
      )}
    </div>
  )
}
```

**Usage:**
```tsx
<AvatarCircles
  numPeople={99}
  avatarUrls={[
    "https://avatar.vercel.sh/1",
    "https://avatar.vercel.sh/2",
    "https://avatar.vercel.sh/3",
    "https://avatar.vercel.sh/4",
  ]}
/>
```

---

## 7. Terminal

Code terminal display component.

```tsx
import { cn } from "@/lib/utils"
import { ReactNode } from "react"

interface TerminalProps {
  children: ReactNode
  className?: string
}

export function Terminal({ children, className }: TerminalProps) {
  return (
    <div
      className={cn(
        "relative mx-auto w-full max-w-lg rounded-lg border bg-black text-white shadow-lg",
        className
      )}
    >
      {/* Terminal Header */}
      <div className="flex items-center gap-2 border-b border-gray-800 px-4 py-3">
        <div className="h-3 w-3 rounded-full bg-red-500" />
        <div className="h-3 w-3 rounded-full bg-yellow-500" />
        <div className="h-3 w-3 rounded-full bg-green-500" />
        <span className="ml-2 text-sm text-gray-400">terminal</span>
      </div>
      {/* Terminal Content */}
      <div className="p-4 font-mono text-sm">{children}</div>
    </div>
  )
}

export function TerminalLine({ children }: { children: ReactNode }) {
  return (
    <div className="flex items-center gap-2">
      <span className="text-green-400">$</span>
      <span>{children}</span>
    </div>
  )
}
```

**Usage:**
```tsx
<Terminal>
  <TerminalLine>npm install magic-ui</TerminalLine>
  <TerminalLine>npx shadcn@latest add marquee</TerminalLine>
</Terminal>
```

---

## Artifact-Ready Layout Components

### Self-Contained Marquee

```jsx
export default function MarqueeDemo() {
  const reviews = [
    { name: "Alice", text: "Amazing product!", avatar: "🧑" },
    { name: "Bob", text: "Love this so much!", avatar: "👨" },
    { name: "Carol", text: "Game changer!", avatar: "👩" },
    { name: "Dave", text: "Highly recommend!", avatar: "🧔" },
  ]

  return (
    <div className="flex flex-col items-center justify-center min-h-screen bg-white overflow-hidden">
      <style>{`
        @keyframes marquee {
          from { transform: translateX(0); }
          to { transform: translateX(calc(-100% - 1rem)); }
        }
      `}</style>
      
      <h2 className="text-2xl font-bold mb-8">What people are saying</h2>
      
      <div className="relative w-full overflow-hidden">
        <div className="flex gap-4 hover:[animation-play-state:paused]" style={{ animation: 'marquee 20s linear infinite' }}>
          {[...reviews, ...reviews, ...reviews, ...reviews].map((review, i) => (
            <div key={i} className="flex-shrink-0 w-64 p-4 rounded-xl border bg-gray-50">
              <div className="flex items-center gap-2 mb-2">
                <span className="text-2xl">{review.avatar}</span>
                <span className="font-medium">{review.name}</span>
              </div>
              <p className="text-gray-600">{review.text}</p>
            </div>
          ))}
        </div>
        
        {/* Gradient overlays */}
        <div className="pointer-events-none absolute inset-y-0 left-0 w-24 bg-gradient-to-r from-white" />
        <div className="pointer-events-none absolute inset-y-0 right-0 w-24 bg-gradient-to-l from-white" />
      </div>
    </div>
  )
}
```

### Self-Contained Bento Grid

```jsx
export default function BentoGridDemo() {
  const features = [
    { title: "Analytics", desc: "Track everything in real-time", icon: "📊", span: "col-span-2" },
    { title: "Security", desc: "Enterprise-grade protection", icon: "🔒", span: "" },
    { title: "Speed", desc: "Lightning fast performance", icon: "⚡", span: "" },
    { title: "Integration", desc: "Connect with 100+ tools", icon: "🔗", span: "col-span-2" },
  ]

  return (
    <div className="min-h-screen bg-gray-100 p-8">
      <h2 className="text-3xl font-bold text-center mb-8">Features</h2>
      
      <div className="grid grid-cols-3 gap-4 max-w-4xl mx-auto auto-rows-[200px]">
        {features.map((feature, i) => (
          <div
            key={i}
            className={`group relative overflow-hidden rounded-xl bg-white p-6 shadow-sm border hover:shadow-lg transition-shadow ${feature.span}`}
          >
            <span className="text-4xl mb-4 block">{feature.icon}</span>
            <h3 className="text-xl font-semibold mb-2">{feature.title}</h3>
            <p className="text-gray-500">{feature.desc}</p>
            
            <div className="absolute inset-0 bg-black/5 opacity-0 group-hover:opacity-100 transition-opacity" />
          </div>
        ))}
      </div>
    </div>
  )
}
```

### Self-Contained Orbiting Circles

```jsx
export default function OrbitingDemo() {
  return (
    <div className="flex items-center justify-center min-h-screen bg-black">
      <style>{`
        @keyframes orbit {
          from { transform: rotate(0deg) translateY(var(--radius)) rotate(0deg); }
          to { transform: rotate(360deg) translateY(var(--radius)) rotate(-360deg); }
        }
      `}</style>
      
      <div className="relative w-80 h-80">
        {/* Center */}
        <div className="absolute inset-0 flex items-center justify-center">
          <div className="text-6xl">🌍</div>
        </div>
        
        {/* Orbit paths */}
        <svg className="absolute inset-0 w-full h-full">
          <circle cx="50%" cy="50%" r="80" fill="none" stroke="rgba(255,255,255,0.1)" strokeWidth="1" />
          <circle cx="50%" cy="50%" r="120" fill="none" stroke="rgba(255,255,255,0.1)" strokeWidth="1" />
        </svg>
        
        {/* Orbiting items */}
        <div 
          className="absolute inset-0 flex items-center justify-center"
          style={{ '--radius': '80px', animation: 'orbit 10s linear infinite' }}
        >
          <span className="text-2xl">🚀</span>
        </div>
        
        <div 
          className="absolute inset-0 flex items-center justify-center"
          style={{ '--radius': '120px', animation: 'orbit 15s linear infinite reverse' }}
        >
          <span className="text-2xl">🛸</span>
        </div>
      </div>
    </div>
  )
}
```
