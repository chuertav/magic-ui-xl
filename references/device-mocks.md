# Device Mocks Reference

Browser and mobile device frames for showcasing screenshots and demos.

---

## 1. Safari (Browser Frame)

macOS Safari browser mockup with realistic UI.

```tsx
import { cn } from "@/lib/utils"
import { ReactNode } from "react"

interface SafariProps {
  url?: string
  className?: string
  children?: ReactNode
  src?: string
  width?: number
  height?: number
}

export function Safari({
  url = "magicui.design",
  className,
  children,
  src,
  width = 1203,
  height = 753,
}: SafariProps) {
  return (
    <div className={cn("rounded-xl border bg-background shadow-xl", className)}>
      {/* Browser Chrome */}
      <div className="flex items-center gap-2 border-b bg-muted/50 px-4 py-3">
        {/* Traffic Lights */}
        <div className="flex gap-2">
          <div className="h-3 w-3 rounded-full bg-red-500" />
          <div className="h-3 w-3 rounded-full bg-yellow-500" />
          <div className="h-3 w-3 rounded-full bg-green-500" />
        </div>
        
        {/* URL Bar */}
        <div className="flex-1 flex justify-center">
          <div className="flex items-center gap-2 rounded-md bg-background px-3 py-1.5 text-sm text-muted-foreground border min-w-[300px]">
            <svg className="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
            </svg>
            <span className="truncate">{url}</span>
          </div>
        </div>
        
        {/* Spacer for symmetry */}
        <div className="w-16" />
      </div>
      
      {/* Content Area */}
      <div className="relative overflow-hidden rounded-b-xl bg-white">
        {src ? (
          <img
            src={src}
            alt="Safari browser content"
            width={width}
            height={height}
            className="w-full h-auto"
          />
        ) : (
          children
        )}
      </div>
    </div>
  )
}
```

**Usage:**
```tsx
// With image
<Safari url="myapp.com" src="/dashboard-screenshot.png" />

// With children
<Safari url="myapp.com">
  <div className="p-8 min-h-[400px]">
    <h1>My App Content</h1>
  </div>
</Safari>
```

---

## 2. Safari (Dark Mode Variant)

```tsx
export function SafariDark({
  url = "magicui.design",
  className,
  children,
  src,
}: SafariProps) {
  return (
    <div className={cn("rounded-xl border border-zinc-800 bg-zinc-900 shadow-2xl", className)}>
      {/* Browser Chrome - Dark */}
      <div className="flex items-center gap-2 border-b border-zinc-800 bg-zinc-900 px-4 py-3">
        {/* Traffic Lights */}
        <div className="flex gap-2">
          <div className="h-3 w-3 rounded-full bg-zinc-600" />
          <div className="h-3 w-3 rounded-full bg-zinc-600" />
          <div className="h-3 w-3 rounded-full bg-zinc-600" />
        </div>
        
        {/* URL Bar */}
        <div className="flex-1 flex justify-center">
          <div className="flex items-center gap-2 rounded-md bg-zinc-800 px-3 py-1.5 text-sm text-zinc-400 min-w-[300px]">
            <svg className="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
            </svg>
            <span className="truncate">{url}</span>
          </div>
        </div>
        
        <div className="w-16" />
      </div>
      
      {/* Content */}
      <div className="relative overflow-hidden rounded-b-xl bg-zinc-950">
        {src ? (
          <img src={src} alt="Browser content" className="w-full h-auto" />
        ) : (
          children
        )}
      </div>
    </div>
  )
}
```

---

## 3. iPhone

Realistic iPhone device frame with notch.

```tsx
import { cn } from "@/lib/utils"
import { ReactNode } from "react"

interface IPhoneProps {
  className?: string
  children?: ReactNode
  src?: string
  width?: number
  height?: number
}

export function IPhone({
  className,
  children,
  src,
  width = 433,
  height = 882,
}: IPhoneProps) {
  return (
    <div
      className={cn(
        "relative mx-auto h-[600px] w-[300px] rounded-[50px] border-[12px] border-zinc-900 bg-zinc-900 shadow-xl",
        className
      )}
    >
      {/* Dynamic Island / Notch */}
      <div className="absolute left-1/2 top-0 z-10 h-6 w-28 -translate-x-1/2 translate-y-2 rounded-full bg-zinc-900" />
      
      {/* Side Button (Power) */}
      <div className="absolute -right-[14px] top-[120px] h-12 w-[3px] rounded-r-lg bg-zinc-800" />
      
      {/* Side Buttons (Volume) */}
      <div className="absolute -left-[14px] top-[100px] h-8 w-[3px] rounded-l-lg bg-zinc-800" />
      <div className="absolute -left-[14px] top-[140px] h-8 w-[3px] rounded-l-lg bg-zinc-800" />
      
      {/* Silent Switch */}
      <div className="absolute -left-[14px] top-[60px] h-5 w-[3px] rounded-l-lg bg-zinc-800" />
      
      {/* Screen */}
      <div className="relative h-full w-full overflow-hidden rounded-[38px] bg-white">
        {/* Status Bar */}
        <div className="absolute top-0 z-10 flex h-7 w-full items-center justify-between px-6 text-[10px] font-medium">
          <span>9:41</span>
          <div className="flex items-center gap-1">
            <svg className="h-3 w-3" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z" />
            </svg>
            <svg className="h-3 w-3" viewBox="0 0 24 24" fill="currentColor">
              <path d="M15.5 14h-.79l-.28-.27a6.5 6.5 0 0 0 1.48-5.34c-.47-2.78-2.79-5-5.59-5.34a6.505 6.505 0 0 0-7.27 7.27c.34 2.8 2.56 5.12 5.34 5.59a6.5 6.5 0 0 0 5.34-1.48l.27.28v.79l4.25 4.25c.41.41 1.08.41 1.49 0 .41-.41.41-1.08 0-1.49L15.5 14z" />
            </svg>
            <div className="flex h-3 w-6 items-center rounded-sm border border-current p-[1px]">
              <div className="h-full w-4/5 rounded-sm bg-current" />
            </div>
          </div>
        </div>
        
        {/* Content */}
        {src ? (
          <img
            src={src}
            alt="iPhone screen"
            width={width}
            height={height}
            className="h-full w-full object-cover"
          />
        ) : (
          <div className="h-full w-full pt-8">
            {children}
          </div>
        )}
        
        {/* Home Indicator */}
        <div className="absolute bottom-2 left-1/2 h-1 w-28 -translate-x-1/2 rounded-full bg-zinc-900" />
      </div>
    </div>
  )
}
```

**Usage:**
```tsx
// With screenshot
<IPhone src="/app-screenshot.png" />

// With live content
<IPhone>
  <div className="flex flex-col items-center justify-center h-full bg-gradient-to-b from-purple-500 to-pink-500 text-white">
    <h1 className="text-2xl font-bold">My App</h1>
    <p>Welcome!</p>
  </div>
</IPhone>
```

---

## 4. iPhone (Simple SVG Version)

Lightweight SVG-based iPhone frame.

```tsx
interface IPhoneSVGProps {
  src?: string
  className?: string
  children?: React.ReactNode
}

export function IPhoneSVG({ src, className, children }: IPhoneSVGProps) {
  return (
    <svg
      viewBox="0 0 433 882"
      fill="none"
      className={cn("h-auto w-full max-w-[280px]", className)}
    >
      {/* Device Frame */}
      <path
        d="M2 73C2 32.68 34.68 0 75 0h283c40.32 0 73 32.68 73 73v736c0 40.32-32.68 73-73 73H75c-40.32 0-73-32.68-73-73V73Z"
        fill="#1C1C1E"
      />
      
      {/* Screen Area */}
      <path
        d="M16 74c0-32.033 25.967-58 58-58h285c32.033 0 58 25.967 58 58v734c0 32.033-25.967 58-58 58H74c-32.033 0-58-25.967-58-58V74Z"
        fill="#fff"
      />
      
      {/* Dynamic Island */}
      <rect x="152" y="24" width="129" height="32" rx="16" fill="#1C1C1E" />
      
      {/* Screen Content */}
      <foreignObject x="16" y="16" width="401" height="850" className="overflow-hidden rounded-[42px]">
        <div className="h-full w-full">
          {src ? (
            <img src={src} alt="Screen" className="h-full w-full object-cover" />
          ) : (
            children
          )}
        </div>
      </foreignObject>
      
      {/* Home Indicator */}
      <rect x="142" y="856" width="149" height="5" rx="2.5" fill="#1C1C1E" />
    </svg>
  )
}
```

---

## 5. Android

Android device frame with typical bezels.

```tsx
import { cn } from "@/lib/utils"
import { ReactNode } from "react"

interface AndroidProps {
  className?: string
  children?: ReactNode
  src?: string
}

export function Android({ className, children, src }: AndroidProps) {
  return (
    <div
      className={cn(
        "relative mx-auto h-[620px] w-[300px] rounded-[40px] border-[10px] border-zinc-800 bg-zinc-800 shadow-xl",
        className
      )}
    >
      {/* Front Camera */}
      <div className="absolute left-1/2 top-3 z-10 h-2 w-2 -translate-x-1/2 rounded-full bg-zinc-700" />
      
      {/* Power Button */}
      <div className="absolute -right-[12px] top-[140px] h-16 w-[3px] rounded-r-lg bg-zinc-700" />
      
      {/* Volume Buttons */}
      <div className="absolute -right-[12px] top-[80px] h-10 w-[3px] rounded-r-lg bg-zinc-700" />
      
      {/* Screen */}
      <div className="relative h-full w-full overflow-hidden rounded-[30px] bg-white">
        {/* Status Bar */}
        <div className="absolute top-0 z-10 flex h-6 w-full items-center justify-between bg-black/5 px-4 text-[10px] font-medium text-zinc-800">
          <span>12:00</span>
          <div className="flex items-center gap-2">
            <svg className="h-3 w-3" viewBox="0 0 24 24" fill="currentColor">
              <path d="M1 9l2 2c4.97-4.97 13.03-4.97 18 0l2-2C16.93 2.93 7.08 2.93 1 9zm8 8l3 3 3-3a4.237 4.237 0 00-6 0zm-4-4l2 2a7.074 7.074 0 0110 0l2-2C15.14 9.14 8.87 9.14 5 13z" />
            </svg>
            <svg className="h-3 w-3" viewBox="0 0 24 24" fill="currentColor">
              <path d="M15.67 4H14V2h-4v2H8.33C7.6 4 7 4.6 7 5.33v15.33C7 21.4 7.6 22 8.33 22h7.33c.74 0 1.34-.6 1.34-1.33V5.33C17 4.6 16.4 4 15.67 4z" />
            </svg>
          </div>
        </div>
        
        {/* Content */}
        {src ? (
          <img src={src} alt="Android screen" className="h-full w-full object-cover" />
        ) : (
          <div className="h-full w-full pt-6">
            {children}
          </div>
        )}
        
        {/* Navigation Bar */}
        <div className="absolute bottom-2 left-1/2 flex -translate-x-1/2 items-center gap-8">
          <div className="h-3 w-3 rotate-45 border-2 border-zinc-400" />
          <div className="h-3 w-3 rounded-full border-2 border-zinc-400" />
          <div className="h-3 w-5 rounded border-2 border-zinc-400" />
        </div>
      </div>
    </div>
  )
}
```

---

## 6. Laptop (MacBook Style)

```tsx
interface LaptopProps {
  className?: string
  children?: ReactNode
  src?: string
}

export function Laptop({ className, children, src }: LaptopProps) {
  return (
    <div className={cn("relative mx-auto", className)}>
      {/* Screen */}
      <div className="relative mx-auto w-[700px] rounded-t-xl border-[12px] border-zinc-900 bg-zinc-900">
        {/* Camera */}
        <div className="absolute left-1/2 top-1 h-2 w-2 -translate-x-1/2 rounded-full bg-zinc-700" />
        
        {/* Screen Content */}
        <div className="relative aspect-[16/10] overflow-hidden rounded-lg bg-white">
          {src ? (
            <img src={src} alt="Laptop screen" className="h-full w-full object-cover" />
          ) : (
            children
          )}
        </div>
      </div>
      
      {/* Base/Keyboard */}
      <div className="relative mx-auto">
        {/* Hinge */}
        <div className="h-3 w-[720px] rounded-b-lg bg-gradient-to-b from-zinc-700 to-zinc-800" />
        
        {/* Trackpad area */}
        <div className="mx-auto h-2 w-[750px] rounded-b-2xl bg-zinc-300" />
      </div>
    </div>
  )
}
```

---

## Artifact-Ready Device Mocks

### Self-Contained Safari Frame

```jsx
export default function SafariDemo() {
  return (
    <div className="min-h-screen bg-gray-100 flex items-center justify-center p-8">
      <div className="w-full max-w-4xl rounded-xl border bg-white shadow-2xl overflow-hidden">
        {/* Browser Chrome */}
        <div className="flex items-center gap-2 border-b bg-gray-100 px-4 py-3">
          {/* Traffic Lights */}
          <div className="flex gap-2">
            <div className="h-3 w-3 rounded-full bg-red-500 hover:bg-red-600 cursor-pointer" />
            <div className="h-3 w-3 rounded-full bg-yellow-500 hover:bg-yellow-600 cursor-pointer" />
            <div className="h-3 w-3 rounded-full bg-green-500 hover:bg-green-600 cursor-pointer" />
          </div>
          
          {/* URL Bar */}
          <div className="flex-1 flex justify-center">
            <div className="flex items-center gap-2 rounded-lg bg-white px-4 py-1.5 text-sm text-gray-500 border shadow-inner min-w-[320px]">
              <span className="text-green-600">🔒</span>
              <span>myawesome.app</span>
            </div>
          </div>
          
          <div className="w-16" />
        </div>
        
        {/* Content */}
        <div className="bg-gradient-to-br from-purple-600 to-pink-500 p-12 text-white text-center min-h-[400px] flex flex-col items-center justify-center">
          <h1 className="text-4xl font-bold mb-4">Welcome to My App</h1>
          <p className="text-xl opacity-90 mb-6">The best way to do amazing things</p>
          <button className="px-6 py-3 bg-white text-purple-600 rounded-full font-semibold hover:bg-gray-100 transition">
            Get Started
          </button>
        </div>
      </div>
    </div>
  )
}
```

### Self-Contained iPhone Frame

```jsx
export default function IPhoneDemo() {
  return (
    <div className="min-h-screen bg-gradient-to-br from-gray-900 to-black flex items-center justify-center p-8">
      <div className="relative h-[600px] w-[290px] rounded-[50px] border-[12px] border-zinc-800 bg-zinc-800 shadow-2xl">
        {/* Dynamic Island */}
        <div className="absolute left-1/2 top-0 z-10 h-6 w-24 -translate-x-1/2 translate-y-2 rounded-full bg-black" />
        
        {/* Side Buttons */}
        <div className="absolute -right-[14px] top-[120px] h-12 w-[3px] rounded-r-lg bg-zinc-700" />
        <div className="absolute -left-[14px] top-[100px] h-8 w-[3px] rounded-l-lg bg-zinc-700" />
        <div className="absolute -left-[14px] top-[140px] h-8 w-[3px] rounded-l-lg bg-zinc-700" />
        
        {/* Screen */}
        <div className="relative h-full w-full overflow-hidden rounded-[38px] bg-white">
          {/* Status Bar */}
          <div className="absolute top-0 z-10 flex h-8 w-full items-center justify-between px-6 text-xs font-semibold">
            <span>9:41</span>
            <div className="flex items-center gap-1">
              <span>📶</span>
              <span>🔋</span>
            </div>
          </div>
          
          {/* App Content */}
          <div className="h-full w-full pt-10 bg-gradient-to-b from-blue-500 to-purple-600 flex flex-col items-center justify-center text-white">
            <div className="text-6xl mb-4">📱</div>
            <h2 className="text-2xl font-bold mb-2">My App</h2>
            <p className="text-sm opacity-80">Tap to continue</p>
          </div>
          
          {/* Home Indicator */}
          <div className="absolute bottom-2 left-1/2 h-1 w-24 -translate-x-1/2 rounded-full bg-black" />
        </div>
      </div>
    </div>
  )
}
```

### Self-Contained Device Comparison

```jsx
export default function DeviceShowcase() {
  return (
    <div className="min-h-screen bg-gray-950 py-16 px-8">
      <h1 className="text-4xl font-bold text-white text-center mb-12">
        Works on Every Device
      </h1>
      
      <div className="flex flex-wrap items-end justify-center gap-8">
        {/* iPhone */}
        <div className="relative h-[400px] w-[190px] rounded-[35px] border-[8px] border-zinc-800 bg-zinc-800 shadow-xl">
          <div className="absolute left-1/2 top-1 h-4 w-16 -translate-x-1/2 rounded-full bg-black" />
          <div className="h-full w-full overflow-hidden rounded-[27px] bg-gradient-to-b from-green-400 to-emerald-600 flex items-center justify-center">
            <span className="text-white text-lg font-bold">iOS App</span>
          </div>
          <div className="absolute bottom-1 left-1/2 h-1 w-16 -translate-x-1/2 rounded-full bg-white" />
        </div>
        
        {/* Android */}
        <div className="relative h-[400px] w-[190px] rounded-[30px] border-[6px] border-zinc-700 bg-zinc-700 shadow-xl">
          <div className="absolute left-1/2 top-2 h-2 w-2 -translate-x-1/2 rounded-full bg-zinc-600" />
          <div className="h-full w-full overflow-hidden rounded-[24px] bg-gradient-to-b from-blue-400 to-indigo-600 flex items-center justify-center">
            <span className="text-white text-lg font-bold">Android</span>
          </div>
        </div>
        
        {/* Browser/Desktop */}
        <div className="w-[500px] rounded-xl border-[8px] border-zinc-800 bg-zinc-800 shadow-xl">
          <div className="flex items-center gap-2 bg-zinc-900 px-3 py-2">
            <div className="flex gap-1.5">
              <div className="h-2.5 w-2.5 rounded-full bg-red-500" />
              <div className="h-2.5 w-2.5 rounded-full bg-yellow-500" />
              <div className="h-2.5 w-2.5 rounded-full bg-green-500" />
            </div>
            <div className="flex-1 text-center">
              <span className="text-xs text-zinc-500 bg-zinc-800 px-3 py-1 rounded">myapp.com</span>
            </div>
          </div>
          <div className="h-[250px] bg-gradient-to-b from-purple-400 to-pink-600 flex items-center justify-center">
            <span className="text-white text-xl font-bold">Web App</span>
          </div>
        </div>
      </div>
      
      <p className="text-center text-gray-500 mt-12">
        One codebase, every platform
      </p>
    </div>
  )
}
```
