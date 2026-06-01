---
name: web-animation
description: >
  Professional web animation framework for scroll-triggered effects, GSAP implementations,
  Lottie integration, CSS animation systems, and motion specification. Use this skill whenever
  an agent needs to design, spec, or direct web animations — including scroll-triggered reveals,
  timeline sequences, hover states, page transitions, and performance-aware motion design.
  Triggers include: any mention of GSAP, ScrollTrigger, Lottie, animation timelines, motion specs,
  scroll-triggered effects, hover animations, page transitions, or requests to animate any web element.
---

# Web Animation — Professional Framework

## Core Philosophy

Animation on the web has one job: reduce cognitive load, communicate state, and pace information delivery. Motion that doesn't serve one of those three purposes is noise. Every animation decision starts with the question: *what does this teach the user, and does it justify the performance cost?*

---

## GSAP — GreenSock Animation Platform

The industry standard for professional web animation. Use GSAP over CSS animations when:
- Sequences require precise timing control
- Animations need to be scrubbed, reversed, or paused
- ScrollTrigger integration is required
- Performance optimization across browsers matters

### Installation

```bash
# CDN (fastest for prototyping)
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>

# npm
npm install gsap
```

### Core Patterns

```javascript
// Register plugins — always required
gsap.registerPlugin(ScrollTrigger);

// Basic tween
gsap.to(".element", { duration: 0.6, opacity: 1, y: 0, ease: "power2.out" });
gsap.from(".element", { opacity: 0, y: 40 }); // animate FROM these values
gsap.fromTo(".element", { opacity: 0 }, { opacity: 1, duration: 0.8 });

// Timeline — sequences with precise control
const tl = gsap.timeline({ defaults: { ease: "power2.out", duration: 0.5 } });
tl.from(".hero-headline", { opacity: 0, y: 30 })
  .from(".hero-subtext", { opacity: 0, y: 20 }, "-=0.3") // overlap by 0.3s
  .from(".hero-cta", { opacity: 0, scale: 0.95 }, "-=0.2");

// Stagger — animate multiple elements with delay between each
gsap.from(".card", {
  opacity: 0,
  y: 40,
  stagger: 0.1,
  ease: "power2.out",
  duration: 0.6
});
```

### Easing Reference

```javascript
// Standard eases — use these 90% of the time
"power2.out"     // smooth deceleration — most natural for UI elements
"power3.out"     // slightly more aggressive deceleration
"power2.inOut"   // smooth in and out — good for transitions
"back.out(1.7)"  // slight overshoot — adds personality to reveals
"elastic.out(1, 0.3)" // springy — use sparingly, high personality

// Avoid "linear" for anything visible — it reads as mechanical
```

---

## ScrollTrigger — Scroll-Linked Animation

### Fundamental Pattern

```javascript
gsap.from(".section-headline", {
  scrollTrigger: {
    trigger: ".section-headline",
    start: "top 80%",    // when top of element hits 80% down from top of viewport
    end: "top 40%",      // when top of element hits 40% down from top of viewport
    toggleActions: "play none none reverse"
    // play on enter | pause on leave | resume on re-enter | reverse on leave-back
  },
  opacity: 0,
  y: 40,
  duration: 0.7,
  ease: "power2.out"
});
```

### Scrub — Animation Tied Directly to Scroll Position

```javascript
// Scrub: true = tied exactly to scroll speed
// Scrub: 0.5 = animation lags 0.5s behind scroll (smoother)
gsap.to(".parallax-bg", {
  scrollTrigger: {
    trigger: ".section",
    start: "top bottom",
    end: "bottom top",
    scrub: 0.5
  },
  y: -100 // moves up 100px as user scrolls through the section
});
```

### Pin — Stick Element During Scroll

```javascript
// Pin a section in place while content animates inside it
ScrollTrigger.create({
  trigger: ".sticky-section",
  start: "top top",
  end: "+=200%",  // pin for 200vh of scroll distance
  pin: true,
  pinSpacing: true
});

// Combine pin + scrub for horizontal scroll panels
gsap.to(".panels-container", {
  x: () => -(document.querySelector(".panels-container").scrollWidth - window.innerWidth),
  ease: "none",
  scrollTrigger: {
    trigger: ".panels-container",
    pin: true,
    scrub: 1,
    end: () => "+=" + document.querySelector(".panels-container").scrollWidth
  }
});
```

### Batch — Efficient Stagger on Scroll

```javascript
// More performant than individual ScrollTriggers for repeated elements
ScrollTrigger.batch(".card", {
  onEnter: batch => gsap.from(batch, {
    opacity: 0,
    y: 40,
    stagger: 0.1,
    ease: "power2.out"
  }),
  start: "top 85%"
});
```

---

## CSS Animations — When to Use Them

Use CSS animations over GSAP when:
- Simple, looping animations (spinners, pulses, shimmer)
- Hover states and micro-interactions
- Transitions between two states (no sequences)
- Performance is critical and JS overhead matters

```css
/* Fade-in reveal — CSS only */
.reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.5s ease, transform 0.5s ease;
}
.reveal.is-visible {
  opacity: 1;
  transform: translateY(0);
}

/* Pulse — looping */
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}
.badge { animation: pulse 2s ease-in-out infinite; }

/* Shimmer — skeleton loading */
@keyframes shimmer {
  0% { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}
.skeleton {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}

/* Stagger with CSS custom properties */
.card:nth-child(1) { --delay: 0ms; }
.card:nth-child(2) { --delay: 100ms; }
.card:nth-child(3) { --delay: 200ms; }
.card { animation-delay: var(--delay); }
```

---

## Lottie — Vector Animation from After Effects

Use Lottie for complex illustrations, icons, and brand animations that require After Effects-quality motion.

```bash
npm install lottie-web
# or CDN
<script src="https://cdnjs.cloudflare.com/ajax/libs/lottie-web/5.12.2/lottie.min.js"></script>
```

```javascript
// Basic playback
const anim = lottie.loadAnimation({
  container: document.getElementById("lottie-container"),
  renderer: "svg",       // svg | canvas | html
  loop: true,
  autoplay: true,
  path: "/animations/hero-animation.json"
});

// Control playback
anim.pause();
anim.play();
anim.stop();
anim.setSpeed(1.5);     // 1.5x speed
anim.goToAndStop(30, true); // go to frame 30, stop

// Scroll-linked Lottie with GSAP
const anim = lottie.loadAnimation({ /* config */ autoplay: false });
anim.addEventListener("DOMLoaded", () => {
  const totalFrames = anim.totalFrames;
  gsap.to({}, {
    scrollTrigger: { trigger: ".lottie-section", scrub: true, start: "top center", end: "bottom center" },
    onUpdate: function() {
      anim.goToAndStop(this.progress() * totalFrames, true);
    }
  });
});
```

---

## Motion Specification — Writing Animation Specs

When directing developers or documenting motion decisions, use this format:

```
ANIMATION SPEC — [Component Name]

Trigger: [scroll / hover / click / page load / state change]
Element: [CSS selector or component name]
Effect: [what changes — opacity, transform, color, etc.]
Duration: [milliseconds]
Delay: [milliseconds, if applicable]
Easing: [power2.out / ease / spring / etc.]
Direction: [in / out / loop]
Stagger: [milliseconds between each element, if applicable]
Mobile: [same / reduced / disabled]
Performance note: [any GPU compositing, will-change, or reduction flag]

Rationale: [why this animation exists — what it communicates]
```

---

## Performance Standards — Non-Negotiable

### Animate only GPU-composited properties

```
✅ Safe (GPU-composited — no layout recalculation):
  transform: translateX/Y/Z, scale, rotate
  opacity
  filter (with caution)

❌ Expensive (triggers layout/paint — avoid animating):
  width, height, margin, padding, top, left
  background-color (use opacity instead)
  box-shadow (use pseudo-element trick instead)
```

### Will-change — Use Sparingly

```css
/* Only add when animation is imminent — don't set on page load */
.card:hover {
  will-change: transform;
}
/* Remove after animation if possible */
```

### Reduced Motion — Required on Every Project

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

```javascript
// GSAP respects this automatically if configured
gsap.matchMedia().add("(prefers-reduced-motion: no-preference)", () => {
  // all scroll animations here
});
```

---

## Common Traps

1. **Animating too many elements at once** — more than 10 simultaneous GSAP tweens starts to compete for compositor resources. Use stagger and batch instead of animating everything at page load.

2. **Scroll animations that fire on mobile when the user isn't expecting them** — always test on touch devices. Scroll velocity is different; pinned sections can feel broken. Add `invalidateOnRefresh: true` to ScrollTrigger for dynamic layouts.

3. **Missing cleanup in SPAs** — ScrollTrigger instances persist across route changes. Always kill triggers on component unmount: `ScrollTrigger.getAll().forEach(t => t.kill())`.

4. **Using GSAP for simple hover states** — CSS transitions are faster and simpler for single-property hover changes. Reserve GSAP for sequences and scroll-linked animation.

5. **Forgetting `will-change` causes its own performance issues** — setting `will-change: transform` on every card creates composite layers for all of them simultaneously, consuming GPU memory. Apply it only when the animation is about to start.
