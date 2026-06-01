---
name: scrollytelling
description: >
  Narrative scroll architecture for designing and directing scrollytelling experiences — 
  pinned sections, scrubbed animations, horizontal panels, step-based storytelling, and 
  scroll-linked data visualization. Use this skill when an agent needs to design or spec 
  a scrollytelling experience, narrative scroll section, pinned animation, or any experience 
  where scroll position drives a story. Triggers include: scrollytelling, scroll-driven narrative,
  pinned section, horizontal scroll, scroll-linked animation, parallax storytelling, or any 
  request to tell a story through scroll behavior.
---

# Scrollytelling — Narrative Scroll Architecture

## What Scrollytelling Actually Is

Scrollytelling uses scroll position as a narrative controller — the user's scroll becomes the pacing mechanism for a story. It is not the same as "scroll animations." The distinction:

- **Scroll animations**: Elements animate as they enter the viewport (fade-in, slide-up). Decorative.
- **Scrollytelling**: Scroll position drives a narrative sequence — new information is revealed in a controlled order tied to how far the user has scrolled. Structural.

The best scrollytelling experiences feel like the user is in control of a film. The worst feel like a long page that takes forever to load because everything is pinned.

---

## Core Architectural Patterns

### Pattern 1 — Step-Based (Waypoint Scrollytelling)

Content scrolls normally. A sticky visual updates as text steps scroll past it.

**When to use:** Data stories, explainers, product walkthroughs, before/after comparisons.

```
Structure:
[Sticky container — fixed visual panel, left or right]
[Scrolling steps — text blocks that trigger visual changes]
  Step 1: Initial state
  Step 2: Visual updates
  Step 3: Visual updates again
  Step 4: Final state
[Sticky released — normal page resumes]
```

```javascript
// Implementation with Intersection Observer (no GSAP required for steps)
const steps = document.querySelectorAll(".step");
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const stepIndex = entry.target.dataset.step;
      updateVisual(stepIndex); // swap chart, image, map state, etc.
    }
  });
}, { threshold: 0.5 }); // fires when 50% of step is visible

steps.forEach(step => observer.observe(step));

// With GSAP ScrollTrigger for more control
steps.forEach((step, i) => {
  ScrollTrigger.create({
    trigger: step,
    start: "top center",
    onEnter: () => updateVisual(i),
    onEnterBack: () => updateVisual(i)
  });
});
```

```css
.scrollytelling-container {
  display: grid;
  grid-template-columns: 1fr 1fr; /* visual | text */
}

.sticky-visual {
  position: sticky;
  top: 0;
  height: 100vh;
  display: flex;
  align-items: center;
}

.steps-container {
  padding: 50vh 0; /* breathing room at top and bottom */
}

.step {
  min-height: 60vh;
  padding: 2rem;
  opacity: 0.4;
  transition: opacity 0.3s;
}

.step.is-active {
  opacity: 1;
}
```

---

### Pattern 2 — Scrubbed Animation (Timeline Scrollytelling)

The animation timeline is directly tied to scroll position. Scrolling forward advances the animation. Scrolling backward reverses it.

**When to use:** Product reveals, technical explanations, transformation sequences, data build-ups.

```javascript
// GSAP + ScrollTrigger scrub
const tl = gsap.timeline({
  scrollTrigger: {
    trigger: ".scrub-section",
    start: "top top",
    end: "+=300%",      // 3x viewport height of scroll drives the animation
    scrub: 1,           // 1 second lag for smoothness
    pin: true,          // pins the section during scroll
    anticipatePin: 1    // prevents flash before pin engages
  }
});

// Build the timeline — this is what the scroll controls
tl.from(".layer-1", { opacity: 0, duration: 1 })
  .from(".layer-2", { opacity: 0, x: -100, duration: 1 }, "+=0.5")
  .from(".layer-3", { scale: 0.5, opacity: 0, duration: 1 }, "+=0.5")
  .to(".headline", { opacity: 1, y: 0, duration: 0.5 });
```

---

### Pattern 3 — Horizontal Panels

Vertical scroll drives horizontal movement through a sequence of full-screen panels.

**When to use:** Timeline sequences, product feature walkthroughs, portfolio sections.

```javascript
const panels = gsap.utils.toArray(".panel");
const panelsContainer = document.querySelector(".panels-container");

gsap.to(panels, {
  xPercent: -100 * (panels.length - 1),
  ease: "none",
  scrollTrigger: {
    trigger: panelsContainer,
    pin: true,
    scrub: 1,
    snap: 1 / (panels.length - 1),  // snaps to each panel
    end: () => "+=" + panelsContainer.offsetWidth
  }
});
```

```css
.panels-wrapper {
  overflow: hidden;
}

.panels-container {
  display: flex;
  width: 400vw; /* 4 panels × 100vw */
}

.panel {
  width: 100vw;
  height: 100vh;
  flex-shrink: 0;
}
```

---

### Pattern 4 — Parallax Depth Layering

Multiple layers move at different rates, creating a sense of depth.

**When to use:** Hero sections, atmospheric backgrounds, immersive brand moments.

```javascript
// Parallax layers — each moves at a different rate
gsap.utils.toArray(".parallax-layer").forEach(layer => {
  const speed = layer.dataset.speed || 0.5; // 0 = no movement, 1 = matches scroll
  gsap.to(layer, {
    y: () => -ScrollTrigger.maxScroll(window) * speed,
    ease: "none",
    scrollTrigger: {
      trigger: layer,
      start: "top top",
      end: "max",
      scrub: true
    }
  });
});
```

```html
<!-- Speed 0 = stationary, speed 0.5 = moves at half scroll rate -->
<div class="parallax-layer" data-speed="0.1"><!-- background --></div>
<div class="parallax-layer" data-speed="0.3"><!-- midground --></div>
<div class="parallax-layer" data-speed="0.6"><!-- foreground --></div>
```

---

## Narrative Architecture — Story Design Before Code

Before any implementation, answer these questions:

**1. What is the user supposed to understand by the end of this section?**
The scroll experience exists to deliver one insight or transition. Name it in one sentence before designing.

**2. How many beats does this story have?**
Count the distinct states the visual will move through. Each state is a beat. Limit to 4–6 beats per scrollytelling section — more than that and users lose orientation.

**3. What does the user control?**
- Scrub model: user controls animation speed via scroll pace
- Step model: user triggers discrete state changes by reaching waypoints
- Match the model to the content — data that builds gradually = scrub; distinct reveals = steps

**4. What is the exit state?**
When the section unpins, what does the user see? The final frame of the animation must be a complete, meaningful visual — not a mid-animation state.

---

## Scrollytelling Design Principles

### The 3-Second Rule
A user who scrolls through a pinned section without reading anything should still understand what happened. The visual must communicate the story without the text. Text supports; visual carries.

### Breathing Room at Top and Bottom
Pin sections need 50vh of normal scroll before and after pinning to feel natural. Without it, the pin feels like it hijacks the page abruptly.

### Never Pin More Than You Need
Every pinned section is a moment where the user loses control of navigation. Limit to 2–3 pinned sections per page maximum. Use step-based scrollytelling (no pin) when the story doesn't require it.

### Mobile Reduces, Never Eliminates
Complex scrubbed animations often break on mobile. The fallback is not "remove all animation" — it's a simplified step-based version with no pin. The story still exists; the delivery is simpler.

```javascript
gsap.matchMedia().add("(min-width: 768px)", () => {
  // full scrollytelling experience — desktop
});

gsap.matchMedia().add("(max-width: 767px)", () => {
  // simplified step-based — mobile
  // no pins, no scrub — just Intersection Observer steps
});
```

---

## Common Tools

| Tool | Use Case |
|---|---|
| GSAP + ScrollTrigger | Primary implementation for scrub, pin, timeline control |
| Intersection Observer | Step-based triggers, no GSAP dependency |
| Scrollama.js | Step-based scrollytelling helper library |
| D3.js | Data-driven visuals that update on scroll steps |
| Three.js | 3D elements driven by scroll position |
| Lottie | After Effects animations scrubbed by scroll |

---

## Performance — Scrollytelling-Specific

1. **Pin only the container, not individual elements** — pinning multiple nested elements causes layout thrashing.

2. **Use `will-change: transform` on scrubbed layers** — but remove it after the section unpins.

3. **Avoid image swapping on steps** — fading between two absolutely positioned images is more performant than src swapping.

4. **Test scroll performance on mid-range Android** — this is where scrollytelling breaks first. If it stutters there, reduce layer count.

5. **`invalidateOnRefresh: true`** — always set this on ScrollTrigger instances that depend on layout measurements. Viewport resize recalculates everything.

```javascript
ScrollTrigger.create({
  trigger: ".section",
  invalidateOnRefresh: true, // recalculates on resize
  // ...
});
```

---

## Common Traps

1. **Pinning everything** — if the whole page is pinned sections, users feel trapped. Scrollytelling earns its place by being surrounded by normal scroll.

2. **The story only works if you read the text** — the visual must carry the narrative. If removing the text makes the scroll section meaningless, redesign the visual.

3. **Forgetting cleanup in React/Vue** — `ScrollTrigger.getAll().forEach(t => t.kill())` in useEffect cleanup or beforeDestroy.

4. **Scrub animations that are too long** — if the user has to scroll 500vh to see a 5-second animation, the pacing is wrong. Match scroll distance to animation complexity.

5. **No exit strategy** — what does the user do after the pinned section? The transition out of pin back to normal scroll needs as much design thought as the animation itself.
