# Advanced Components Reference

Complex interactive components for rich user experiences.

---

## 1. Globe

Interactive 3D globe using Three.js/Cobe.

```tsx
"use client"
import { useEffect, useRef } from "react"
import createGlobe from "cobe"

interface GlobeProps {
  className?: string
  config?: {
    width?: number
    height?: number
    phi?: number
    theta?: number
    dark?: number
    diffuse?: number
    mapSamples?: number
    mapBrightness?: number
    baseColor?: [number, number, number]
    markerColor?: [number, number, number]
    glowColor?: [number, number, number]
    markers?: Array<{ location: [number, number]; size: number }>
  }
}

export function Globe({ className, config = {} }: GlobeProps) {
  const canvasRef = useRef<HTMLCanvasElement>(null)
  const pointerInteracting = useRef<number | null>(null)
  const pointerInteractionMovement = useRef(0)

  useEffect(() => {
    let phi = config.phi || 0
    let width = 0

    const onResize = () => {
      if (canvasRef.current) {
        width = canvasRef.current.offsetWidth
      }
    }
    onResize()
    window.addEventListener("resize", onResize)

    const globe = createGlobe(canvasRef.current!, {
      devicePixelRatio: 2,
      width: width * 2,
      height: width * 2,
      phi: config.phi || 0,
      theta: config.theta || 0.3,
      dark: config.dark || 1,
      diffuse: config.diffuse || 3,
      mapSamples: config.mapSamples || 16000,
      mapBrightness: config.mapBrightness || 1.2,
      baseColor: config.baseColor || [0.4, 0.6, 1],
      markerColor: config.markerColor || [1, 0.5, 1],
      glowColor: config.glowColor || [0.4, 0.6, 1],
      markers: config.markers || [
        { location: [37.78, -122.41], size: 0.1 }, // San Francisco
        { location: [51.5, -0.12], size: 0.1 },    // London
        { location: [35.68, 139.69], size: 0.1 },  // Tokyo
      ],
      onRender: (state) => {
        if (!pointerInteracting.current) {
          phi += 0.005
        }
        state.phi = phi + pointerInteractionMovement.current
        state.width = width * 2
        state.height = width * 2
      },
    })

    setTimeout(() => (canvasRef.current!.style.opacity = "1"))

    return () => {
      globe.destroy()
      window.removeEventListener("resize", onResize)
    }
  }, [config])

  return (
    <div className={className}>
      <canvas
        ref={canvasRef}
        onPointerDown={(e) => {
          pointerInteracting.current = e.clientX - pointerInteractionMovement.current
          canvasRef.current!.style.cursor = "grabbing"
        }}
        onPointerUp={() => {
          pointerInteracting.current = null
          canvasRef.current!.style.cursor = "grab"
        }}
        onPointerOut={() => {
          pointerInteracting.current = null
          canvasRef.current!.style.cursor = "grab"
        }}
        onMouseMove={(e) => {
          if (pointerInteracting.current !== null) {
            const delta = e.clientX - pointerInteracting.current
            pointerInteractionMovement.current = delta
          }
        }}
        onTouchMove={(e) => {
          if (pointerInteracting.current !== null && e.touches[0]) {
            const delta = e.touches[0].clientX - pointerInteracting.current
            pointerInteractionMovement.current = delta
          }
        }}
        style={{
          width: "100%",
          height: "100%",
          cursor: "grab",
          contain: "layout paint size",
          opacity: 0,
          transition: "opacity 1s ease",
        }}
      />
    </div>
  )
}
```

**Dependencies:** `cobe` (npm install cobe)

**Usage:**
```tsx
<Globe
  className="w-80 h-80"
  config={{
    markers: [
      { location: [19.43, -99.13], size: 0.15 }, // Mexico City
      { location: [40.71, -74.01], size: 0.1 },  // New York
    ]
  }}
/>
```

---

## 2. IconCloud

Floating 3D sphere of icons/logos.

```tsx
"use client"
import { useEffect, useMemo, useState } from "react"
import { Cloud, fetchSimpleIcons, renderSimpleIcon, ICloud } from "react-icon-cloud"

interface IconCloudProps {
  iconSlugs: string[]
}

export function IconCloud({ iconSlugs }: IconCloudProps) {
  const [data, setData] = useState<any>(null)

  useEffect(() => {
    fetchSimpleIcons({ slugs: iconSlugs }).then(setData)
  }, [iconSlugs])

  const renderedIcons = useMemo(() => {
    if (!data) return null
    return Object.values(data.simpleIcons).map((icon: any) =>
      renderSimpleIcon({
        icon,
        size: 42,
        aProps: {
          href: undefined,
          target: undefined,
          rel: undefined,
          onClick: (e: any) => e.preventDefault(),
        },
      })
    )
  }, [data])

  const cloudProps: ICloud = {
    containerProps: {
      style: {
        display: "flex",
        justifyContent: "center",
        alignItems: "center",
        width: "100%",
        paddingTop: 40,
      },
    },
    options: {
      reverse: true,
      depth: 1,
      wheelZoom: false,
      imageScale: 2,
      activeCursor: "default",
      tooltip: "native",
      initial: [0.1, -0.1],
      clickToFront: 500,
      tooltipDelay: 0,
      outlineColour: "#0000",
      maxSpeed: 0.04,
      minSpeed: 0.02,
    },
  }

  return (
    <Cloud {...cloudProps}>
      {renderedIcons}
    </Cloud>
  )
}
```

**Dependencies:** `react-icon-cloud`

**Usage:**
```tsx
<IconCloud
  iconSlugs={[
    "typescript", "javascript", "react", "nextdotjs", "vercel",
    "github", "gitlab", "visualstudiocode", "figma", "tailwindcss"
  ]}
/>
```

---

## 3. Lens

Magnifying lens effect on hover.

```tsx
"use client"
import { useState, useRef, MouseEvent, ReactNode } from "react"
import { motion, AnimatePresence } from "framer-motion"
import { cn } from "@/lib/utils"

interface LensProps {
  children: ReactNode
  zoomFactor?: number
  lensSize?: number
  className?: string
}

export function Lens({
  children,
  zoomFactor = 1.5,
  lensSize = 170,
  className,
}: LensProps) {
  const [isHovering, setIsHovering] = useState(false)
  const [mousePosition, setMousePosition] = useState({ x: 0, y: 0 })
  const containerRef = useRef<HTMLDivElement>(null)

  const handleMouseMove = (e: MouseEvent<HTMLDivElement>) => {
    if (containerRef.current) {
      const rect = containerRef.current.getBoundingClientRect()
      const x = e.clientX - rect.left
      const y = e.clientY - rect.top
      setMousePosition({ x, y })
    }
  }

  return (
    <div
      ref={containerRef}
      className={cn("relative overflow-hidden", className)}
      onMouseEnter={() => setIsHovering(true)}
      onMouseLeave={() => setIsHovering(false)}
      onMouseMove={handleMouseMove}
    >
      {children}
      
      <AnimatePresence>
        {isHovering && (
          <motion.div
            initial={{ opacity: 0, scale: 0.8 }}
            animate={{ opacity: 1, scale: 1 }}
            exit={{ opacity: 0, scale: 0.8 }}
            className="absolute pointer-events-none z-50 rounded-full border-2 border-white/50 shadow-xl overflow-hidden"
            style={{
              width: lensSize,
              height: lensSize,
              left: mousePosition.x - lensSize / 2,
              top: mousePosition.y - lensSize / 2,
            }}
          >
            <div
              style={{
                position: "absolute",
                width: containerRef.current?.offsetWidth,
                height: containerRef.current?.offsetHeight,
                transform: `scale(${zoomFactor})`,
                transformOrigin: `${mousePosition.x}px ${mousePosition.y}px`,
                left: -(mousePosition.x - lensSize / 2),
                top: -(mousePosition.y - lensSize / 2),
              }}
            >
              {children}
            </div>
          </motion.div>
        )}
      </AnimatePresence>
    </div>
  )
}
```

**Usage:**
```tsx
<Lens zoomFactor={2} lensSize={200}>
  <img src="/product-image.jpg" alt="Product" className="w-full" />
</Lens>
```

---

## 4. FileTree

Interactive file explorer tree structure.

```tsx
"use client"
import { useState, ReactNode } from "react"
import { cn } from "@/lib/utils"
import { ChevronRight, File, Folder, FolderOpen } from "lucide-react"

interface TreeNode {
  name: string
  type: "file" | "folder"
  children?: TreeNode[]
  icon?: ReactNode
}

interface FileTreeProps {
  data: TreeNode[]
  className?: string
}

function TreeItem({ node, level = 0 }: { node: TreeNode; level?: number }) {
  const [isOpen, setIsOpen] = useState(false)
  const isFolder = node.type === "folder"

  return (
    <div>
      <div
        className={cn(
          "flex items-center gap-1 py-1 px-2 rounded-md hover:bg-muted cursor-pointer select-none",
          "text-sm text-muted-foreground hover:text-foreground transition-colors"
        )}
        style={{ paddingLeft: `${level * 16 + 8}px` }}
        onClick={() => isFolder && setIsOpen(!isOpen)}
      >
        {isFolder ? (
          <>
            <ChevronRight
              className={cn(
                "h-4 w-4 shrink-0 transition-transform",
                isOpen && "rotate-90"
              )}
            />
            {isOpen ? (
              <FolderOpen className="h-4 w-4 shrink-0 text-blue-500" />
            ) : (
              <Folder className="h-4 w-4 shrink-0 text-blue-500" />
            )}
          </>
        ) : (
          <>
            <span className="w-4" />
            {node.icon || <File className="h-4 w-4 shrink-0 text-gray-500" />}
          </>
        )}
        <span className="truncate">{node.name}</span>
      </div>
      
      {isFolder && isOpen && node.children && (
        <div>
          {node.children.map((child, i) => (
            <TreeItem key={i} node={child} level={level + 1} />
          ))}
        </div>
      )}
    </div>
  )
}

export function FileTree({ data, className }: FileTreeProps) {
  return (
    <div className={cn("rounded-lg border bg-background p-2", className)}>
      {data.map((node, i) => (
        <TreeItem key={i} node={node} />
      ))}
    </div>
  )
}
```

**Usage:**
```tsx
<FileTree
  data={[
    {
      name: "src",
      type: "folder",
      children: [
        { name: "components", type: "folder", children: [
          { name: "Button.tsx", type: "file" },
          { name: "Card.tsx", type: "file" },
        ]},
        { name: "app.tsx", type: "file" },
        { name: "index.css", type: "file" },
      ],
    },
    { name: "package.json", type: "file" },
    { name: "README.md", type: "file" },
  ]}
/>
```

---

## 5. HeroVideoDialog

Video modal with thumbnail preview.

```tsx
"use client"
import { useState } from "react"
import { motion, AnimatePresence } from "framer-motion"
import { Play, X } from "lucide-react"
import { cn } from "@/lib/utils"

interface HeroVideoDialogProps {
  videoSrc: string
  thumbnailSrc: string
  thumbnailAlt?: string
  className?: string
}

export function HeroVideoDialog({
  videoSrc,
  thumbnailSrc,
  thumbnailAlt = "Video thumbnail",
  className,
}: HeroVideoDialogProps) {
  const [isOpen, setIsOpen] = useState(false)

  return (
    <>
      {/* Thumbnail with play button */}
      <div
        className={cn(
          "relative cursor-pointer group rounded-xl overflow-hidden",
          className
        )}
        onClick={() => setIsOpen(true)}
      >
        <img
          src={thumbnailSrc}
          alt={thumbnailAlt}
          className="w-full h-full object-cover transition-transform duration-300 group-hover:scale-105"
        />
        <div className="absolute inset-0 bg-black/30 group-hover:bg-black/40 transition-colors" />
        <div className="absolute inset-0 flex items-center justify-center">
          <div className="w-16 h-16 rounded-full bg-white/90 flex items-center justify-center shadow-lg group-hover:scale-110 transition-transform">
            <Play className="w-6 h-6 text-black ml-1" fill="black" />
          </div>
        </div>
      </div>

      {/* Video Modal */}
      <AnimatePresence>
        {isOpen && (
          <motion.div
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            className="fixed inset-0 z-50 flex items-center justify-center bg-black/80 p-4"
            onClick={() => setIsOpen(false)}
          >
            <motion.div
              initial={{ scale: 0.9, opacity: 0 }}
              animate={{ scale: 1, opacity: 1 }}
              exit={{ scale: 0.9, opacity: 0 }}
              className="relative w-full max-w-4xl aspect-video rounded-xl overflow-hidden"
              onClick={(e) => e.stopPropagation()}
            >
              <button
                onClick={() => setIsOpen(false)}
                className="absolute -top-12 right-0 text-white hover:text-gray-300 transition-colors"
              >
                <X className="w-8 h-8" />
              </button>
              <iframe
                src={videoSrc}
                className="w-full h-full"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowFullScreen
              />
            </motion.div>
          </motion.div>
        )}
      </AnimatePresence>
    </>
  )
}
```

**Usage:**
```tsx
<HeroVideoDialog
  videoSrc="https://www.youtube.com/embed/dQw4w9WgXcQ"
  thumbnailSrc="/video-thumbnail.jpg"
/>
```

---

## 6. ScrollProgress

Page scroll progress indicator.

```tsx
"use client"
import { useEffect, useState } from "react"
import { motion, useScroll, useSpring } from "framer-motion"
import { cn } from "@/lib/utils"

interface ScrollProgressProps {
  className?: string
  color?: string
  height?: number
  position?: "top" | "bottom"
}

export function ScrollProgress({
  className,
  color = "hsl(var(--primary))",
  height = 4,
  position = "top",
}: ScrollProgressProps) {
  const { scrollYProgress } = useScroll()
  const scaleX = useSpring(scrollYProgress, {
    stiffness: 100,
    damping: 30,
    restDelta: 0.001,
  })

  return (
    <motion.div
      className={cn(
        "fixed left-0 right-0 z-50 origin-left",
        position === "top" ? "top-0" : "bottom-0",
        className
      )}
      style={{
        scaleX,
        height,
        backgroundColor: color,
      }}
    />
  )
}
```

**Usage:**
```tsx
<ScrollProgress color="#8b5cf6" height={3} />
```

---

## 7. CodeComparison

Side-by-side code diff display.

```tsx
import { cn } from "@/lib/utils"

interface CodeComparisonProps {
  beforeCode: string
  afterCode: string
  beforeTitle?: string
  afterTitle?: string
  language?: string
  className?: string
}

export function CodeComparison({
  beforeCode,
  afterCode,
  beforeTitle = "Before",
  afterTitle = "After",
  language = "tsx",
  className,
}: CodeComparisonProps) {
  return (
    <div className={cn("grid md:grid-cols-2 gap-4", className)}>
      <div className="rounded-lg border bg-zinc-950 overflow-hidden">
        <div className="flex items-center justify-between px-4 py-2 border-b border-zinc-800 bg-zinc-900">
          <span className="text-sm font-medium text-zinc-400">{beforeTitle}</span>
          <span className="text-xs text-zinc-500">{language}</span>
        </div>
        <pre className="p-4 overflow-x-auto text-sm">
          <code className="text-zinc-300">{beforeCode}</code>
        </pre>
      </div>
      
      <div className="rounded-lg border border-green-500/30 bg-zinc-950 overflow-hidden">
        <div className="flex items-center justify-between px-4 py-2 border-b border-green-500/30 bg-green-500/10">
          <span className="text-sm font-medium text-green-400">{afterTitle}</span>
          <span className="text-xs text-green-500/70">{language}</span>
        </div>
        <pre className="p-4 overflow-x-auto text-sm">
          <code className="text-zinc-300">{afterCode}</code>
        </pre>
      </div>
    </div>
  )
}
```

---

## 8. NeonGradientCard

Card with animated neon glow effect.

```tsx
import { cn } from "@/lib/utils"
import { ReactNode, CSSProperties } from "react"

interface NeonGradientCardProps {
  children: ReactNode
  className?: string
  borderSize?: number
  borderRadius?: number
  neonColors?: {
    firstColor: string
    secondColor: string
  }
}

export function NeonGradientCard({
  children,
  className,
  borderSize = 2,
  borderRadius = 20,
  neonColors = {
    firstColor: "#ff00aa",
    secondColor: "#00FFF1",
  },
}: NeonGradientCardProps) {
  return (
    <div
      className={cn(
        "relative z-10 rounded-[--border-radius] p-[--border-size]",
        className
      )}
      style={
        {
          "--border-size": `${borderSize}px`,
          "--border-radius": `${borderRadius}px`,
          "--neon-first-color": neonColors.firstColor,
          "--neon-second-color": neonColors.secondColor,
          "--card-content-radius": `${borderRadius - borderSize}px`,
          "--pseudo-element-width": "200%",
          "--pseudo-element-height": "200%",
          "--after-blur": "30px",
        } as CSSProperties
      }
    >
      {/* Animated gradient border */}
      <div
        className="absolute inset-0 rounded-[--border-radius] -z-10 overflow-hidden"
        style={{
          background: `linear-gradient(90deg, var(--neon-first-color), var(--neon-second-color), var(--neon-first-color))`,
          backgroundSize: "200% 100%",
          animation: "gradient-shift 3s linear infinite",
        }}
      />
      
      {/* Glow effect */}
      <div
        className="absolute inset-0 rounded-[--border-radius] -z-20 blur-xl opacity-50"
        style={{
          background: `linear-gradient(90deg, var(--neon-first-color), var(--neon-second-color))`,
        }}
      />
      
      {/* Content */}
      <div
        className="relative rounded-[--card-content-radius] bg-zinc-950"
        style={{ padding: "1.5rem" }}
      >
        {children}
      </div>
    </div>
  )
}
```

**Required CSS:**
```css
@keyframes gradient-shift {
  0% { background-position: 0% 50%; }
  100% { background-position: 200% 50%; }
}
```

---

## 9. CoolMode

Emoji explosion effect on click.

```tsx
"use client"
import { ReactNode, useRef } from "react"

interface CoolModeProps {
  children: ReactNode
  emoji?: string[]
}

export function CoolMode({ children, emoji = ["🎉", "✨", "💫", "⭐", "🌟"] }: CoolModeProps) {
  const containerRef = useRef<HTMLDivElement>(null)

  const handleClick = (e: React.MouseEvent) => {
    if (!containerRef.current) return
    
    const rect = containerRef.current.getBoundingClientRect()
    const x = e.clientX - rect.left
    const y = e.clientY - rect.top

    for (let i = 0; i < 10; i++) {
      const particle = document.createElement("span")
      particle.textContent = emoji[Math.floor(Math.random() * emoji.length)]
      particle.style.cssText = `
        position: absolute;
        pointer-events: none;
        font-size: ${12 + Math.random() * 12}px;
        left: ${x}px;
        top: ${y}px;
        opacity: 1;
        transition: all 0.6s ease-out;
      `
      containerRef.current.appendChild(particle)

      const angle = Math.random() * Math.PI * 2
      const velocity = 50 + Math.random() * 50
      const endX = x + Math.cos(angle) * velocity
      const endY = y + Math.sin(angle) * velocity - 30

      requestAnimationFrame(() => {
        particle.style.transform = `translate(${endX - x}px, ${endY - y}px) rotate(${Math.random() * 360}deg)`
        particle.style.opacity = "0"
      })

      setTimeout(() => particle.remove(), 600)
    }
  }

  return (
    <div ref={containerRef} className="relative inline-block" onClick={handleClick}>
      {children}
    </div>
  )
}
```

**Usage:**
```tsx
<CoolMode emoji={["🚀", "💥", "✨"]}>
  <button className="px-4 py-2 bg-blue-500 text-white rounded">
    Click me!
  </button>
</CoolMode>
```

---

## Artifact-Ready Versions

### Self-Contained File Tree

```jsx
export default function FileTreeDemo() {
  const [openFolders, setOpenFolders] = React.useState({ src: true, components: false })

  const toggleFolder = (name) => {
    setOpenFolders(prev => ({ ...prev, [name]: !prev[name] }))
  }

  const files = [
    { name: 'src', type: 'folder', children: [
      { name: 'components', type: 'folder', children: [
        { name: 'Button.tsx', type: 'file' },
        { name: 'Card.tsx', type: 'file' },
        { name: 'Input.tsx', type: 'file' },
      ]},
      { name: 'app.tsx', type: 'file' },
      { name: 'index.css', type: 'file' },
    ]},
    { name: 'package.json', type: 'file' },
    { name: 'tsconfig.json', type: 'file' },
    { name: 'README.md', type: 'file' },
  ]

  const renderItem = (item, level = 0) => {
    const isOpen = openFolders[item.name]
    const isFolder = item.type === 'folder'
    
    return (
      <div key={item.name}>
        <div
          className="flex items-center gap-2 py-1 px-2 rounded hover:bg-gray-800 cursor-pointer text-sm"
          style={{ paddingLeft: `${level * 16 + 8}px` }}
          onClick={() => isFolder && toggleFolder(item.name)}
        >
          {isFolder ? (
            <>
              <span className={`transition-transform ${isOpen ? 'rotate-90' : ''}`}>▶</span>
              <span>{isOpen ? '📂' : '📁'}</span>
            </>
          ) : (
            <>
              <span className="w-4" />
              <span>📄</span>
            </>
          )}
          <span className="text-gray-300">{item.name}</span>
        </div>
        {isFolder && isOpen && item.children?.map(child => renderItem(child, level + 1))}
      </div>
    )
  }

  return (
    <div className="min-h-screen bg-gray-950 flex items-center justify-center p-8">
      <div className="w-64 rounded-lg border border-gray-800 bg-gray-900 p-3">
        <div className="text-xs text-gray-500 uppercase mb-2 px-2">Explorer</div>
        {files.map(file => renderItem(file))}
      </div>
    </div>
  )
}
```

### Self-Contained Neon Card

```jsx
export default function NeonCardDemo() {
  return (
    <div className="min-h-screen bg-black flex items-center justify-center p-8">
      <style>{`
        @keyframes gradient-shift {
          0% { background-position: 0% 50%; }
          100% { background-position: 200% 50%; }
        }
      `}</style>
      
      <div className="relative p-[2px] rounded-2xl">
        {/* Animated border */}
        <div
          className="absolute inset-0 rounded-2xl -z-10"
          style={{
            background: 'linear-gradient(90deg, #ff00aa, #00fff1, #ff00aa)',
            backgroundSize: '200% 100%',
            animation: 'gradient-shift 3s linear infinite',
          }}
        />
        
        {/* Glow */}
        <div
          className="absolute inset-0 rounded-2xl -z-20 blur-xl opacity-50"
          style={{ background: 'linear-gradient(90deg, #ff00aa, #00fff1)' }}
        />
        
        {/* Content */}
        <div className="relative bg-zinc-950 rounded-[18px] p-8 w-80">
          <h3 className="text-2xl font-bold text-white mb-2">Neon Card</h3>
          <p className="text-gray-400 mb-4">
            A beautiful card with animated neon gradient border and glow effect.
          </p>
          <button className="w-full py-2 bg-white text-black rounded-lg font-medium hover:bg-gray-100">
            Learn More
          </button>
        </div>
      </div>
    </div>
  )
}
```
