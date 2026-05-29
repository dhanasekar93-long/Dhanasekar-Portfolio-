# Cinematic Portfolio Hero

A premium, Apple-level cinematic hero section built with Next.js App Router, Three.js, and GSAP.

---

## Quick Setup

### 1. Install dependencies
```bash
npm install
```

### 2. Add your video
Place your talking-head video at:
```
public/video/hero.mp4
```
The file `gemini_generated_video_fa562403.mp4` should be renamed to `hero.mp4`.

### 3. Run development server
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

---

## Project Structure

```
├── app/
│   ├── globals.css          # Global resets, fonts, CSS variables
│   ├── layout.tsx           # Root layout with metadata
│   ├── page.tsx             # Main page — composes hero + next section
│   └── page.module.css      # Page-level styles
│
├── components/
│   ├── VideoIntro/
│   │   ├── VideoIntro.tsx           # Hero section component
│   │   └── VideoIntro.module.css    # Cinematic hero styles
│   │
│   └── CinematicLayer/
│       ├── CinematicLayer.tsx       # Three.js bokeh particle canvas
│       └── CinematicLayer.module.css
│
├── public/
│   └── video/
│       └── hero.mp4         # ← YOUR VIDEO GOES HERE
│
├── next.config.js
├── tsconfig.json
└── package.json
```

---

## Customization

### Change Name & Role
Edit `components/VideoIntro/VideoIntro.tsx`:
```tsx
<span className={styles.firstName} data-first>
  Your         {/* ← Change this */}
</span>
<span className={styles.lastName} data-last>
  Name          {/* ← Change this */}
</span>

<p className={styles.role} data-role>
  Your role description here.  {/* ← Change this */}
</p>
```

### Change Particle Colors
Edit `components/CinematicLayer/CinematicLayer.tsx`:
```tsx
const warmPalette = [
  new THREE.Color(0xe8824a),  // orange — change hex values
  new THREE.Color(0xf0a060),  // warm orange
  // ...
];
```

### Adjust Particle Count
In `CinematicLayer.tsx`, change:
```tsx
const PARTICLE_COUNT = 280; // Increase for denser field, decrease for performance
```

### Tweak GSAP Entrance Timing
In `VideoIntro.tsx`, edit the timeline:
```tsx
tl.to({}, { duration: 0.6 })  // initial pause before reveal
  .to(tagline, { opacity: 1, y: 0, duration: 1.1 }, "+=0.1")
  // ...
```

### Color Theme
Edit `app/globals.css`:
```css
:root {
  --orange: #e8824a;       /* Primary accent */
  --orange-warm: #f0a060;  /* Warm variant */
  --blue-cool: #4a7fa8;    /* Cool blue accent */
  --white: #f5f2ee;        /* Warm white text */
  --black: #080604;        /* Deep warm black */
}
```

---

## Features

| Feature | Implementation |
|---|---|
| Fullscreen video hero | `object-fit: cover` with 100svh |
| Ambient blurred background | Duplicate video with `filter: blur(60px)` |
| Cinematic gradients | Multi-directional CSS gradient overlays |
| Three.js bokeh particles | Additive blending, sprite textures, sine oscillation |
| Mouse parallax | Camera position lerped to mouse position |
| GSAP staggered entrance | Timeline with `power3.out` easing |
| Glassmorphism controls | `backdrop-filter: blur()` + border |
| Sound hint badge | Auto-dismisses after 5 seconds |
| Scroll indicator | Animated pulse line |
| Responsive | `clamp()` typography, mobile layout adjustments |

---

## Performance Notes

- Three.js renderer uses `powerPreference: "high-performance"` and caps pixel ratio at 1.5×
- All Three.js resources (geometry, material, texture, renderer) are properly disposed on unmount
- Mouse parallax uses `lerp` interpolation — no event-driven jitter
- GSAP targets existing DOM elements — no layout thrash
- Videos use `playsInline` + `muted` for iOS autoplay compatibility

---

## Build for Production

```bash
npm run build
npm start
```

---

## Font Attribution

- **Cormorant Garamond** — display / name typography (Google Fonts)
- **Montserrat** — UI labels, taglines, controls (Google Fonts)
