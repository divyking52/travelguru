# MY TOUR GURU — Kinetic Scroll-Driven Web Architecture

A production-grade, Awwwards-caliber kinetic web experience built for **My Tour Guru Holiday Pvt Ltd**.

---

## Architecture Overview

```
travel guru/
├── index.html          # Monolithic production-ready web application (HTML5, Inline CSS & JS)
├── package.json        # Project metadata, scripts, and dependencies
└── README.md           # Technical documentation and scroll choreography blueprint
```

### Key Technologies & Libraries
- **Scroll Engine:** [Lenis](https://github.com/darkroomengineering/lenis) (v1.1.18) synced directly to GSAP's optimized ticker.
- **Animation Orchestration:** [GSAP 3](https://greensock.com/gsap/) with [ScrollTrigger](https://greensock.com/scrolltrigger/).
- **Typography:** Syne (High-impact editorial display) & Plus Jakarta Sans (Precision UI).
- **Physics & Gestures:** Velocity-reactive skewing, magnetic cursor attraction, multi-plane image parallax.

---

## 5-Act Scroll-Driven Choreography Blueprint

### Act I: The Pin & Scrub Unveil (Hero)
- **Initial Load:** Staggered character reveal on the headline (`yPercent: 120` to `yPercent: 0`) masked with `overflow: hidden`, paired with an ambient background scale-down from `1.15` to `1.0`.
- **On Scroll Scrub (`scrub: 1`):** Pins the hero viewport for `150vh`. As the user scrubs down, typography scales outward to `3.2x` and fades to `opacity: 0`, while a central masked media portal expands from `40vw × 40vh` (`clip-path: inset(30vh 30vw 30vh 30vw round 24px)`) to full viewport `100vw × 100vh` (`clip-path: inset(0 0 0 0 round 0px)`), revealing live coordinates and telemetry.

### Act II: Value Proposition (Sequential Word-by-Word Illumination)
- Pins the editorial philosophy section.
- Splices paragraph text into individual `span.scrub-word` tokens initialized at `opacity: 0.15` with muted slate color (`#3A4454`).
- Links scroll progress directly to staggered illumination (`opacity: 1.0`, `#FFFFFF`) sequentially as the user scrubs through the viewport.

### Act III: Features Showcase (Horizontal Scroll Hijack & Parallax Cards)
- Vertical scroll is converted into a pinned horizontal track (`x: -(track.scrollWidth - window.innerWidth)`).
- **Secondary Multi-Plane Parallax:** Internal card imagery translates horizontally from `xPercent: 12` to `xPercent: -12` relative to the card container, producing realistic optical depth.
- **Dynamic HUD:** Real-time active index indicator (`01 / 04`) with proportional progress bar.
- **Custom Magnetic Cursor:** Morphs into an expanded `"DRAG / SCROLL"` badge when hovering over the track.
- **Mobile Responsive Fallback:** `gsap.matchMedia("(min-width: 769px)")` cleanly degrades on mobile into a vertical stacked layout with zero scroll trapping.

### Act IV: Metrics & Social Proof (Velocity-Reactive Marquee & Number Tickers)
- Dual-direction infinite kinetic typography marquee.
- Reads `ScrollTrigger.getVelocity()` every frame, calculating smooth interpolated velocity that dynamically increases marquee translation speed and applies a physical slant (`skewX`) up to `±12°`.
- Slot-machine style odometer counters triggered at `top 80%` using `power4.out` easing.

### Act V: Sticky Curtain Reveal (Full-Screen Footer)
- The main content body has `position: relative; z-index: 2; margin-bottom: 100vh;` and a heavy drop shadow.
- The footer is fixed behind it at `position: fixed; bottom: 0; z-index: 1; min-height: 100vh;`.
- As the user scrolls to the bottom of the page, the main content lifts up like a curtain, revealing the full-screen interactive footer with magnetic CTAs, live IST clock, and office locations.

---

## Performance & Compositor Guardrails

1. **Strict 60fps Guarantee:**
   - Animates **only** compositor-friendly properties: `transform: translate3d(), scale(), rotate(), skew()` and `opacity` or GPU-accelerated `clip-path`.
   - Never animates layout geometry (`top`, `left`, `width`, `height`, `margin`) inside scroll loops.
2. **Spring Physics & Custom Easing:**
   - Easing functions: `cubic-bezier(0.16, 1, 0.3, 1)` and GSAP `power4.out`, `expo.out`.
3. **Accessibility:**
   - Full `@media (prefers-reduced-motion: reduce)` support: disables scrub pins, displays content immediately.
4. **Memory Management:**
   - Complete cleanup lifecycle via `gsap.context().revert()` and `lenis.destroy()` on window unload.

---

## Quick Start & Verification

### Run Locally

#### Option A: Python HTTP Server (Current Live Host)
```bash
python -m http.server 8080
```
Open **[http://localhost:8080](http://localhost:8080)** in your browser.

#### Option B: Node.js Server
```bash
node server.js
```
Open **[http://localhost:3000](http://localhost:3000)** in your browser.
