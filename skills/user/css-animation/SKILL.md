---
name: css-animation
description: >
  Professional CSS animation framework covering @keyframes, transitions, scroll-driven 
  animations (native CSS), View Transitions API, and animation-timeline. Use this skill 
  when an agent needs to design, spec, or implement animations using pure CSS — including 
  scroll-linked effects without JavaScript, page transitions, keyframe sequences, and 
  performance-aware motion design. Triggers include: CSS animation, @keyframes, 
  animation-timeline, scroll-driven animation, View Transitions API, CSS transitions, 
  hover animations, or any request to animate without JavaScript.
---

# CSS Animation — Professional Framework

## Core Philosophy

CSS animation is the correct default for web motion. Reach for JavaScript (GSAP, Framer Motion) only when CSS can't do the job — sequences that require precise coordination, scroll-scrub tied to a timeline, or gesture-driven interaction. For everything else, CSS is faster, simpler, and more maintainable. The 2024–2026 CSS spec closed most of the gaps that used to require JS. Know where the line is.

---

## Transitions — Two-State Changes

Use transitions for any animation between exactly two states. The browser handles the interpolation.

```css
/* Basic transition */
.button {
  background: #0057ff;
  transform: scale(1);
  transition: background 0.2s ease, transform 0.15s ease;
}
.button:hover {
  background: #0040cc;
  transform: scale(1.03);
}

/* Transition shorthand: property duration easing delay */
transition: all 0.3s ease;           /* ❌ avoid — animates everything, causes perf issues */
transition: transform 0.3s ease;      /* ✅ specific property only */
transition: transform 0.3s ease, opacity 0.3s ease; /* ✅ multiple properties */

/* Timing functions */
ease          /* default — slow start, fast middle, slow end */
ease-out      /* fast start, slow end — most natural for elements entering */
ease-in       /* slow start, fast end — good for elements leaving */
ease-in-out   /* slow start and end — good for state changes */
linear        /* constant speed — use only for looping animations */

/* Custom cubic bezier */
transition-timing-function: cubic-bezier(0.16, 1, 0.3, 1); /* ease-out expo */
transition-timing-function: cubic-bezier(0.34, 1.56, 0.64, 1); /* spring-like overshoot */
```

---

## @keyframes — Multi-State Sequences

Use keyframes when animation has more than two states, loops, or needs to run automatically.

```css
/* Basic keyframe */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(24px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Multiple stops */
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%       { transform: scale(1.08); }
}

/* Shimmer — skeleton loading */
@keyframes shimmer {
  0%   { background-position: -200% center; }
  100% { background-position: 200% center; }
}
.skeleton {
  background: linear-gradient(
    90deg,
    #f0f0f0 25%,
    #e8e8e8 50%,
    #f0f0f0 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s ease-in-out infinite;
}

/* Applying animations */
.element {
  animation-name: fadeInUp;
  animation-duration: 0.6s;
  animation-timing-function: ease-out;
  animation-delay: 0.1s;
  animation-fill-mode: both;     /* holds start state during delay, end state after */
  animation-iteration-count: 1;  /* or: infinite, 3, etc. */
  animation-direction: normal;   /* or: reverse, alternate, alternate-reverse */

  /* Shorthand: name duration easing delay iterations direction fill-mode */
  animation: fadeInUp 0.6s ease-out 0.1s 1 normal both;
}
```

### Stagger with CSS Custom Properties

```css
.card { animation: fadeInUp 0.5s ease-out both; }
.card:nth-child(1) { animation-delay: 0ms; }
.card:nth-child(2) { animation-delay: 80ms; }
.card:nth-child(3) { animation-delay: 160ms; }
.card:nth-child(4) { animation-delay: 240ms; }

/* Dynamic stagger with custom property */
.card { animation-delay: calc(var(--index) * 80ms); }
/* Set --index in HTML: <div class="card" style="--index: 0"> */
```

---

## Scroll-Driven Animations — Native CSS (No JavaScript)

The most significant CSS animation advancement since keyframes. Browser support: Chrome 115+, Edge 115+. Safari and Firefox support is catching up — use `@supports` for progressive enhancement.

### animation-timeline: scroll()

Ties an animation's progress directly to scroll position.

```css
/* Basic scroll-driven fade */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}

.hero-text {
  animation: fadeIn linear;
  animation-timeline: scroll();         /* tracks root scroller */
  animation-range: entry 0% entry 40%; /* fires as element enters viewport */
}

/* scroll() parameters */
animation-timeline: scroll();           /* nearest scrollable ancestor, block axis */
animation-timeline: scroll(root);       /* page scroll */
animation-timeline: scroll(nearest);    /* nearest scrollable ancestor */
animation-timeline: scroll(self);       /* element's own scroll (if it scrolls) */
animation-timeline: scroll(root inline); /* horizontal scroll */
```

### animation-timeline: view()

Ties animation to how far an element has traveled through the viewport.

```css
/* Reveal as element scrolls into view */
@keyframes reveal {
  from { opacity: 0; transform: translateY(40px); }
  to   { opacity: 1; transform: translateY(0); }
}

.section-card {
  animation: reveal linear both;
  animation-timeline: view();
  animation-range: entry 0% entry 60%;
}

/* animation-range values */
animation-range: entry 0% entry 50%;   /* while entering viewport */
animation-range: exit 0% exit 100%;    /* while exiting viewport */
animation-range: contain 0% contain 100%; /* while fully in viewport */
animation-range: cover 0% cover 100%;  /* entire time element intersects viewport */

/* Parallax with scroll-driven */
@keyframes parallax {
  from { transform: translateY(0); }
  to   { transform: translateY(-80px); }
}
.parallax-bg {
  animation: parallax linear;
  animation-timeline: scroll(root);
}
```

### Progressive Enhancement Pattern

```css
/* Base state — works without scroll-driven animation */
.reveal-element {
  opacity: 1;
  transform: none;
}

/* Enhanced version for supporting browsers */
@supports (animation-timeline: scroll()) {
  .reveal-element {
    opacity: 0;
    transform: translateY(30px);
    animation: reveal linear both;
    animation-timeline: view();
    animation-range: entry 0% entry 50%;
  }
}
```

---

## View Transitions API — Page and State Transitions

Native browser transitions between page states or DOM changes. No JavaScript animation library needed for most use cases.

### Same-Document Transitions

```javascript
// Wrap DOM change in startViewTransition
document.startViewTransition(() => {
  // any DOM change — swap content, update class, change route
  updateDOM();
});
```

```css
/* Default cross-fade is automatic — customize with these */
::view-transition-old(root) {
  animation: fadeOut 0.3s ease-out forwards;
}
::view-transition-new(root) {
  animation: fadeIn 0.3s ease-out forwards;
}

/* Named view transitions — shared element morphing */
.card-thumbnail {
  view-transition-name: card-image; /* unique name per element */
}
.card-detail-image {
  view-transition-name: card-image; /* same name = browser morphs between them */
}

/* Style the morphing element during transition */
::view-transition-old(card-image),
::view-transition-new(card-image) {
  animation-duration: 0.4s;
  animation-timing-function: cubic-bezier(0.16, 1, 0.3, 1);
}
```

### Multi-Page View Transitions (MPA)

For sites with full page navigations (not SPAs):

```css
/* In <head> of every page */
@view-transition {
  navigation: auto; /* enables cross-page transitions */
}

/* Customize the transition */
::view-transition-old(root) {
  animation: slideOut 0.3s ease-in forwards;
}
::view-transition-new(root) {
  animation: slideIn 0.3s ease-out forwards;
}

@keyframes slideOut {
  to { transform: translateX(-100%); }
}
@keyframes slideIn {
  from { transform: translateX(100%); }
}
```

---

## animation-timeline: --named (Scroll Timeline)

For precise scroll control with a named timeline:

```css
/* Define a named scroll timeline on a scrollable container */
.scroll-container {
  scroll-timeline-name: --my-timeline;
  scroll-timeline-axis: block;
  overflow-y: scroll;
}

/* Attach animation to that named timeline */
.animated-element {
  animation: grow linear both;
  animation-timeline: --my-timeline;
}
```

---

## Performance — CSS Animation Rules

### Animate Only Composited Properties

```
✅ GPU-composited — fast, no layout recalculation:
  transform: translate, scale, rotate, skew
  opacity
  filter (blur, brightness — with caution)
  clip-path (with caution)

❌ Triggers layout — avoid animating:
  width, height, top, left, margin, padding
  background-color (use opacity on a pseudo-element instead)
  font-size, line-height
```

### will-change — Use Surgically

```css
/* Apply only when animation is imminent */
.card:hover {
  will-change: transform;
}

/* Never set globally */
* { will-change: transform; } /* ❌ destroys performance — forces GPU layers for everything */

/* Remove after animation when possible */
.card {
  transition: transform 0.3s ease;
}
.card:hover {
  will-change: transform;
  transform: scale(1.03);
}
```

### Reduced Motion — Required

```css
/* Always wrap decorative animations */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}

/* Or selectively disable scroll-driven animations */
@media (prefers-reduced-motion: reduce) {
  .reveal-element {
    animation: none;
    opacity: 1;
    transform: none;
  }
}
```

---

## Practical Patterns

### Entrance Animation on Class Toggle (Intersection Observer)

```css
.fade-up {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.5s ease-out, transform 0.5s ease-out;
}
.fade-up.is-visible {
  opacity: 1;
  transform: translateY(0);
}
```

```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) e.target.classList.add("is-visible");
  });
}, { threshold: 0.15 });

document.querySelectorAll(".fade-up").forEach(el => observer.observe(el));
```

### Progress Bar Tied to Page Scroll

```css
.progress-bar {
  position: fixed;
  top: 0;
  left: 0;
  height: 3px;
  background: #0057ff;
  transform-origin: left;
  animation: progress linear;
  animation-timeline: scroll(root);
}

@keyframes progress {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}
```

### Sticky Header Shrink on Scroll

```css
@keyframes shrink {
  from { padding: 1.5rem 2rem; font-size: 1.25rem; }
  to   { padding: 0.75rem 2rem; font-size: 1rem; }
}

.site-header {
  animation: shrink linear both;
  animation-timeline: scroll(root);
  animation-range: 0px 100px; /* fires over first 100px of scroll */
}
```

---

## When CSS Reaches Its Limit — Hand Off to JS

| Scenario | CSS | JS (GSAP / Framer) |
|---|---|---|
| Simple hover / focus states | ✅ | — |
| Entrance animations on scroll | ✅ native scroll-driven | — |
| Looping decorative animation | ✅ | — |
| Page transitions | ✅ View Transitions API | — |
| Progress bar tied to scroll | ✅ | — |
| Scrubbed timeline (animation speed = scroll speed) | ✅ scroll-driven | GSAP for complex sequences |
| Sequences with precise timing dependencies | — | ✅ GSAP timeline |
| Drag and gesture interaction | — | ✅ Framer Motion |
| Scroll + pin (sticky during animation) | — | ✅ GSAP ScrollTrigger |
| Reverse on scroll-back | ✅ scroll-driven (auto) | GSAP scrub |
| Canvas / WebGL animation | — | ✅ Three.js / custom |

---

## Common Traps

1. **Using `transition: all`** — animates every property including ones that trigger layout. Always specify the exact property.

2. **Forgetting `animation-fill-mode: both`** — without it, elements snap to their pre-animation state during a delay, then snap to post-animation state at the end. `both` holds the start state during delay and end state after completion.

3. **Applying `will-change` too broadly** — creates unnecessary GPU layers. Apply only on hover or immediately before animation starts.

4. **Scroll-driven animation without `@supports`** — Chrome 115+ only. Always wrap in `@supports (animation-timeline: scroll())` for production.

5. **Animating `height: auto`** — CSS can't interpolate to or from `auto`. Use `max-height` with a known maximum, or use the `layout` prop in Framer Motion, or JS-measured height animation via GSAP.

6. **View transition names that aren't unique** — two elements with the same `view-transition-name` on screen simultaneously breaks the transition. Names must be unique per frame.
