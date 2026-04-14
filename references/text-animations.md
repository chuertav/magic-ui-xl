# Text Animations Reference

Complete implementations for all 20 text animation components.

---

## 1. TypingAnimation

Typewriter effect with blinking cursor.

```tsx
"use client"
import { useEffect, useState } from "react"
import { cn } from "@/lib/utils"

interface TypingAnimationProps {
  text: string
  duration?: number
  className?: string
}

export function TypingAnimation({
  text,
  duration = 100,
  className,
}: TypingAnimationProps) {
  const [displayedText, setDisplayedText] = useState("")
  const [i, setI] = useState(0)

  useEffect(() => {
    const typingEffect = setInterval(() => {
      if (i < text.length) {
        setDisplayedText(text.substring(0, i + 1))
        setI(i + 1)
      } else {
        clearInterval(typingEffect)
      }
    }, duration)

    return () => clearInterval(typingEffect)
  }, [duration, i, text])

  return (
    <h1 className={cn(
      "font-display text-center text-4xl font-bold tracking-[-0.02em] drop-shadow-sm md:text-7xl md:leading-[5rem]",
      className
    )}>
      {displayedText}
      <span className="animate-pulse">|</span>
    </h1>
  )
}
```

**Usage:**
```tsx
<TypingAnimation text="Welcome to our platform" duration={80} />
```

---

## 2. NumberTicker

Animated counting number with easing.

```tsx
"use client"
import { useEffect, useRef } from "react"
import { useInView, useMotionValue, useSpring } from "framer-motion"
import { cn } from "@/lib/utils"

interface NumberTickerProps {
  value: number
  direction?: "up" | "down"
  delay?: number
  className?: string
  decimalPlaces?: number
}

export function NumberTicker({
  value,
  direction = "up",
  delay = 0,
  className,
  decimalPlaces = 0,
}: NumberTickerProps) {
  const ref = useRef<HTMLSpanElement>(null)
  const motionValue = useMotionValue(direction === "down" ? value : 0)
  const springValue = useSpring(motionValue, {
    damping: 60,
    stiffness: 100,
  })
  const isInView = useInView(ref, { once: true, margin: "0px" })

  useEffect(() => {
    if (isInView) {
      setTimeout(() => {
        motionValue.set(direction === "down" ? 0 : value)
      }, delay * 1000)
    }
  }, [motionValue, isInView, delay, value, direction])

  useEffect(
    () =>
      springValue.on("change", (latest) => {
        if (ref.current) {
          ref.current.textContent = Intl.NumberFormat("en-US", {
            minimumFractionDigits: decimalPlaces,
            maximumFractionDigits: decimalPlaces,
          }).format(Number(latest.toFixed(decimalPlaces)))
        }
      }),
    [springValue, decimalPlaces]
  )

  return (
    <span
      ref={ref}
      className={cn(
        "inline-block tabular-nums text-black dark:text-white",
        className
      )}
    >
      {value}
    </span>
  )
}
```

**Usage:**
```tsx
<NumberTicker value={1000} />
<NumberTicker value={99.9} decimalPlaces={1} />
```

---

## 3. AnimatedGradientText

Moving gradient text effect.

```tsx
import { cn } from "@/lib/utils"
import { ReactNode } from "react"

interface AnimatedGradientTextProps {
  children: ReactNode
  className?: string
}

export function AnimatedGradientText({
  children,
  className,
}: AnimatedGradientTextProps) {
  return (
    <div
      className={cn(
        "group relative mx-auto flex max-w-fit flex-row items-center justify-center rounded-2xl bg-white/40 px-4 py-1.5 text-sm font-medium shadow-[inset_0_-8px_10px_#8fdfff1f] backdrop-blur-sm transition-shadow duration-500 ease-out [--bg-size:300%] hover:shadow-[inset_0_-5px_10px_#8fdfff3f] dark:bg-black/40",
        className
      )}
    >
      <div
        className="absolute inset-0 block h-full w-full animate-gradient bg-gradient-to-r from-[#ffaa40]/50 via-[#9c40ff]/50 to-[#ffaa40]/50 bg-[length:var(--bg-size)_100%] p-[1px] ![mask-composite:subtract] [border-radius:inherit] [mask:linear-gradient(#fff_0_0)_content-box,linear-gradient(#fff_0_0)]"
      />
      {children}
    </div>
  )
}
```

**Required CSS:**
```css
@keyframes gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.animate-gradient {
  animation: gradient 8s linear infinite;
}
```

**Usage:**
```tsx
<AnimatedGradientText>
  🎉 <span>Introducing Magic UI</span>
</AnimatedGradientText>
```

---

## 4. AnimatedShinyText

Shimmer/shine effect on text.

```tsx
import { cn } from "@/lib/utils"
import { CSSProperties, ReactNode } from "react"

interface AnimatedShinyTextProps {
  children: ReactNode
  className?: string
  shimmerWidth?: number
}

export function AnimatedShinyText({
  children,
  className,
  shimmerWidth = 100,
}: AnimatedShinyTextProps) {
  return (
    <p
      style={{ "--shimmer-width": `${shimmerWidth}px` } as CSSProperties}
      className={cn(
        "mx-auto max-w-md text-neutral-600/70 dark:text-neutral-400/70",
        "animate-shimmer bg-clip-text bg-no-repeat [background-position:0_0] [background-size:var(--shimmer-width)_100%] [transition:background-position_1s_cubic-bezier(.6,.6,0,1)_infinite]",
        "bg-gradient-to-r from-transparent via-black/80 via-50% to-transparent dark:via-white/80",
        className
      )}
    >
      {children}
    </p>
  )
}
```

**Required CSS:**
```css
@keyframes shimmer {
  0%, 90%, 100% { background-position: calc(-100% - var(--shimmer-width)) 0; }
  30%, 60% { background-position: calc(100% + var(--shimmer-width)) 0; }
}

.animate-shimmer {
  animation: shimmer 8s infinite;
}
```

---

## 5. AuroraText

Aurora borealis gradient effect.

```tsx
import { cn } from "@/lib/utils"
import { ReactNode } from "react"

interface AuroraTextProps {
  children: ReactNode
  className?: string
}

export function AuroraText({ children, className }: AuroraTextProps) {
  return (
    <span
      className={cn(
        "relative inline-flex overflow-hidden",
        className
      )}
    >
      <span className="animate-aurora bg-[linear-gradient(90deg,hsl(var(--color-1)),hsl(var(--color-2)),hsl(var(--color-3)),hsl(var(--color-4)),hsl(var(--color-5)))] bg-[length:200%_auto] bg-clip-text text-transparent">
        {children}
      </span>
    </span>
  )
}
```

**Required CSS Variables:**
```css
:root {
  --color-1: 0 100% 63%;
  --color-2: 270 100% 63%;
  --color-3: 210 100% 63%;
  --color-4: 195 100% 63%;
  --color-5: 90 100% 63%;
}

@keyframes aurora {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.animate-aurora {
  animation: aurora 6s ease-in-out infinite;
}
```

---

## 6. HyperText

Scramble/decode text effect on hover.

```tsx
"use client"
import { useEffect, useRef, useState } from "react"
import { cn } from "@/lib/utils"

interface HyperTextProps {
  text: string
  duration?: number
  className?: string
  animateOnLoad?: boolean
}

const alphabets = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("")

export function HyperText({
  text,
  duration = 800,
  className,
  animateOnLoad = true,
}: HyperTextProps) {
  const [displayText, setDisplayText] = useState(text.split(""))
  const [isAnimating, setIsAnimating] = useState(false)
  const iterationCount = useRef(0)

  const triggerAnimation = () => {
    if (isAnimating) return
    setIsAnimating(true)
    iterationCount.current = 0
  }

  useEffect(() => {
    if (!isAnimating) return

    const interval = setInterval(() => {
      if (iterationCount.current < text.length) {
        setDisplayText((prev) =>
          prev.map((char, index) =>
            char === " "
              ? char
              : index <= iterationCount.current
              ? text[index]
              : alphabets[Math.floor(Math.random() * 26)]
          )
        )
        iterationCount.current++
      } else {
        clearInterval(interval)
        setIsAnimating(false)
      }
    }, duration / text.length)

    return () => clearInterval(interval)
  }, [isAnimating, text, duration])

  useEffect(() => {
    if (animateOnLoad) triggerAnimation()
  }, [animateOnLoad])

  return (
    <span
      className={cn("inline-flex cursor-default overflow-hidden", className)}
      onMouseEnter={triggerAnimation}
    >
      {displayText.map((char, index) => (
        <span key={index} className="font-mono">
          {char}
        </span>
      ))}
    </span>
  )
}
```

---

## 7. WordRotate

Rotating words with animation.

```tsx
"use client"
import { useEffect, useState } from "react"
import { AnimatePresence, motion } from "framer-motion"
import { cn } from "@/lib/utils"

interface WordRotateProps {
  words: string[]
  duration?: number
  className?: string
}

export function WordRotate({
  words,
  duration = 2500,
  className,
}: WordRotateProps) {
  const [index, setIndex] = useState(0)

  useEffect(() => {
    const interval = setInterval(() => {
      setIndex((prevIndex) => (prevIndex + 1) % words.length)
    }, duration)
    return () => clearInterval(interval)
  }, [words, duration])

  return (
    <div className="overflow-hidden py-2">
      <AnimatePresence mode="wait">
        <motion.h1
          key={words[index]}
          initial={{ opacity: 0, y: -50 }}
          animate={{ opacity: 1, y: 0 }}
          exit={{ opacity: 0, y: 50 }}
          transition={{ duration: 0.3, ease: "easeInOut" }}
          className={cn("font-display font-bold", className)}
        >
          {words[index]}
        </motion.h1>
      </AnimatePresence>
    </div>
  )
}
```

**Usage:**
```tsx
<WordRotate words={["Fast", "Modern", "Beautiful"]} />
```

---

## 8. MorphingText

Smooth text morphing between words.

```tsx
"use client"
import { useEffect, useState } from "react"
import { cn } from "@/lib/utils"

interface MorphingTextProps {
  texts: string[]
  className?: string
}

export function MorphingText({ texts, className }: MorphingTextProps) {
  const [index, setIndex] = useState(0)
  const [isAnimating, setIsAnimating] = useState(false)

  useEffect(() => {
    const interval = setInterval(() => {
      setIsAnimating(true)
      setTimeout(() => {
        setIndex((prev) => (prev + 1) % texts.length)
        setIsAnimating(false)
      }, 500)
    }, 3000)
    return () => clearInterval(interval)
  }, [texts.length])

  return (
    <span
      className={cn(
        "inline-block transition-all duration-500",
        isAnimating ? "blur-sm opacity-0 scale-105" : "blur-0 opacity-100 scale-100",
        className
      )}
    >
      {texts[index]}
    </span>
  )
}
```

---

## 9. SparklesText

Text with floating sparkle particles.

```tsx
"use client"
import { useEffect, useState } from "react"
import { cn } from "@/lib/utils"

interface Sparkle {
  id: string
  x: string
  y: string
  color: string
  delay: number
  scale: number
}

interface SparklesTextProps {
  children: string
  className?: string
  sparklesCount?: number
  colors?: { first: string; second: string }
}

export function SparklesText({
  children,
  className,
  sparklesCount = 10,
  colors = { first: "#9E7AFF", second: "#FE8BBB" },
}: SparklesTextProps) {
  const [sparkles, setSparkles] = useState<Sparkle[]>([])

  useEffect(() => {
    const generateSparkles = () => {
      return Array.from({ length: sparklesCount }, (_, i) => ({
        id: `sparkle-${i}`,
        x: `${Math.random() * 100}%`,
        y: `${Math.random() * 100}%`,
        color: Math.random() > 0.5 ? colors.first : colors.second,
        delay: Math.random() * 2,
        scale: Math.random() * 0.5 + 0.5,
      }))
    }
    setSparkles(generateSparkles())
  }, [sparklesCount, colors])

  return (
    <span className={cn("relative inline-block", className)}>
      {sparkles.map((sparkle) => (
        <span
          key={sparkle.id}
          className="pointer-events-none absolute animate-sparkle"
          style={{
            left: sparkle.x,
            top: sparkle.y,
            animationDelay: `${sparkle.delay}s`,
            transform: `scale(${sparkle.scale})`,
          }}
        >
          <svg
            width="21"
            height="21"
            viewBox="0 0 21 21"
            fill="none"
          >
            <path
              d="M10.5 0C10.5 0 10.5 7.5 10.5 10.5C10.5 13.5 10.5 21 10.5 21C10.5 21 7.5 13.5 0 10.5C7.5 7.5 10.5 0 10.5 0Z"
              fill={sparkle.color}
            />
            <path
              d="M10.5 0C10.5 0 10.5 7.5 10.5 10.5C10.5 13.5 10.5 21 10.5 21C10.5 21 13.5 13.5 21 10.5C13.5 7.5 10.5 0 10.5 0Z"
              fill={sparkle.color}
            />
          </svg>
        </span>
      ))}
      <span className="relative z-10">{children}</span>
    </span>
  )
}
```

**Required CSS:**
```css
@keyframes sparkle {
  0%, 100% { opacity: 0; transform: scale(0); }
  50% { opacity: 1; transform: scale(1); }
}

.animate-sparkle {
  animation: sparkle 2s ease-in-out infinite;
}
```

---

## 10. TextReveal

Scroll-based text reveal effect.

```tsx
"use client"
import { useRef } from "react"
import { motion, useScroll, useTransform } from "framer-motion"
import { cn } from "@/lib/utils"

interface TextRevealProps {
  text: string
  className?: string
}

export function TextReveal({ text, className }: TextRevealProps) {
  const containerRef = useRef<HTMLDivElement>(null)
  const { scrollYProgress } = useScroll({
    target: containerRef,
    offset: ["start 0.9", "start 0.25"],
  })

  const words = text.split(" ")

  return (
    <div ref={containerRef} className={cn("relative z-0 h-[200vh]", className)}>
      <div className="sticky top-0 mx-auto flex h-[50%] max-w-4xl items-center bg-transparent px-[1rem] py-[5rem]">
        <p className="flex flex-wrap p-5 text-2xl font-bold text-black/20 dark:text-white/20 md:p-8 md:text-3xl lg:p-10 lg:text-4xl xl:text-5xl">
          {words.map((word, i) => {
            const start = i / words.length
            const end = start + 1 / words.length
            return (
              <Word key={i} progress={scrollYProgress} range={[start, end]}>
                {word}
              </Word>
            )
          })}
        </p>
      </div>
    </div>
  )
}

interface WordProps {
  children: string
  progress: any
  range: [number, number]
}

function Word({ children, progress, range }: WordProps) {
  const opacity = useTransform(progress, range, [0, 1])
  return (
    <span className="relative mx-1 lg:mx-2.5">
      <span className="absolute opacity-30">{children}</span>
      <motion.span style={{ opacity }} className="text-black dark:text-white">
        {children}
      </motion.span>
    </span>
  )
}
```

---

## 11. SpinningText

Circular spinning text around a center point.

```tsx
"use client"
import { cn } from "@/lib/utils"

interface SpinningTextProps {
  children: string
  className?: string
  duration?: number
  radius?: number
}

export function SpinningText({
  children,
  className,
  duration = 10,
  radius = 80,
}: SpinningTextProps) {
  const characters = children.split("")

  return (
    <div
      className={cn("relative", className)}
      style={{ width: radius * 2, height: radius * 2 }}
    >
      <div
        className="absolute inset-0 animate-spin"
        style={{ animationDuration: `${duration}s` }}
      >
        {characters.map((char, i) => (
          <span
            key={i}
            className="absolute left-1/2 top-0 origin-[0_100px] -translate-x-1/2"
            style={{
              transform: `rotate(${(360 / characters.length) * i}deg)`,
              transformOrigin: `center ${radius}px`,
            }}
          >
            {char}
          </span>
        ))}
      </div>
    </div>
  )
}
```

---

## 12. ScrollBasedVelocity

Text that changes size based on scroll speed.

```tsx
"use client"
import { useRef } from "react"
import { motion, useScroll, useSpring, useTransform, useMotionValue, useVelocity, useAnimationFrame } from "framer-motion"
import { cn } from "@/lib/utils"

interface VelocityScrollProps {
  text: string
  defaultVelocity?: number
  className?: string
}

export function VelocityScroll({
  text,
  defaultVelocity = 5,
  className,
}: VelocityScrollProps) {
  const baseX = useMotionValue(0)
  const { scrollY } = useScroll()
  const scrollVelocity = useVelocity(scrollY)
  const smoothVelocity = useSpring(scrollVelocity, {
    damping: 50,
    stiffness: 400,
  })
  const velocityFactor = useTransform(smoothVelocity, [0, 1000], [0, 5], {
    clamp: false,
  })

  const x = useTransform(baseX, (v) => `${wrap(-20, -45, v)}%`)
  const directionFactor = useRef<number>(1)

  useAnimationFrame((t, delta) => {
    let moveBy = directionFactor.current * defaultVelocity * (delta / 1000)

    if (velocityFactor.get() < 0) {
      directionFactor.current = -1
    } else if (velocityFactor.get() > 0) {
      directionFactor.current = 1
    }

    moveBy += directionFactor.current * moveBy * velocityFactor.get()
    baseX.set(baseX.get() + moveBy)
  })

  return (
    <div className="relative m-0 flex flex-nowrap overflow-hidden whitespace-nowrap">
      <motion.div
        className={cn("flex flex-nowrap whitespace-nowrap text-4xl font-bold", className)}
        style={{ x }}
      >
        {Array.from({ length: 4 }).map((_, i) => (
          <span key={i} className="mr-10">
            {text}
          </span>
        ))}
      </motion.div>
    </div>
  )
}

function wrap(min: number, max: number, v: number) {
  const range = max - min
  return ((((v - min) % range) + range) % range) + min
}
```

---

## Artifact-Ready Versions

For Claude artifacts (no external dependencies), use this simplified pattern:

```jsx
// Self-contained typing animation for artifacts
export default function TypingDemo() {
  const [text, setText] = React.useState('')
  const fullText = "Welcome to Magic UI"
  
  React.useEffect(() => {
    let i = 0
    const interval = setInterval(() => {
      if (i <= fullText.length) {
        setText(fullText.slice(0, i))
        i++
      } else {
        clearInterval(interval)
      }
    }, 80)
    return () => clearInterval(interval)
  }, [])

  return (
    <div className="flex items-center justify-center min-h-screen bg-gradient-to-br from-purple-900 to-black">
      <h1 className="text-4xl font-bold text-white">
        {text}
        <span className="animate-pulse text-purple-400">|</span>
      </h1>
    </div>
  )
}
```
