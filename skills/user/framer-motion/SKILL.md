---
name: framer-motion
description: >
  Framer Motion animation framework for React — component-level animation, layout animations,
  gesture-driven interactions, shared element transitions, and scroll-linked effects.
  Use this skill when an agent needs to design, spec, or implement animations in a React 
  environment using Framer Motion. Triggers include: Framer Motion, motion components, 
  AnimatePresence, layout animations, drag interactions, useScroll, useTransform, 
  React animation, or any request to animate React components.
---

# Framer Motion — React Animation Framework

## Core Philosophy

Framer Motion treats animation as a first-class part of the React component model. Animations live in the component tree, respond to state, and clean themselves up automatically. The mental model is declarative: describe what a component looks like in different states, and Framer Motion handles the transition.

---

## Installation

```bash
npm install framer-motion
```

---

## Fundamental Concepts

### The `motion` Component

Any HTML element can become animatable by prefixing it with `motion.`:

```jsx
import { motion } from "framer-motion";

// Basic fade-in
<motion.div
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 0.5, ease: "easeOut" }}
>
  Content
</motion.div>

// Exit animation — requires AnimatePresence wrapper
<motion.div
  exit={{ opacity: 0, y: -20 }}
>
  Content
</motion.div>
```

### Variants — Defining Animation States

Variants make complex, coordinated animations manageable:

```jsx
const containerVariants = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: {
      staggerChildren: 0.1,    // 100ms between each child
      delayChildren: 0.2       // wait 200ms before starting children
    }
  }
};

const itemVariants = {
  hidden: { opacity: 0, y: 20 },
  visible: { opacity: 1, y: 0 }
};

// Parent propagates state to all children automatically
<motion.ul variants={containerVariants} initial="hidden" animate="visible">
  {items.map(item => (
    <motion.li key={item.id} variants={itemVariants}>
      {item.text}
    </motion.li>
  ))}
</motion.ul>
```

---

## AnimatePresence — Mount / Unmount Animations

Required for exit animations. Wraps any component that conditionally renders:

```jsx
import { AnimatePresence, motion } from "framer-motion";

// Modal with enter/exit
<AnimatePresence>
  {isOpen && (
    <motion.div
      key="modal"
      initial={{ opacity: 0, scale: 0.95 }}
      animate={{ opacity: 1, scale: 1 }}
      exit={{ opacity: 0, scale: 0.95 }}
      transition={{ duration: 0.2 }}
    >
      Modal content
    </motion.div>
  )}
</AnimatePresence>

// List items — key prop is critical for AnimatePresence to track removals
<AnimatePresence>
  {items.map(item => (
    <motion.div
      key={item.id}
      initial={{ opacity: 0, height: 0 }}
      animate={{ opacity: 1, height: "auto" }}
      exit={{ opacity: 0, height: 0 }}
      transition={{ duration: 0.3 }}
    >
      {item.content}
    </motion.div>
  ))}
</AnimatePresence>
```

---

## Layout Animations

Framer Motion can animate layout changes automatically — no manual position calculation needed:

```jsx
// Add layout prop — Framer Motion detects and animates position/size changes
<motion.div layout>
  Content that changes size or position
</motion.div>

// Animate only specific layout properties
<motion.div layout="position">  // only animates position changes
<motion.div layout="size">      // only animates size changes

// layoutId — shared element transitions between components
// The element "morphs" between its two positions
<motion.div layoutId="hero-image">
  <img src={thumbnail} />
</motion.div>

// In a different component / route
<motion.div layoutId="hero-image">
  <img src={fullsize} />
</motion.div>
```

---

## Gesture Animations

```jsx
// Hover and tap — declarative
<motion.button
  whileHover={{ scale: 1.05, backgroundColor: "#0057ff" }}
  whileTap={{ scale: 0.97 }}
  transition={{ type: "spring", stiffness: 400, damping: 17 }}
>
  Click me
</motion.button>

// Drag
<motion.div
  drag                            // drag in both axes
  drag="x"                       // drag x axis only
  dragConstraints={{ left: -100, right: 100 }}  // limit drag range
  dragElastic={0.2}              // how much it stretches past constraint
  onDragEnd={(event, info) => {
    if (info.offset.x > 100) dismissCard();
  }}
>
  Draggable card
</motion.div>
```

---

## Scroll-Linked Animation

### useScroll + useTransform

```jsx
import { useScroll, useTransform, motion } from "framer-motion";

function ParallaxHero() {
  const { scrollY } = useScroll();

  // Map scroll position to a value range
  const opacity = useTransform(scrollY, [0, 300], [1, 0]);
  const y = useTransform(scrollY, [0, 300], [0, -100]);

  return (
    <motion.div style={{ opacity, y }}>
      Hero content
    </motion.div>
  );
}

// Element-specific scroll tracking
function ScrollReveal({ children }) {
  const ref = useRef(null);
  const { scrollYProgress } = useScroll({
    target: ref,
    offset: ["start end", "end start"]  // [when element enters, when it leaves]
  });

  const opacity = useTransform(scrollYProgress, [0, 0.3], [0, 1]);
  const y = useTransform(scrollYProgress, [0, 0.3], [40, 0]);

  return (
    <motion.div ref={ref} style={{ opacity, y }}>
      {children}
    </motion.div>
  );
}
```

### useInView — Trigger on Viewport Entry

```jsx
import { useInView } from "framer-motion";

function AnimateOnScroll({ children }) {
  const ref = useRef(null);
  const isInView = useInView(ref, { once: true, margin: "0px 0px -100px 0px" });

  return (
    <motion.div
      ref={ref}
      initial={{ opacity: 0, y: 30 }}
      animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 30 }}
      transition={{ duration: 0.6, ease: "easeOut" }}
    >
      {children}
    </motion.div>
  );
}
```

---

## Transition Configuration

```jsx
// Spring — most natural for UI interactions
transition={{ type: "spring", stiffness: 300, damping: 25 }}
// stiffness: higher = snappier. damping: higher = less bouncy.
// Good defaults: stiffness: 300-500, damping: 20-30

// Tween — precise duration control
transition={{ type: "tween", duration: 0.4, ease: "easeOut" }}

// Ease presets
ease: "linear" | "easeIn" | "easeOut" | "easeInOut" | "circIn" | "circOut" | "backOut"

// Custom cubic bezier
ease: [0.16, 1, 0.3, 1]  // custom ease-out expo

// Orchestration
transition={{
  duration: 0.5,
  delay: 0.2,
  staggerChildren: 0.1,  // in variants
  delayChildren: 0.3     // in variants
}}
```

---

## Page Transitions — React Router

```jsx
import { AnimatePresence, motion } from "framer-motion";
import { useLocation, Routes, Route } from "react-router-dom";

const pageVariants = {
  initial: { opacity: 0, x: -20 },
  animate: { opacity: 1, x: 0 },
  exit: { opacity: 0, x: 20 }
};

function App() {
  const location = useLocation();

  return (
    <AnimatePresence mode="wait">  // "wait" = exit completes before enter starts
      <Routes location={location} key={location.pathname}>
        <Route path="/" element={
          <motion.div variants={pageVariants} initial="initial" animate="animate" exit="exit">
            <HomePage />
          </motion.div>
        } />
      </Routes>
    </AnimatePresence>
  );
}
```

---

## useAnimate — Imperative Animation

For animations that need to fire in response to events, not state:

```jsx
import { useAnimate } from "framer-motion";

function SubmitButton() {
  const [scope, animate] = useAnimate();

  const handleSubmit = async () => {
    await animate(scope.current, { scale: 0.95 }, { duration: 0.1 });
    await animate(scope.current, { scale: 1 }, { duration: 0.2, ease: "backOut" });
    // then do the actual submit
  };

  return (
    <motion.button ref={scope} onClick={handleSubmit}>
      Submit
    </motion.button>
  );
}
```

---

## Performance

```jsx
// Use style for scroll-linked values — keeps them off the React render cycle
const y = useTransform(scrollY, [0, 300], [0, -100]);
<motion.div style={{ y }} />  // ✅ no re-render on scroll

// Avoid animating layout-triggering properties
// ❌ Avoid: width, height, margin, padding
// ✅ Use: scaleX, scaleY, x, y, opacity

// LazyMotion — reduces bundle size by 80% for production
import { LazyMotion, domAnimation, m } from "framer-motion";

<LazyMotion features={domAnimation}>
  <m.div animate={{ opacity: 1 }} />  // use m.div instead of motion.div
</LazyMotion>

// Reduced motion
import { useReducedMotion } from "framer-motion";

function AnimatedComponent() {
  const shouldReduceMotion = useReducedMotion();
  return (
    <motion.div
      animate={{ opacity: 1, y: shouldReduceMotion ? 0 : -20 }}
    />
  );
}
```

---

## Common Traps

1. **Missing `key` prop with AnimatePresence** — without a stable key, exit animations don't fire. Always give conditionally rendered components a unique key.

2. **`layout` on too many elements** — layout animations require Framer Motion to measure every affected element. Limit to the specific elements that need it.

3. **Animating `height: auto`** — use `layout` prop instead of animating height directly. Framer Motion handles the measurement; direct height animation breaks with dynamic content.

4. **`useScroll` without a target ref on complex pages** — without specifying `target`, `scrollY` tracks the page. If you want element-relative tracking, pass the ref.

5. **Blocking the render cycle with scroll handlers** — `useTransform` is designed to run off the main thread via MotionValue. Don't convert values back to state with `useState` — that defeats the purpose and causes re-renders on every scroll tick.
