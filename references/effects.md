# Special Effects Reference

Complete implementations for visual effects and animations.

---

## 1. AnimatedBeam

Flowing beam effect connecting elements.

```tsx
"use client"
import { cn } from "@/lib/utils"
import { motion } from "framer-motion"
import { RefObject, useEffect, useId, useState } from "react"

interface AnimatedBeamProps {
  className?: string
  containerRef: RefObject<HTMLElement>
  fromRef: RefObject<HTMLElement>
  toRef: RefObject<HTMLElement>
  curvature?: number
  endYOffset?: number
  reverse?: boolean
  pathColor?: string
  pathWidth?: number
  pathOpacity?: number
  gradientStartColor?: string
  gradientStopColor?: string
  delay?: number
  duration?: number
  startXOffset?: number
  startYOffset?: number
  endXOffset?: number
}

export function AnimatedBeam({
  className,
  containerRef,
  fromRef,
  toRef,
  curvature = 0,
  reverse = false,
  duration = Math.random() * 3 + 4,
  delay = 0,
  pathColor = "gray",
  pathWidth = 2,
  pathOpacity = 0.2,
  gradientStartColor = "#ffaa40",
  gradientStopColor = "#9c40ff",
  startXOffset = 0,
  startYOffset = 0,
  endXOffset = 0,
  endYOffset = 0,
}: AnimatedBeamProps) {
  const id = useId()
  const [pathD, setPathD] = useState("")
  const [svgDimensions, setSvgDimensions] = useState({ width: 0, height: 0 })

  useEffect(() => {
    const updatePath = () => {
      if (containerRef.current && fromRef.current && toRef.current) {
        const containerRect = containerRef.current.getBoundingClientRect()
        const rectA = fromRef.current.getBoundingClientRect()
        const rectB = toRef.current.getBoundingClientRect()

        const svgWidth = containerRect.width
        const svgHeight = containerRect.height
        setSvgDimensions({ width: svgWidth, height: svgHeight })

        const startX = rectA.left - containerRect.left + rectA.width / 2 + startXOffset
        const startY = rectA.top - containerRect.top + rectA.height / 2 + startYOffset
        const endX = rectB.left - containerRect.left + rectB.width / 2 + endXOffset
        const endY = rectB.top - containerRect.top + rectB.height / 2 + endYOffset

        const controlY = startY - curvature
        const d = `M ${startX},${startY} Q ${(startX + endX) / 2},${controlY} ${endX},${endY}`
        setPathD(d)
      }
    }

    updatePath()
    const resizeObserver = new ResizeObserver(updatePath)
    if (containerRef.current) resizeObserver.observe(containerRef.current)
    return () => resizeObserver.disconnect()
  }, [containerRef, fromRef, toRef, curvature, startXOffset, startYOffset, endXOffset, endYOffset])

  return (
    <svg
      fill="none"
      width={svgDimensions.width}
      height={svgDimensions.height}
      xmlns="http://www.w3.org/2000/svg"
      className={cn("pointer-events-none absolute left-0 top-0 transform-gpu stroke-2", className)}
      viewBox={`0 0 ${svgDimensions.width} ${svgDimensions.height}`}
    >
      <path d={pathD} stroke={pathColor} strokeWidth={pathWidth} strokeOpacity={pathOpacity} strokeLinecap="round" />
      <path d={pathD} strokeWidth={pathWidth} stroke={`url(#${id})`} strokeOpacity="1" strokeLinecap="round" />
      <defs>
        <motion.linearGradient
          className="transform-gpu"
          id={id}
          gradientUnits="userSpaceOnUse"
          initial={{ x1: "0%", x2: "0%", y1: "0%", y2: "0%" }}
          animate={{
            x1: reverse ? ["90%", "-10%"] : ["10%", "110%"],
            x2: reverse ? ["100%", "0%"] : ["0%", "100%"],
            y1: ["0%", "0%"],
            y2: ["0%", "0%"],
          }}
          transition={{ delay, duration, ease: [0.16, 1, 0.3, 1], repeat: Infinity, repeatDelay: 0 }}
        >
          <stop stopColor={gradientStartColor} stopOpacity="0" />
          <stop stopColor={gradientStartColor} />
          <stop offset="32.5%" stopColor={gradientStopColor} />
          <stop offset="100%" stopColor={gradientStopColor} stopOpacity="0" />
        </motion.linearGradient>
      </defs>
    </svg>
  )
}
```

---

## 2. BorderBeam

Animated border light effect.

```tsx
import { cn } from "@/lib/utils"

interface BorderBeamProps {
  className?: string
  size?: number
  duration?: number
  borderWidth?: number
  anchor?: number
  colorFrom?: string
  colorTo?: string
  delay?: number
}

export function BorderBeam({
  className,
  size = 200,
  duration = 15,
  anchor = 90,
  borderWidth = 1.5,
  colorFrom = "#ffaa40",
  colorTo = "#9c40ff",
  delay = 0,
}: BorderBeamProps) {
  return (
    <div
      style={
        {
          "--size": size,
          "--duration": duration,
          "--anchor": anchor,
          "--border-width": borderWidth,
          "--color-from": colorFrom,
          "--color-to": colorTo,
          "--delay": `-${delay}s`,
        } as React.CSSProperties
      }
      className={cn(
        "pointer-events-none absolute inset-0 rounded-[inherit] [border:calc(var(--border-width)*1px)_solid_transparent]",
        "![mask-clip:padding-box,border-box] ![mask-composite:intersect] [mask:linear-gradient(transparent,transparent),linear-gradient(white,white)]",
        "after:absolute after:aspect-square after:w-[calc(var(--size)*1px)] after:animate-border-beam after:[animation-delay:var(--delay)] after:[background:linear-gradient(to_left,var(--color-from),var(--color-to),transparent)] after:[offset-anchor:calc(var(--anchor)*1%)_50%] after:[offset-path:rect(0_auto_auto_0_round_calc(var(--size)*1px))]",
        className
      )}
    />
  )
}
```

**Required CSS:**
```css
@keyframes border-beam {
  100% { offset-distance: 100%; }
}

.animate-border-beam {
  animation: border-beam calc(var(--duration)*1s) infinite linear;
}
```

**Usage:**
```tsx
<div className="relative rounded-xl border bg-background p-8">
  <BorderBeam size={250} duration={12} />
  <h2>Card with animated border</h2>
</div>
```

---

## 3. ShineBorder

Shine effect on card borders.

```tsx
import { cn } from "@/lib/utils"
import { CSSProperties, ReactNode } from "react"

interface ShineBorderProps {
  borderRadius?: number
  borderWidth?: number
  duration?: number
  color?: string | string[]
  className?: string
  children: ReactNode
}

export function ShineBorder({
  borderRadius = 8,
  borderWidth = 1,
  duration = 14,
  color = "#000000",
  className,
  children,
}: ShineBorderProps) {
  return (
    <div
      style={
        {
          "--border-radius": `${borderRadius}px`,
        } as CSSProperties
      }
      className={cn(
        "relative grid min-h-[60px] w-fit min-w-[300px] place-items-center rounded-[--border-radius] bg-white p-3 text-black dark:bg-black dark:text-white",
        className
      )}
    >
      <div
        style={
          {
            "--border-width": `${borderWidth}px`,
            "--border-radius": `${borderRadius}px`,
            "--shine-pulse-duration": `${duration}s`,
            "--mask-linear-gradient": `linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0)`,
            "--background-radial-gradient": `radial-gradient(transparent,transparent, ${Array.isArray(color) ? color.join(",") : color},transparent,transparent)`,
          } as CSSProperties
        }
        className="before:bg-shine-size before:absolute before:inset-0 before:aspect-square before:size-full before:rounded-[--border-radius] before:p-[--border-width] before:will-change-[background-position] before:content-[''] before:![-webkit-mask-composite:xor] before:[background-image:--background-radial-gradient] before:[background-size:300%_300%] before:![mask-composite:exclude] before:[mask:--mask-linear-gradient] motion-safe:before:animate-shine"
      />
      {children}
    </div>
  )
}
```

**Required CSS:**
```css
@keyframes shine {
  0% { background-position: 0% 0%; }
  50% { background-position: 100% 100%; }
  100% { background-position: 0% 0%; }
}

.animate-shine {
  animation: shine var(--shine-pulse-duration) infinite linear;
}
```

---

## 4. MagicCard

Card with spotlight hover effect.

```tsx
"use client"
import { cn } from "@/lib/utils"
import { motion, useMotionTemplate, useMotionValue } from "framer-motion"
import { MouseEvent, ReactNode } from "react"

interface MagicCardProps {
  children: ReactNode
  className?: string
  gradientSize?: number
  gradientColor?: string
  gradientOpacity?: number
}

export function MagicCard({
  children,
  className,
  gradientSize = 200,
  gradientColor = "#262626",
  gradientOpacity = 0.8,
}: MagicCardProps) {
  const mouseX = useMotionValue(-gradientSize)
  const mouseY = useMotionValue(-gradientSize)

  const handleMouseMove = (e: MouseEvent<HTMLDivElement>) => {
    const { left, top } = e.currentTarget.getBoundingClientRect()
    mouseX.set(e.clientX - left)
    mouseY.set(e.clientY - top)
  }

  const handleMouseLeave = () => {
    mouseX.set(-gradientSize)
    mouseY.set(-gradientSize)
  }

  return (
    <div
      onMouseMove={handleMouseMove}
      onMouseLeave={handleMouseLeave}
      className={cn(
        "group relative flex size-full overflow-hidden rounded-xl bg-neutral-100 dark:bg-neutral-900 border text-black dark:text-white",
        className
      )}
    >
      <div className="relative z-10">{children}</div>
      <motion.div
        className="pointer-events-none absolute -inset-px rounded-xl opacity-0 transition-opacity duration-300 group-hover:opacity-100"
        style={{
          background: useMotionTemplate`
            radial-gradient(${gradientSize}px circle at ${mouseX}px ${mouseY}px, ${gradientColor}, transparent 100%)
          `,
          opacity: gradientOpacity,
        }}
      />
    </div>
  )
}
```

---

## 5. Meteors

Falling meteor streaks effect.

```tsx
import { cn } from "@/lib/utils"

interface MeteorsProps {
  number?: number
}

export function Meteors({ number = 20 }: MeteorsProps) {
  const meteors = new Array(number).fill(true)
  
  return (
    <>
      {meteors.map((_, idx) => (
        <span
          key={idx}
          className={cn(
            "animate-meteor-effect absolute top-1/2 left-1/2 h-0.5 w-0.5 rounded-[9999px] bg-slate-500 shadow-[0_0_0_1px_#ffffff10] rotate-[215deg]",
            "before:content-[''] before:absolute before:top-1/2 before:transform before:-translate-y-[50%] before:w-[50px] before:h-[1px] before:bg-gradient-to-r before:from-[#64748b] before:to-transparent"
          )}
          style={{
            top: 0,
            left: Math.floor(Math.random() * (400 - -400) + -400) + "px",
            animationDelay: Math.random() * (0.8 - 0.2) + 0.2 + "s",
            animationDuration: Math.floor(Math.random() * (10 - 2) + 2) + "s",
          }}
        />
      ))}
    </>
  )
}
```

**Required CSS:**
```css
@keyframes meteor {
  0% { transform: rotate(215deg) translateX(0); opacity: 1; }
  70% { opacity: 1; }
  100% { transform: rotate(215deg) translateX(-500px); opacity: 0; }
}

.animate-meteor-effect {
  animation: meteor 5s linear infinite;
}
```

---

## 6. Confetti

Celebration confetti burst.

```tsx
"use client"
import { useEffect, useRef } from "react"
import confetti from "canvas-confetti"

interface ConfettiProps {
  trigger?: boolean
}

export function Confetti({ trigger }: ConfettiProps) {
  const canvasRef = useRef<HTMLCanvasElement>(null)

  useEffect(() => {
    if (trigger && canvasRef.current) {
      const myConfetti = confetti.create(canvasRef.current, {
        resize: true,
        useWorker: true,
      })

      myConfetti({
        particleCount: 100,
        spread: 160,
        origin: { y: 0.6 },
      })
    }
  }, [trigger])

  return (
    <canvas
      ref={canvasRef}
      className="pointer-events-none fixed inset-0 z-50 h-full w-full"
    />
  )
}
```

**Note:** Requires `canvas-confetti` package. For artifacts, use a simplified version:

```jsx
// Self-contained confetti for artifacts
export default function ConfettiDemo() {
  const [particles, setParticles] = React.useState([])

  const burst = () => {
    const newParticles = Array.from({ length: 50 }, (_, i) => ({
      id: Date.now() + i,
      x: 50 + (Math.random() - 0.5) * 20,
      y: 50,
      color: ['#ff0', '#f0f', '#0ff', '#f00', '#0f0'][Math.floor(Math.random() * 5)],
      angle: Math.random() * 360,
      velocity: 2 + Math.random() * 3,
    }))
    setParticles(newParticles)
    setTimeout(() => setParticles([]), 2000)
  }

  return (
    <div className="relative h-screen flex items-center justify-center bg-gray-900">
      <style>{`
        @keyframes fall {
          to { transform: translateY(100vh) rotate(720deg); opacity: 0; }
        }
      `}</style>
      
      {particles.map(p => (
        <div
          key={p.id}
          className="absolute w-3 h-3 rounded-sm"
          style={{
            left: `${p.x}%`,
            top: `${p.y}%`,
            backgroundColor: p.color,
            animation: 'fall 2s ease-out forwards',
            transform: `rotate(${p.angle}deg)`,
          }}
        />
      ))}
      
      <button onClick={burst} className="px-6 py-3 bg-purple-600 text-white rounded-lg font-medium">
        🎉 Celebrate!
      </button>
    </div>
  )
}
```

---

## 7. BlurFade

Blur + fade entrance animation.

```tsx
"use client"
import { motion, Variants } from "framer-motion"
import { ReactNode } from "react"

interface BlurFadeProps {
  children: ReactNode
  className?: string
  variant?: {
    hidden: { y: number }
    visible: { y: number }
  }
  duration?: number
  delay?: number
  yOffset?: number
  inView?: boolean
  inViewMargin?: string
  blur?: string
}

export function BlurFade({
  children,
  className,
  variant,
  duration = 0.4,
  delay = 0,
  yOffset = 6,
  inView = false,
  inViewMargin = "-50px",
  blur = "6px",
}: BlurFadeProps) {
  const defaultVariants: Variants = {
    hidden: { y: yOffset, opacity: 0, filter: `blur(${blur})` },
    visible: { y: -yOffset, opacity: 1, filter: `blur(0px)` },
  }

  const combinedVariants = variant || defaultVariants

  return (
    <motion.div
      initial="hidden"
      animate={inView ? undefined : "visible"}
      whileInView={inView ? "visible" : undefined}
      viewport={{ once: true, margin: inViewMargin }}
      transition={{ delay, duration, ease: "easeOut" }}
      variants={combinedVariants}
      className={className}
    >
      {children}
    </motion.div>
  )
}
```

**Usage:**
```tsx
<BlurFade delay={0.1}>
  <h1>Heading with blur fade</h1>
</BlurFade>
<BlurFade delay={0.2}>
  <p>Paragraph with staggered animation</p>
</BlurFade>
```

---

## 8. GlareHover

Glare effect following mouse on hover.

```tsx
"use client"
import { cn } from "@/lib/utils"
import { MouseEvent, ReactNode, useState } from "react"

interface GlareHoverProps {
  children: ReactNode
  className?: string
  glareColor?: string
}

export function GlareHover({
  children,
  className,
  glareColor = "rgba(255, 255, 255, 0.4)",
}: GlareHoverProps) {
  const [position, setPosition] = useState({ x: 0, y: 0 })
  const [isHovered, setIsHovered] = useState(false)

  const handleMouseMove = (e: MouseEvent<HTMLDivElement>) => {
    const rect = e.currentTarget.getBoundingClientRect()
    setPosition({
      x: e.clientX - rect.left,
      y: e.clientY - rect.top,
    })
  }

  return (
    <div
      onMouseMove={handleMouseMove}
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
      className={cn("relative overflow-hidden", className)}
    >
      {children}
      <div
        className="pointer-events-none absolute -inset-px transition-opacity duration-300"
        style={{
          opacity: isHovered ? 1 : 0,
          background: `radial-gradient(600px circle at ${position.x}px ${position.y}px, ${glareColor}, transparent 40%)`,
        }}
      />
    </div>
  )
}
```

---

## Artifact-Ready Effects

### Self-Contained Border Beam Card

```jsx
export default function BorderBeamDemo() {
  return (
    <div className="flex items-center justify-center min-h-screen bg-black">
      <style>{`
        @keyframes border-beam {
          100% { offset-distance: 100%; }
        }
      `}</style>
      
      <div className="relative rounded-xl border border-gray-800 bg-gray-950 p-8 overflow-hidden">
        {/* Border beam effect */}
        <div
          className="pointer-events-none absolute inset-0 rounded-[inherit]"
          style={{
            border: '1.5px solid transparent',
            mask: 'linear-gradient(transparent, transparent), linear-gradient(white, white)',
            maskClip: 'padding-box, border-box',
            maskComposite: 'exclude',
          }}
        >
          <div
            className="absolute aspect-square w-[200px]"
            style={{
              background: 'linear-gradient(to left, #ffaa40, #9c40ff, transparent)',
              offsetPath: 'rect(0 auto auto 0 round 200px)',
              animation: 'border-beam 12s infinite linear',
            }}
          />
        </div>
        
        <h3 className="text-xl font-bold text-white mb-2">Magic Card</h3>
        <p className="text-gray-400">With animated border beam effect</p>
      </div>
    </div>
  )
}
```

### Self-Contained Meteors

```jsx
export default function MeteorsDemo() {
  return (
    <div className="relative flex h-screen w-full items-center justify-center overflow-hidden bg-slate-950">
      <style>{`
        @keyframes meteor {
          0% { transform: rotate(215deg) translateX(0); opacity: 1; }
          70% { opacity: 1; }
          100% { transform: rotate(215deg) translateX(-500px); opacity: 0; }
        }
      `}</style>
      
      {Array.from({ length: 20 }).map((_, i) => (
        <span
          key={i}
          className="absolute h-0.5 w-0.5 rounded-full bg-slate-500 shadow-[0_0_0_1px_#ffffff10]"
          style={{
            top: '0%',
            left: `${Math.random() * 100}%`,
            animation: `meteor ${2 + Math.random() * 8}s linear infinite`,
            animationDelay: `${Math.random() * 2}s`,
          }}
        >
          <span 
            className="absolute top-1/2 -translate-y-1/2 w-12 h-px"
            style={{
              background: 'linear-gradient(to right, #64748b, transparent)',
            }}
          />
        </span>
      ))}
      
      <div className="relative z-10 text-center">
        <h1 className="text-5xl font-bold text-white">Meteor Shower</h1>
        <p className="mt-4 text-slate-400">Watch the stars fall</p>
      </div>
    </div>
  )
}
```
