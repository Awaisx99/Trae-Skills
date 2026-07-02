# Skill: GSAP (GreenSock Animation Platform)

## Purpose
To create performant, professional-grade animations for web projects using GSAP - the industry standard for JavaScript animations. Covers core GSAP, React integration, WordPress/Elementor integration, ScrollTrigger, and best practices.

## When to Use
- Building animated landing pages
- Creating scroll-based animations
- Adding micro-interactions to UI elements
- Animating SVGs, DOM elements, canvas, and three.js
- Integrating animations into WordPress/Elementor sites
- Building React applications with smooth animations

## Procedure

### 1. Core GSAP Basics
GSAP's core API includes `to()`, `from()`, and `fromTo()` methods.

```javascript
// Import GSAP
import gsap from "gsap";

// Animate element to a state
gsap.to(".element", {
  x: 200, // Move 200px right
  rotation: 360, // Rotate 360deg
  duration: 1, // 1 second duration
  ease: "power2.out" // Easing function
});

// Animate element from a state
gsap.from(".element", {
  opacity: 0,
  y: 50,
  duration: 0.5
});

// Animate between two states
gsap.fromTo(".element", 
  { x: -100, opacity: 0 }, // From
  { x: 0, opacity: 1, duration: 1 } // To
);
```

**Key Concepts**:
- Easing: Use built-in eases like `"power1.out"`, `"bounce.inOut"`, `"elastic.out"`, or create custom curves
- Staggering: Animate multiple elements with delay using `stagger: 0.1`
- Timelines: Chain animations together for complex sequences

```javascript
// Staggered animation
gsap.from(".box", {
  opacity: 0,
  y: 20,
  stagger: 0.1, // 0.1s delay between each element
  duration: 0.5
});

// Timeline for complex sequences
const tl = gsap.timeline();
tl.to(".box1", { x: 100 })
  .to(".box2", { y: 100 }, "-=0.5") // Overlap with previous animation
  .to(".box3", { rotation: 360 });
```

---

### 2. React Integration (@gsap/react)
Use the official `useGSAP()` hook for React - it automatically handles cleanup!

**Installation**:
```bash
npm install gsap @gsap/react
```

**Basic Usage**:
```jsx
import { useRef } from "react";
import gsap from "gsap";
import { useGSAP } from "@gsap/react";

gsap.registerPlugin(useGSAP);

function AnimatedComponent() {
  const container = useRef();
  
  useGSAP(() => {
    // GSAP code here - automatically cleaned up!
    gsap.to(".box", {
      x: 100,
      rotation: 360,
      duration: 1
    });
  }, { scope: container }); // Scope selectors to container

  return (
    <div ref={container}>
      <div className="box">Hello</div>
    </div>
  );
}
```

**Targeting Elements**:
- Use Refs for individual elements
- Use Scoped Selectors for groups of elements (best practice!)

```jsx
// Using Refs for individual elements
const boxRef = useRef();

useGSAP(() => {
  gsap.to(boxRef.current, { rotation: 360 });
});

// Using Scoped Selectors (better for many elements!)
const container = useRef();

useGSAP(() => {
  gsap.from(".box", {
    opacity: 0,
    stagger: 0.1
  });
}, { scope: container });

return (
  <div ref={container}>
    <div className="box">1</div>
    <div className="box">2</div>
    <div className="box">3</div>
  </div>
);
```

**Timelines in React**:
Store timelines in refs for later control (play, pause, reverse, etc.)

```jsx
function AnimatedSection() {
  const container = useRef();
  const tl = useRef();

  useGSAP(() => {
    tl.current = gsap.timeline()
      .to(".box", { x: 200 })
      .to(".circle", { y: 100 });
  }, { scope: container });

  return (
    <div ref={container}>
      <button onClick={() => tl.current.play()}>Play</button>
      <button onClick={() => tl.current.reverse()}>Reverse</button>
      <div className="box">Box</div>
      <div className="circle">Circle</div>
    </div>
  );
}
```

**Reacting to State Changes**:
Use dependencies array to trigger animations when state changes

```jsx
function Box({ isActive }) {
  const boxRef = useRef();

  useGSAP(() => {
    gsap.to(boxRef.current, {
      x: isActive ? 100 : 0,
      duration: 0.5
    });
  }, [isActive]);

  return <div ref={boxRef} className="box">Box</div>;
}
```

---

### 3. WordPress/Elementor Integration
Enqueue GSAP properly in WordPress and use with Elementor!

**Step 1: Enqueue GSAP in functions.php (Child Theme!)**
```php
<?php
// Enqueue GSAP and ScrollTrigger in your child theme's functions.php
function theme_enqueue_gsap() {
    // Core GSAP
    wp_enqueue_script(
        'gsap',
        'https://cdn.jsdelivr.net/npm/gsap@3.12/dist/gsap.min.js',
        array(),
        '3.12',
        true // Load in footer
    );

    // ScrollTrigger (if needed)
    wp_enqueue_script(
        'gsap-scrolltrigger',
        'https://cdn.jsdelivr.net/npm/gsap@3.12/dist/ScrollTrigger.min.js',
        array('gsap'), // Depends on GSAP core
        '3.12',
        true
    );

    // Your custom animation file
    wp_enqueue_script(
        'custom-animations',
        get_stylesheet_directory_uri() . '/js/animations.js',
        array('gsap', 'gsap-scrolltrigger'),
        '1.0',
        true
    );
}
add_action('wp_enqueue_scripts', 'theme_enqueue_gsap');
?>
```

**Step 2: Create animations.js in your child theme's js/ folder**
```javascript
// Wait for DOM and assets to load
document.addEventListener("DOMContentLoaded", function() {
  window.addEventListener("load", function() {
    
    // Basic animation for Elementor elements
    gsap.from(".elementor-section .elementor-widget", {
      opacity: 0,
      y: 50,
      duration: 0.8,
      stagger: 0.2,
      ease: "power2.out"
    });

    // ScrollTrigger animation (see below for more details)
    gsap.registerPlugin(ScrollTrigger);
    
    gsap.from(".hero-title", {
      opacity: 0,
      y: 100,
      duration: 1,
      scrollTrigger: {
        trigger: ".hero-section",
        start: "top 80%",
        toggleActions: "play none none none"
      }
    });
  });
});
```

**Elementor-Specific Tips**:
- Use Elementor's CSS classes (`.elementor-section`, `.elementor-widget`, etc.)
- Add custom classes to Elementor elements for targeting (Advanced → CSS Classes)
- For Elementor Pro Popups: Animate popups with GSAP using popup triggers
- For Elementor Forms: Add micro-interactions to form fields/buttons

---

### 4. ScrollTrigger Plugin (Must-Have!)
Create scroll-based animations with ScrollTrigger - GSAP's most powerful plugin!

```javascript
// Register ScrollTrigger
gsap.registerPlugin(ScrollTrigger);

// Basic scroll-triggered animation
gsap.from(".element", {
  opacity: 0,
  x: -100,
  duration: 1,
  scrollTrigger: {
    trigger: ".element", // Element that triggers animation
    start: "top 80%", // When top of element hits 80% of viewport
    end: "bottom 20%", // When bottom hits 20%
    toggleActions: "play none none none", // OnEnter, OnLeave, OnEnterBack, OnLeaveBack
    markers: true // Show debug markers - remove in production!
  }
});

// Pin an element while scrolling
ScrollTrigger.create({
  trigger: ".pinned-element",
  start: "top top",
  end: "+=500", // Pin for 500px of scrolling
  pin: true,
  markers: true
});

// Scroll scrubbing (animation follows scroll position)
gsap.to(".scrub-element", {
  x: 500,
  rotation: 360,
  scrollTrigger: {
    trigger: ".scrub-section",
    start: "top top",
    end: "bottom bottom",
    scrub: 1 // Smooth scrubbing with 1s lag
  }
});
```

---

### 5. Advanced Techniques

**FLIP Plugin (Prevent Layout Shifts)**:
Animate elements smoothly when they move or resize

```javascript
import { Flip } from "gsap/Flip";
gsap.registerPlugin(Flip);

function flipAnimation() {
  const state = Flip.getState(".box"); // Get current state
  // Make DOM changes (move element, change size, etc.)
  Flip.from(state, { duration: 0.5, ease: "power1.inOut" });
}
```

**Reusable Effects**:
Create reusable animations with `registerEffect()`

```javascript
gsap.registerEffect({
  name: "fadeInUp",
  effect: (targets, config) => {
    return gsap.from(targets, {
      opacity: 0,
      y: config.y || 50,
      duration: config.duration || 0.5,
      stagger: config.stagger || 0
    });
  },
  defaults: { y: 50, duration: 0.5 }
});

// Use the effect!
gsap.effects.fadeInUp(".elements", { stagger: 0.1 });
```

**Performance Optimizations**:
- Use `quickTo()` or `quickSetter()` for frequent updates (mousemove, scroll)
- Animate `transform` and `opacity` only (best performance!)
- Avoid animating `top`/`left`/`width`/`height` (triggers layout reflows)
- Use `will-change: transform, opacity` for elements being animated

```javascript
// Quick setter for mousemove
const quickX = gsap.quickSetter(".box", "x", "px");

window.addEventListener("mousemove", (e) => {
  quickX(e.clientX);
});
```

---

## Constraints & Best Practices
1. **Always clean up animations**: In React, use `useGSAP()` which does this automatically!
2. **Avoid layout thrashing**: Animate `transform` and `opacity` only
3. **Respect reduced motion**: Use `gsap.matchMedia()` to disable animations for users who prefer it
4. **Test on mobile**: Animations should be smooth on all devices
5. **Use CDNs for WordPress**: Load GSAP from CDN (jsDelivr, Cloudflare) for best performance
6. **Scope selectors**: Prevent conflicts by scoping selectors in React and WordPress

---

## Expected Outcome
Professional, smooth, performant animations that enhance user experience without hurting performance!

---

## Extras: Elementor Scroll-Reveal Image Effect (Sundae Creative Style)
Recreate the perfect "image-on-text" scroll effect from https://sundaecreative.com/! The image starts centered on the text, scales to full viewport width, and moves down below the text as you scroll!

### Step 1: HTML Structure
```html
<!-- Use this structure in Elementor or custom theme -->
<div class="scroll-container" style="position: relative; height: 200vh;">
  <section class="hero-section" style="position: relative; height: 100vh; display: flex; align-items: center; justify-content: center; background: #1a1a1a; overflow: hidden;">
    <div class="hero-nav-top" style="position: absolute; top: 2rem; left: 0; right: 0; display: flex; justify-content: space-between; padding: 0 4rem; color: rgba(255,255,255,0.7); font-size: 0.875rem; text-transform: uppercase; letter-spacing: 0.15em; font-weight: 500;">
      <span>Menu</span>
      <span>sundaecreative</span>
      <span>Let's Talk</span>
    </div>
    <h1 class="hero-heading" style="color: white; font-size: clamp(3rem, 12vw, 12rem); font-weight: 900; text-align: center; line-height: 0.9; z-index: 1; position: relative;">
      A GLOBAL<br>
      COMMUNICATIONS<br>
      & PR AGENCY FOR<br>
      LIFESTYLE BRANDS
    </h1>
    <div class="hero-nav-bottom" style="position: absolute; bottom: 2rem; left: 0; right: 0; display: flex; justify-content: space-between; padding: 0 4rem; color: rgba(255,255,255,0.6); font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.08em; font-weight: 500;">
      <span>WE STRATEGICALLY<br>COMMUNICATE</span>
      <span>WITH AUDIENCES</span>
    </div>
    <div class="hero-image-wrap" style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); z-index: 2; width: 30%; min-width: 300px;">
      <img class="hero-image" src="https://images.unsplash.com/photo-1573496799652-408c2ac9fe98?w=800&h=600&fit=crop" alt="Hero" style="width: 100%; display: block; border-radius: 12px; box-shadow: 0 30px 60px -15px rgba(0,0,0,0.5);">
    </div>
  </section>
</div>
```

### Step 2: JavaScript (GSAP + ScrollTrigger)
Add to your theme's `animations.js` file or Elementor HTML widget:
```javascript
document.addEventListener('DOMContentLoaded', function() {
  gsap.registerPlugin(ScrollTrigger);
  
  const imageWrap = document.querySelector('.hero-image-wrap');
  
  gsap.to(imageWrap, {
    width: '100vw',
    y: () => window.innerHeight / 2 + (window.innerHeight * 0.45),
    borderRadius: '0px',
    ease: 'none',
    scrollTrigger: {
      trigger: '.scroll-container',
      start: 'top top',
      end: 'bottom top',
      scrub: 1
    }
  });
});
```

### Step 3: Elementor Usage Instructions
1. In Elementor, create this structure with sections/widgets:
2. Use **Outer Section** → Add custom class `scroll-container` → Set height to 200vh
3. **Inner Section** (inside outer) → Add custom class `hero-section` → Set height to 100vh → Dark background
4. Add **Heading Widgets** for nav top/heading/nav bottom as in HTML above
5. Add **HTML Widget** for image container with custom class `hero-image-wrap`
6. Go to **Elementor → Custom Code** or your child theme's functions.php to enqueue GSAP (see WordPress Integration section)
7. Paste the JavaScript in `animations.js` file or in an Elementor HTML widget (wrap in `<script>` tags)

### Customization Options
- Change `height: 200vh` on `.scroll-container` to adjust scroll distance
- Adjust the image starting width (`width: 30%;` for larger/smaller
- Tweak `y: () => window.innerHeight / 2 + (window.innerHeight * 0.45)` to change how far down the image travels
- Modify `scrub: 1` to change smoothness (higher = smoother)

---

## Continuous Learning & Skill Improvement
**Crucial Note**: For every design, animation, or workflow task:
1. Document lessons learned after completion
2. Update relevant skills with new knowledge as an "Extras" or "Crucial Learnings" section
3. Apply improved approaches to all future similar tasks
