# Backgrounds Reference

Complete implementations for all background effect components.

---

## 1. DotPattern

A subtle dot grid background pattern.

```tsx
import { cn } from "@/lib/utils"
import { useId } from "react"

interface DotPatternProps {
  width?: number
  height?: number
  x?: number
  y?: number
  cx?: number
  cy?: number
  cr?: number
  className?: string
  [key: string]: unknown
}

export function DotPattern({
  width = 16,
  height = 16,
  x = 0,
  y = 0,
  cx = 1,
  cy = 1,
  cr = 1,
  className,
  ...props
}: DotPatternProps) {
  const id = useId()

  return (
    <svg
      aria-hidden="true"
      className={cn(
        "pointer-events-none absolute inset-0 h-full w-full fill-neutral-400/80",
        className
      )}
      {...props}
    >
      <defs>
        <pattern
          id={id}
          width={width}
          height={height}
          patternUnits="userSpaceOnUse"
          patternContentUnits="userSpaceOnUse"
          x={x}
          y={y}
        >
          <circle id="pattern-circle" cx={cx} cy={cy} r={cr} />
        </pattern>
      </defs>
      <rect width="100%" height="100%" strokeWidth={0} fill={`url(#${id})`} />
    </svg>
  )
}
```

**Usage:**
```tsx
<div className="relative h-screen w-full">
  <DotPattern className="[mask-image:radial-gradient(300px_circle_at_center,white,transparent)]" />
  {/* Content */}
</div>
```

---

## 2. GridPattern

A line-based grid background.

```tsx
import { cn } from "@/lib/utils"
import { useId } from "react"

interface GridPatternProps {
  width?: number
  height?: number
  x?: number
  y?: number
  strokeDasharray?: string
  squares?: [number, number][]
  className?: string
  [key: string]: unknown
}

export function GridPattern({
  width = 40,
  height = 40,
  x = -1,
  y = -1,
  strokeDasharray = "0",
  squares,
  className,
  ...props
}: GridPatternProps) {
  const id = useId()

  return (
    <svg
      aria-hidden="true"
      className={cn(
        "pointer-events-none absolute inset-0 h-full w-full fill-gray-400/30 stroke-gray-400/30",
        className
      )}
      {...props}
    >
      <defs>
        <pattern
          id={id}
          width={width}
          height={height}
          patternUnits="userSpaceOnUse"
          x={x}
          y={y}
        >
          <path
            d={`M.5 ${height}V.5H${width}`}
            fill="none"
            strokeDasharray={strokeDasharray}
          />
        </pattern>
      </defs>
      <rect width="100%" height="100%" strokeWidth={0} fill={`url(#${id})`} />
      {squares && (
        <svg x={x} y={y} className="overflow-visible">
          {squares.map(([squareX, squareY]) => (
            <rect
              strokeWidth="0"
              key={`${squareX}-${squareY}`}
              width={width - 1}
              height={height - 1}
              x={squareX * width + 1}
              y={squareY * height + 1}
            />
          ))}
        </svg>
      )}
    </svg>
  )
}
```

---

## 3. RetroGrid

Perspective retro/vaporwave style grid.

```tsx
import { cn } from "@/lib/utils"

interface RetroGridProps {
  className?: string
  angle?: number
}

export function RetroGrid({ className, angle = 65 }: RetroGridProps) {
  return (
    <div
      className={cn(
        "pointer-events-none absolute size-full overflow-hidden opacity-50 [perspective:200px]",
        className
      )}
      style={{ "--grid-angle": `${angle}deg` } as React.CSSProperties}
    >
      {/* Grid */}
      <div className="absolute inset-0 [transform:rotateX(var(--grid-angle))]">
        <div
          className={cn(
            "animate-grid",
            "[background-repeat:repeat] [background-size:60px_60px] [height:300vh] [inset:0%_0px] [margin-left:-50%] [transform-origin:100%_0_0] [width:600vw]",
            "[background-image:linear-gradient(to_right,rgba(0,0,0,0.3)_1px,transparent_0),linear-gradient(to_bottom,rgba(0,0,0,0.3)_1px,transparent_0)]",
            "dark:[background-image:linear-gradient(to_right,rgba(255,255,255,0.2)_1px,transparent_0),linear-gradient(to_bottom,rgba(255,255,255,0.2)_1px,transparent_0)]"
          )}
        />
      </div>
      {/* Background Gradient */}
      <div className="absolute inset-0 bg-gradient-to-t from-white to-transparent to-90% dark:from-black" />
    </div>
  )
}
```

**Required CSS:**
```css
@keyframes grid {
  0% { transform: translateY(-50%); }
  100% { transform: translateY(0); }
}

.animate-grid {
  animation: grid 15s linear infinite;
}
```

---

## 4. FlickeringGrid

Animated flickering grid cells.

```tsx
"use client"
import { useEffect, useRef, useState, useCallback } from "react"
import { cn } from "@/lib/utils"

interface FlickeringGridProps {
  squareSize?: number
  gridGap?: number
  flickerChance?: number
  color?: string
  maxOpacity?: number
  className?: string
}

export function FlickeringGrid({
  squareSize = 4,
  gridGap = 6,
  flickerChance = 0.3,
  color = "rgb(0, 0, 0)",
  maxOpacity = 0.3,
  className,
}: FlickeringGridProps) {
  const canvasRef = useRef<HTMLCanvasElement>(null)
  const [isInView, setIsInView] = useState(false)

  const setupCanvas = useCallback(
    (canvas: HTMLCanvasElement) => {
      const canvasWidth = canvas.clientWidth
      const canvasHeight = canvas.clientHeight
      const dpr = window.devicePixelRatio || 1
      canvas.width = canvasWidth * dpr
      canvas.height = canvasHeight * dpr
      canvas.style.width = `${canvasWidth}px`
      canvas.style.height = `${canvasHeight}px`
      const cols = Math.floor(canvasWidth / (squareSize + gridGap))
      const rows = Math.floor(canvasHeight / (squareSize + gridGap))
      return { cols, rows, dpr }
    },
    [squareSize, gridGap]
  )

  useEffect(() => {
    const canvas = canvasRef.current
    if (!canvas) return

    const ctx = canvas.getContext("2d")
    if (!ctx) return

    const { cols, rows, dpr } = setupCanvas(canvas)

    const drawGrid = () => {
      ctx.clearRect(0, 0, canvas.width, canvas.height)
      for (let i = 0; i < cols; i++) {
        for (let j = 0; j < rows; j++) {
          if (Math.random() < flickerChance) {
            ctx.fillStyle = color.replace(")", `, ${Math.random() * maxOpacity})`)
              .replace("rgb", "rgba")
            ctx.fillRect(
              i * (squareSize + gridGap) * dpr,
              j * (squareSize + gridGap) * dpr,
              squareSize * dpr,
              squareSize * dpr
            )
          }
        }
      }
    }

    let animationId: number
    const animate = () => {
      if (isInView) {
        drawGrid()
        animationId = requestAnimationFrame(animate)
      }
    }

    if (isInView) animate()
    return () => cancelAnimationFrame(animationId)
  }, [setupCanvas, flickerChance, color, maxOpacity, squareSize, gridGap, isInView])

  useEffect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => setIsInView(entry.isIntersecting),
      { threshold: 0 }
    )
    if (canvasRef.current) observer.observe(canvasRef.current)
    return () => observer.disconnect()
  }, [])

  return (
    <canvas
      ref={canvasRef}
      className={cn("pointer-events-none absolute inset-0 size-full", className)}
    />
  )
}
```

---

## 5. Ripple

Expanding ripple effect from center.

```tsx
import { cn } from "@/lib/utils"
import { CSSProperties } from "react"

interface RippleProps {
  mainCircleSize?: number
  mainCircleOpacity?: number
  numCircles?: number
  className?: string
}

export function Ripple({
  mainCircleSize = 210,
  mainCircleOpacity = 0.24,
  numCircles = 8,
  className,
}: RippleProps) {
  return (
    <div
      className={cn(
        "absolute inset-0 [mask-image:linear-gradient(to_bottom,white,transparent)]",
        className
      )}
    >
      {Array.from({ length: numCircles }, (_, i) => {
        const size = mainCircleSize + i * 70
        const opacity = mainCircleOpacity - i * 0.03
        const animationDelay = `${i * 0.06}s`

        return (
          <div
            key={i}
            className="absolute animate-ripple rounded-full bg-foreground/25 shadow-xl border"
            style={
              {
                width: `${size}px`,
                height: `${size}px`,
                opacity,
                animationDelay,
                top: "50%",
                left: "50%",
                transform: "translate(-50%, -50%) scale(1)",
              } as CSSProperties
            }
          />
        )
      })}
    </div>
  )
}
```

**Required CSS:**
```css
@keyframes ripple {
  0%, 100% {
    transform: translate(-50%, -50%) scale(1);
  }
  50% {
    transform: translate(-50%, -50%) scale(0.9);
  }
}

.animate-ripple {
  animation: ripple 3s ease-in-out infinite;
}
```

---

## 6. Particles

Floating particle effect.

```tsx
"use client"
import { useEffect, useRef, useState } from "react"
import { cn } from "@/lib/utils"

interface ParticlesProps {
  className?: string
  quantity?: number
  staticity?: number
  ease?: number
  refresh?: boolean
  color?: string
  size?: number
}

export function Particles({
  className,
  quantity = 100,
  staticity = 50,
  ease = 50,
  refresh = false,
  color = "#ffffff",
  size = 2,
}: ParticlesProps) {
  const canvasRef = useRef<HTMLCanvasElement>(null)
  const [context, setContext] = useState<CanvasRenderingContext2D | null>(null)
  const circles = useRef<any[]>([])
  const mouse = useRef({ x: 0, y: 0 })
  const canvasSize = useRef({ w: 0, h: 0 })

  useEffect(() => {
    if (canvasRef.current) {
      const ctx = canvasRef.current.getContext("2d")
      setContext(ctx)
    }
  }, [])

  useEffect(() => {
    const initCanvas = () => {
      resizeCanvas()
      drawParticles()
    }

    const resizeCanvas = () => {
      if (canvasRef.current && context) {
        circles.current = []
        canvasSize.current.w = canvasRef.current.offsetWidth
        canvasSize.current.h = canvasRef.current.offsetHeight
        canvasRef.current.width = canvasSize.current.w * window.devicePixelRatio
        canvasRef.current.height = canvasSize.current.h * window.devicePixelRatio
        canvasRef.current.style.width = `${canvasSize.current.w}px`
        canvasRef.current.style.height = `${canvasSize.current.h}px`
        context.scale(window.devicePixelRatio, window.devicePixelRatio)
      }
    }

    const drawParticles = () => {
      circles.current = []
      for (let i = 0; i < quantity; i++) {
        const x = Math.random() * canvasSize.current.w
        const y = Math.random() * canvasSize.current.h
        const translateX = 0
        const translateY = 0
        const pSize = Math.random() * size + 1
        const alpha = 0
        const targetAlpha = parseFloat((Math.random() * 0.6 + 0.1).toFixed(1))
        const dx = (Math.random() - 0.5) * 0.2
        const dy = (Math.random() - 0.5) * 0.2
        circles.current.push({ x, y, translateX, translateY, size: pSize, alpha, targetAlpha, dx, dy })
      }
    }

    const animate = () => {
      if (context) {
        context.clearRect(0, 0, canvasSize.current.w, canvasSize.current.h)
        circles.current.forEach((circle, i) => {
          const edge = [
            circle.x + circle.translateX - circle.size,
            canvasSize.current.w - circle.x - circle.translateX - circle.size,
            circle.y + circle.translateY - circle.size,
            canvasSize.current.h - circle.y - circle.translateY - circle.size,
          ]
          const closestEdge = edge.reduce((a, b) => Math.min(a, b))
          const remapClosestEdge = closestEdge / 20

          if (remapClosestEdge > 1) {
            circle.alpha += 0.02
            if (circle.alpha > circle.targetAlpha) circle.alpha = circle.targetAlpha
          } else {
            circle.alpha = circle.targetAlpha * remapClosestEdge
          }

          circle.x += circle.dx
          circle.y += circle.dy
          circle.translateX += (mouse.current.x / (staticity / circle.size) - circle.translateX) / ease
          circle.translateY += (mouse.current.y / (staticity / circle.size) - circle.translateY) / ease

          if (circle.x < -circle.size || circle.x > canvasSize.current.w + circle.size ||
              circle.y < -circle.size || circle.y > canvasSize.current.h + circle.size) {
            circles.current.splice(i, 1)
            const newCircle = {
              x: Math.random() * canvasSize.current.w,
              y: Math.random() * canvasSize.current.h,
              translateX: 0, translateY: 0,
              size: Math.random() * size + 1,
              alpha: 0,
              targetAlpha: parseFloat((Math.random() * 0.6 + 0.1).toFixed(1)),
              dx: (Math.random() - 0.5) * 0.2,
              dy: (Math.random() - 0.5) * 0.2,
            }
            circles.current.push(newCircle)
          }

          context.beginPath()
          context.arc(circle.x + circle.translateX, circle.y + circle.translateY, circle.size, 0, 2 * Math.PI)
          context.fillStyle = color.replace(")", `, ${circle.alpha})`).replace("rgb", "rgba")
          context.fill()
        })
      }
      requestAnimationFrame(animate)
    }

    initCanvas()
    animate()

    const handleMouseMove = (e: MouseEvent) => {
      if (canvasRef.current) {
        const rect = canvasRef.current.getBoundingClientRect()
        mouse.current.x = e.clientX - rect.left - canvasSize.current.w / 2
        mouse.current.y = e.clientY - rect.top - canvasSize.current.h / 2
      }
    }

    window.addEventListener("resize", resizeCanvas)
    window.addEventListener("mousemove", handleMouseMove)
    return () => {
      window.removeEventListener("resize", resizeCanvas)
      window.removeEventListener("mousemove", handleMouseMove)
    }
  }, [context, quantity, staticity, ease, color, size, refresh])

  return <canvas ref={canvasRef} className={cn("absolute inset-0", className)} />
}
```

---

## 7. AnimatedGridPattern

Moving animated grid lines.

```tsx
"use client"
import { useEffect, useId, useRef, useState } from "react"
import { motion } from "framer-motion"
import { cn } from "@/lib/utils"

interface AnimatedGridPatternProps {
  width?: number
  height?: number
  x?: number
  y?: number
  strokeDasharray?: any
  numSquares?: number
  className?: string
  maxOpacity?: number
  duration?: number
}

export function AnimatedGridPattern({
  width = 40,
  height = 40,
  x = -1,
  y = -1,
  strokeDasharray = 0,
  numSquares = 50,
  className,
  maxOpacity = 0.5,
  duration = 4,
  ...props
}: AnimatedGridPatternProps) {
  const id = useId()
  const containerRef = useRef<SVGSVGElement>(null)
  const [dimensions, setDimensions] = useState({ width: 0, height: 0 })
  const [squares, setSquares] = useState<Array<{ id: number; pos: [number, number] }>>([])

  function getPos() {
    return [
      Math.floor((Math.random() * dimensions.width) / width),
      Math.floor((Math.random() * dimensions.height) / height),
    ] as [number, number]
  }

  function generateSquares(count: number) {
    return Array.from({ length: count }, (_, i) => ({
      id: i,
      pos: getPos(),
    }))
  }

  useEffect(() => {
    if (dimensions.width && dimensions.height) {
      setSquares(generateSquares(numSquares))
    }
  }, [dimensions, numSquares])

  useEffect(() => {
    const resizeObserver = new ResizeObserver((entries) => {
      for (const entry of entries) {
        setDimensions({
          width: entry.contentRect.width,
          height: entry.contentRect.height,
        })
      }
    })

    if (containerRef.current) {
      resizeObserver.observe(containerRef.current)
    }

    return () => resizeObserver.disconnect()
  }, [])

  return (
    <svg
      ref={containerRef}
      aria-hidden="true"
      className={cn(
        "pointer-events-none absolute inset-0 h-full w-full fill-gray-400/30 stroke-gray-400/30",
        className
      )}
      {...props}
    >
      <defs>
        <pattern id={id} width={width} height={height} patternUnits="userSpaceOnUse" x={x} y={y}>
          <path d={`M.5 ${height}V.5H${width}`} fill="none" strokeDasharray={strokeDasharray} />
        </pattern>
      </defs>
      <rect width="100%" height="100%" fill={`url(#${id})`} />
      <svg x={x} y={y} className="overflow-visible">
        {squares.map(({ pos: [sqX, sqY], id: sqId }, index) => (
          <motion.rect
            initial={{ opacity: 0 }}
            animate={{ opacity: maxOpacity }}
            transition={{ duration, repeat: Infinity, delay: index * 0.1, repeatType: "reverse" }}
            key={`${sqX}-${sqY}-${sqId}`}
            width={width - 1}
            height={height - 1}
            x={sqX * width + 1}
            y={sqY * height + 1}
            fill="currentColor"
            strokeWidth="0"
          />
        ))}
      </svg>
    </svg>
  )
}
```

---

## Artifact-Ready Backgrounds

### Self-Contained Dot Pattern

```jsx
export default function DotPatternDemo() {
  return (
    <div className="relative flex h-screen w-full items-center justify-center overflow-hidden bg-white">
      <svg
        className="pointer-events-none absolute inset-0 h-full w-full fill-neutral-400/50"
        style={{
          maskImage: 'radial-gradient(400px circle at center, white, transparent)',
        }}
      >
        <defs>
          <pattern id="dotPattern" width="16" height="16" patternUnits="userSpaceOnUse">
            <circle cx="1" cy="1" r="1" />
          </pattern>
        </defs>
        <rect width="100%" height="100%" fill="url(#dotPattern)" />
      </svg>
      <h1 className="text-4xl font-bold">Your Content Here</h1>
    </div>
  )
}
```

### Self-Contained Retro Grid

```jsx
export default function RetroGridDemo() {
  return (
    <div className="relative flex h-screen w-full items-center justify-center overflow-hidden bg-black">
      <style>{`
        @keyframes grid-scroll {
          0% { transform: translateY(-50%); }
          100% { transform: translateY(0); }
        }
      `}</style>
      
      <div className="pointer-events-none absolute size-full overflow-hidden opacity-50" style={{ perspective: '200px' }}>
        <div className="absolute inset-0" style={{ transform: 'rotateX(65deg)' }}>
          <div
            className="w-[600vw] h-[300vh] ml-[-50%]"
            style={{
              backgroundImage: 'linear-gradient(to right, rgba(255,255,255,0.2) 1px, transparent 0), linear-gradient(to bottom, rgba(255,255,255,0.2) 1px, transparent 0)',
              backgroundSize: '60px 60px',
              animation: 'grid-scroll 15s linear infinite',
              transformOrigin: '100% 0 0',
            }}
          />
        </div>
        <div className="absolute inset-0 bg-gradient-to-t from-black to-transparent to-90%" />
      </div>
      
      <h1 className="relative z-10 text-6xl font-bold text-white">RETRO</h1>
    </div>
  )
}
```

### Self-Contained Ripple Background

```jsx
export default function RippleDemo() {
  return (
    <div className="relative flex h-screen w-full items-center justify-center overflow-hidden bg-gradient-to-br from-purple-900 to-black">
      <style>{`
        @keyframes ripple-expand {
          0%, 100% { transform: translate(-50%, -50%) scale(1); }
          50% { transform: translate(-50%, -50%) scale(0.9); }
        }
      `}</style>
      
      <div className="absolute inset-0" style={{ maskImage: 'linear-gradient(to bottom, white, transparent)' }}>
        {Array.from({ length: 8 }).map((_, i) => (
          <div
            key={i}
            className="absolute rounded-full border border-purple-500/30 bg-purple-500/10"
            style={{
              width: `${210 + i * 70}px`,
              height: `${210 + i * 70}px`,
              opacity: 0.24 - i * 0.03,
              top: '50%',
              left: '50%',
              transform: 'translate(-50%, -50%)',
              animation: `ripple-expand 3s ease-in-out ${i * 0.06}s infinite`,
            }}
          />
        ))}
      </div>
      
      <h1 className="relative z-10 text-5xl font-bold text-white">Ripple Effect</h1>
    </div>
  )
}
```
