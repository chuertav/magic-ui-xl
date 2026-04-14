# Buttons Reference

Complete implementations for all animated button components.

---

## 1. ShimmerButton

A button with a traveling light shimmer effect around the perimeter.

```tsx
import { cn } from "@/lib/utils"
import { ButtonHTMLAttributes, CSSProperties, ReactNode } from "react"

interface ShimmerButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  shimmerColor?: string
  shimmerSize?: string
  borderRadius?: string
  shimmerDuration?: string
  background?: string
  className?: string
  children?: ReactNode
}

export function ShimmerButton({
  shimmerColor = "#ffffff",
  shimmerSize = "0.05em",
  borderRadius = "100px",
  shimmerDuration = "3s",
  background = "rgba(0, 0, 0, 1)",
  className,
  children,
  ...props
}: ShimmerButtonProps) {
  return (
    <button
      style={
        {
          "--shimmer-color": shimmerColor,
          "--shimmer-size": shimmerSize,
          "--border-radius": borderRadius,
          "--shimmer-duration": shimmerDuration,
          "--background": background,
        } as CSSProperties
      }
      className={cn(
        "group relative z-0 flex cursor-pointer items-center justify-center overflow-hidden whitespace-nowrap border border-white/10 px-6 py-3 text-white [background:var(--background)] [border-radius:var(--border-radius)]",
        "transform-gpu transition-transform duration-300 ease-in-out active:translate-y-px",
        className
      )}
      {...props}
    >
      {/* Shimmer effect */}
      <div
        className={cn(
          "absolute inset-0 overflow-visible [container-type:size]",
          "-z-30 blur-[2px]",
          "animate-shimmer-slide [aspect-ratio:1] [border-radius:0]"
        )}
        style={{
          background: `conic-gradient(from 0deg, transparent 0 340deg, var(--shimmer-color) 360deg)`,
        }}
      />
      
      {/* Background */}
      <div
        className={cn(
          "absolute -z-20 [background:var(--background)] [border-radius:var(--border-radius)] [inset:var(--shimmer-size)]"
        )}
      />
      
      {children}
    </button>
  )
}
```

**Required CSS:**
```css
@keyframes shimmer-slide {
  to {
    transform: translate(calc(100cqw - 100%), calc(100cqh - 100%));
  }
}

.animate-shimmer-slide {
  animation: shimmer-slide var(--shimmer-duration) ease-in-out infinite alternate;
}
```

**Usage:**
```tsx
<ShimmerButton className="shadow-2xl">
  <span className="text-sm font-medium">Get Started</span>
</ShimmerButton>
```

---

## 2. RainbowButton

Button with animated rainbow gradient border.

```tsx
import { cn } from "@/lib/utils"
import { ButtonHTMLAttributes, ReactNode } from "react"

interface RainbowButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  children: ReactNode
  className?: string
}

export function RainbowButton({
  children,
  className,
  ...props
}: RainbowButtonProps) {
  return (
    <button
      className={cn(
        "group relative inline-flex h-11 animate-rainbow cursor-pointer items-center justify-center rounded-xl border-0 bg-[length:200%] px-8 py-2 font-medium text-white transition-colors [background-clip:padding-box,border-box,border-box] [background-origin:border-box] [border:calc(0.08*1rem)_solid_transparent]",
        "focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-ring disabled:pointer-events-none disabled:opacity-50",
        // Background layers
        "bg-[linear-gradient(#121213,#121213),linear-gradient(#121213_50%,rgba(18,18,19,0.6)_80%,rgba(18,18,19,0)),linear-gradient(90deg,hsl(var(--color-1)),hsl(var(--color-5)),hsl(var(--color-3)),hsl(var(--color-4)),hsl(var(--color-2)))]",
        // Dark mode
        "dark:bg-[linear-gradient(#fff,#fff),linear-gradient(#fff_50%,rgba(255,255,255,0.6)_80%,rgba(0,0,0,0)),linear-gradient(90deg,hsl(var(--color-1)),hsl(var(--color-5)),hsl(var(--color-3)),hsl(var(--color-4)),hsl(var(--color-2)))]",
        className
      )}
      {...props}
    >
      {children}
    </button>
  )
}
```

**Required CSS:**
```css
:root {
  --color-1: 0 100% 63%;
  --color-2: 270 100% 63%;
  --color-3: 210 100% 63%;
  --color-4: 195 100% 63%;
  --color-5: 90 100% 63%;
}

@keyframes rainbow {
  0% { background-position: 0%; }
  100% { background-position: 200%; }
}

.animate-rainbow {
  animation: rainbow var(--speed, 2s) infinite linear;
}
```

---

## 3. RippleButton

Button with click ripple effect.

```tsx
"use client"
import { useState, MouseEvent, ButtonHTMLAttributes, ReactNode } from "react"
import { cn } from "@/lib/utils"

interface RippleButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  children: ReactNode
  className?: string
  rippleColor?: string
}

interface Ripple {
  x: number
  y: number
  id: number
}

export function RippleButton({
  children,
  className,
  rippleColor = "rgba(255, 255, 255, 0.5)",
  onClick,
  ...props
}: RippleButtonProps) {
  const [ripples, setRipples] = useState<Ripple[]>([])

  const handleClick = (e: MouseEvent<HTMLButtonElement>) => {
    const rect = e.currentTarget.getBoundingClientRect()
    const x = e.clientX - rect.left
    const y = e.clientY - rect.top
    const id = Date.now()

    setRipples((prev) => [...prev, { x, y, id }])

    setTimeout(() => {
      setRipples((prev) => prev.filter((ripple) => ripple.id !== id))
    }, 1000)

    onClick?.(e)
  }

  return (
    <button
      className={cn(
        "relative overflow-hidden rounded-lg bg-primary px-6 py-3 text-primary-foreground transition-colors hover:bg-primary/90",
        className
      )}
      onClick={handleClick}
      {...props}
    >
      {ripples.map((ripple) => (
        <span
          key={ripple.id}
          className="absolute animate-ripple rounded-full"
          style={{
            left: ripple.x,
            top: ripple.y,
            backgroundColor: rippleColor,
            transform: "translate(-50%, -50%)",
          }}
        />
      ))}
      <span className="relative z-10">{children}</span>
    </button>
  )
}
```

**Required CSS:**
```css
@keyframes ripple {
  0% {
    width: 0;
    height: 0;
    opacity: 0.5;
  }
  100% {
    width: 500px;
    height: 500px;
    opacity: 0;
  }
}

.animate-ripple {
  animation: ripple 1s linear forwards;
}
```

---

## 4. PulsatingButton

Button with continuous pulse animation.

```tsx
import { cn } from "@/lib/utils"
import { ButtonHTMLAttributes, ReactNode } from "react"

interface PulsatingButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  children: ReactNode
  className?: string
  pulseColor?: string
  duration?: string
}

export function PulsatingButton({
  children,
  className,
  pulseColor = "#0096ff",
  duration = "1.5s",
  ...props
}: PulsatingButtonProps) {
  return (
    <button
      className={cn(
        "relative flex cursor-pointer items-center justify-center rounded-lg bg-blue-500 px-6 py-3 text-center text-white",
        className
      )}
      style={
        {
          "--pulse-color": pulseColor,
          "--duration": duration,
        } as React.CSSProperties
      }
      {...props}
    >
      <div className="relative z-10">{children}</div>
      <div className="absolute left-1/2 top-1/2 size-full -translate-x-1/2 -translate-y-1/2 animate-pulse rounded-lg bg-inherit" />
    </button>
  )
}
```

**Required CSS:**
```css
@keyframes pulse {
  0% {
    transform: translate(-50%, -50%) scale(1);
    opacity: 1;
  }
  100% {
    transform: translate(-50%, -50%) scale(1.5);
    opacity: 0;
  }
}
```

---

## 5. ShinyButton

Button with shine effect on hover.

```tsx
import { cn } from "@/lib/utils"
import { motion, type AnimationProps } from "framer-motion"
import { ButtonHTMLAttributes, ReactNode } from "react"

interface ShinyButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  children: ReactNode
  className?: string
}

const animationProps: AnimationProps = {
  initial: { "--x": "100%", scale: 0.8 },
  animate: { "--x": "-100%", scale: 1 },
  whileTap: { scale: 0.95 },
  transition: {
    repeat: Infinity,
    repeatType: "loop",
    repeatDelay: 1,
    type: "spring",
    stiffness: 20,
    damping: 15,
    mass: 2,
    scale: {
      type: "spring",
      stiffness: 200,
      damping: 5,
      mass: 0.5,
    },
  },
}

export function ShinyButton({
  children,
  className,
  ...props
}: ShinyButtonProps) {
  return (
    <motion.button
      {...animationProps}
      className={cn(
        "relative rounded-lg px-6 py-2 font-medium backdrop-blur-xl transition-shadow duration-300 ease-in-out hover:shadow dark:bg-[radial-gradient(circle_at_50%_0%,hsl(var(--primary)/10%)_0%,transparent_60%)] dark:hover:shadow-[0_0_20px_hsl(var(--primary)/10%)]",
        className
      )}
      {...props}
    >
      <span
        className="relative block size-full text-sm uppercase tracking-wide text-[rgb(0,0,0,65%)] dark:font-light dark:text-[rgb(255,255,255,90%)]"
        style={{
          maskImage:
            "linear-gradient(-75deg,hsl(var(--primary)) calc(var(--x) + 20%),transparent calc(var(--x) + 30%),hsl(var(--primary)) calc(var(--x) + 100%))",
        }}
      >
        {children}
      </span>
      <span
        style={{
          mask: "linear-gradient(rgb(0,0,0), rgb(0,0,0)) content-box,linear-gradient(rgb(0,0,0), rgb(0,0,0))",
          maskComposite: "exclude",
        }}
        className="absolute inset-0 z-10 block rounded-[inherit] bg-[linear-gradient(-75deg,hsl(var(--primary)/10%)_calc(var(--x)+20%),hsl(var(--primary)/50%)_calc(var(--x)+25%),hsl(var(--primary)/10%)_calc(var(--x)+100%))] p-px"
      />
    </motion.button>
  )
}
```

---

## 6. InteractiveHoverButton

Button with sliding background on hover.

```tsx
import { cn } from "@/lib/utils"
import { ArrowRight } from "lucide-react"
import { ButtonHTMLAttributes, ReactNode } from "react"

interface InteractiveHoverButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  children?: ReactNode
  className?: string
}

export function InteractiveHoverButton({
  children = "Button",
  className,
  ...props
}: InteractiveHoverButtonProps) {
  return (
    <button
      className={cn(
        "group relative w-32 cursor-pointer overflow-hidden rounded-full border bg-background p-2 text-center font-semibold",
        className
      )}
      {...props}
    >
      <span className="inline-block translate-x-1 transition-all duration-300 group-hover:translate-x-12 group-hover:opacity-0">
        {children}
      </span>
      <div className="absolute top-0 z-10 flex h-full w-full translate-x-12 items-center justify-center gap-2 text-primary-foreground opacity-0 transition-all duration-300 group-hover:-translate-x-1 group-hover:opacity-100">
        <span>{children}</span>
        <ArrowRight />
      </div>
      <div className="absolute left-[20%] top-[40%] h-2 w-2 scale-[1] rounded-lg bg-primary transition-all duration-300 group-hover:left-[0%] group-hover:top-[0%] group-hover:h-full group-hover:w-full group-hover:scale-[1.8] group-hover:bg-primary" />
    </button>
  )
}
```

---

## Artifact-Ready Versions (No External Dependencies)

### Self-Contained Shimmer Button

```jsx
export default function ShimmerButtonDemo() {
  return (
    <div className="flex items-center justify-center min-h-screen bg-gray-950">
      <style>{`
        @keyframes shimmer-slide {
          to {
            transform: translate(calc(100cqw - 100%), calc(100cqh - 100%));
          }
        }
      `}</style>
      
      <button className="group relative z-0 flex cursor-pointer items-center justify-center overflow-hidden whitespace-nowrap border border-white/10 px-6 py-3 text-white bg-black rounded-full transform-gpu transition-transform duration-300 ease-in-out active:translate-y-px">
        {/* Shimmer effect */}
        <div
          className="absolute inset-0 overflow-visible -z-30 blur-[2px]"
          style={{
            containerType: 'size',
            aspectRatio: 1,
            borderRadius: 0,
            animation: 'shimmer-slide 3s ease-in-out infinite alternate',
            background: 'conic-gradient(from 0deg, transparent 0 340deg, white 360deg)',
          }}
        />
        
        {/* Background */}
        <div className="absolute -z-20 bg-black rounded-full inset-[0.05em]" />
        
        <span className="text-sm font-medium">Get Started</span>
      </button>
    </div>
  )
}
```

### Self-Contained Ripple Button

```jsx
export default function RippleButtonDemo() {
  const [ripples, setRipples] = React.useState([])

  const handleClick = (e) => {
    const rect = e.currentTarget.getBoundingClientRect()
    const x = e.clientX - rect.left
    const y = e.clientY - rect.top
    const id = Date.now()

    setRipples(prev => [...prev, { x, y, id }])
    setTimeout(() => {
      setRipples(prev => prev.filter(r => r.id !== id))
    }, 1000)
  }

  return (
    <div className="flex items-center justify-center min-h-screen bg-gray-100">
      <style>{`
        @keyframes ripple {
          0% { width: 0; height: 0; opacity: 0.5; }
          100% { width: 500px; height: 500px; opacity: 0; }
        }
      `}</style>
      
      <button
        onClick={handleClick}
        className="relative overflow-hidden rounded-lg bg-blue-500 px-6 py-3 text-white transition-colors hover:bg-blue-600"
      >
        {ripples.map(ripple => (
          <span
            key={ripple.id}
            className="absolute rounded-full bg-white/50"
            style={{
              left: ripple.x,
              top: ripple.y,
              transform: 'translate(-50%, -50%)',
              animation: 'ripple 1s linear forwards',
            }}
          />
        ))}
        <span className="relative z-10">Click Me</span>
      </button>
    </div>
  )
}
```

### Self-Contained Pulsating Button

```jsx
export default function PulsatingButtonDemo() {
  return (
    <div className="flex items-center justify-center min-h-screen bg-gray-900">
      <style>{`
        @keyframes pulse-ring {
          0% { transform: scale(1); opacity: 0.8; }
          100% { transform: scale(1.5); opacity: 0; }
        }
      `}</style>
      
      <button className="relative flex cursor-pointer items-center justify-center rounded-lg bg-blue-500 px-6 py-3 text-white font-medium">
        <span className="relative z-10">Subscribe Now</span>
        <span 
          className="absolute inset-0 rounded-lg bg-blue-500"
          style={{ animation: 'pulse-ring 1.5s ease-out infinite' }}
        />
      </button>
    </div>
  )
}
```
