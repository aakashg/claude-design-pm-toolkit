# Claude Design PM Prompt Toolkit
## Reference: The Design System

The CSS primitives, typography system, animation patterns, and color tokens that power all four prompts in this toolkit. Paste the relevant blocks directly into any Claude Design prompt to maintain visual consistency across sessions.

---

## Liquid Glass CSS

This is the core visual effect used across all four prompts. Two variants: subtle (cards, nav, badges) and strong (CTA buttons, icon circles).

### Subtle — .liquid-glass

```css
.liquid-glass {
  background: rgba(255, 255, 255, 0.01);
  background-blend-mode: luminosity;
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: none;
  box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.1);
  position: relative;
  overflow: hidden;
}
.liquid-glass::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1.4px;
  background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 0.45) 0%,
    rgba(255, 255, 255, 0.15) 20%,
    rgba(255, 255, 255, 0) 40%,
    rgba(255, 255, 255, 0) 60%,
    rgba(255, 255, 255, 0.15) 80%,
    rgba(255, 255, 255, 0.45) 100%
  );
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}
```

**How it works:** The `backdrop-filter: blur(16px)` blurs whatever is behind the element, creating depth against dark video backgrounds. The `::before` pseudo-element uses `mask-composite: exclude` to render only the border area of a gradient — bright white at the top and bottom, fading to invisible in the middle. This creates a glowing edge that looks like light catching the rim of glass. The `padding: 1.4px` controls border thickness.

### Strong — .liquid-glass-strong

```css
.liquid-glass-strong {
  background: rgba(255, 255, 255, 0.01);
  background-blend-mode: luminosity;
  backdrop-filter: blur(50px);
  -webkit-backdrop-filter: blur(50px);
  border: none;
  box-shadow: 4px 4px 4px rgba(0, 0, 0, 0.05),
    inset 0 1px 1px rgba(255, 255, 255, 0.15);
  position: relative;
  overflow: hidden;
}
.liquid-glass-strong::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1.4px;
  background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 0.5) 0%,
    rgba(255, 255, 255, 0.2) 20%,
    rgba(255, 255, 255, 0) 40%,
    rgba(255, 255, 255, 0) 60%,
    rgba(255, 255, 255, 0.2) 80%,
    rgba(255, 255, 255, 0.5) 100%
  );
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}
```

**Difference from subtle:** `blur(50px)` vs `blur(16px)` — the higher blur creates more visual mass, making buttons feel heavier and more tactile. The border gradient is also slightly brighter (0.5 vs 0.45 at the top). Use `.liquid-glass-strong` on anything the user will click.

---

## Typography System

### Dark/Cinematic (Prompts 1 and 4)

```css
@import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Barlow:wght@300;400;500;600&display=swap');

/* Display headings */
.heading-display {
  font-family: 'Instrument Serif', serif;
  font-style: italic;
  line-height: 0.88;
  letter-spacing: -0.03em;
}
/* Hero scale: 80px desktop, 52px mobile */
/* Section scale: 52–64px desktop, 36–44px mobile */
/* Card title scale: 22–28px */

/* Body text */
.body-text {
  font-family: 'Barlow', sans-serif;
  font-weight: 300;
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.55);
}
/* 15–16px body, 13–14px captions, 12px labels */

/* Labels and caps */
.label-caps {
  font-family: 'Barlow', sans-serif;
  font-weight: 600;
  font-size: 11px;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.30);
}
```

### Clean SaaS (Prompt 2)

```css
@import url('https://fonts.googleapis.com/css2?family=Readex+Pro:wght@300;400;500;600;700&display=swap');

body {
  font-family: 'Readex Pro', system-ui, -apple-system, sans-serif;
  -webkit-font-smoothing: antialiased;
}
.hero-title {
  letter-spacing: -0.04em;
  line-height: 0.95;
}
/* 80px hero, 42px section headings, 16px body */
/* font-weight 500 for display, 300 for body, 600 for labels */
```

### Bold/Technical (alternative)

```css
/* Use General Sans from Fontshare for a more geometric feel */
@import url('https://api.fontshare.com/v2/css?f[]=general-sans@400,500,600&display=swap');

/* Or use Readex Pro with all-lowercase styling for a terminal/dark aesthetic */
.all-lower { text-transform: lowercase; }
.hero-stagger {
  font-size: clamp(36px, 13vw, 96px);
  font-weight: 500;
  letter-spacing: -0.04em;
  line-height: 0.95;
  position: absolute; /* for staggered layout */
}
```

### Warm Consumer (for friendly consumer apps — Substack-feel, Arc-feel)

```css
@import url('https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600&family=Inter:wght@400;500;600&display=swap');

body {
  font-family: 'Inter', system-ui, sans-serif;
  color: #1a1410;
  background: #fdfaf4; /* warm off-white */
}
.heading-warm {
  font-family: 'Fraunces', serif;
  font-variation-settings: 'opsz' 80;
  font-weight: 500;
  letter-spacing: -0.02em;
  line-height: 1.05;
}
/* Hero: 64px, Section: 40px, Card title: 20px */
/* Colors in palette: #fdfaf4 (bg), #1a1410 (text), #c2410c (accent orange), #3f6212 (accent olive) */
```

Use when your brand is warm, human, conversational (a newsletter, a reading app, a journaling tool). Feels opposite to dark-cinematic — soft, grounded, a bit nostalgic.

### Retro Terminal (for developer tools, infrastructure, CLI-adjacent products)

```css
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Inter:wght@400;500;600&display=swap');

body {
  font-family: 'Inter', sans-serif;
  background: #0a0a0a;
  color: #e5e5e5;
}
.terminal-heading {
  font-family: 'JetBrains Mono', monospace;
  font-weight: 500;
  letter-spacing: -0.02em;
  text-transform: lowercase;
}
.terminal-cursor::after {
  content: '▌';
  display: inline-block;
  color: #22c55e;
  animation: blink 1s step-end infinite;
}
@keyframes blink { 50% { opacity: 0; } }
/* Colors: #0a0a0a bg, #e5e5e5 text, #22c55e accent green, #f59e0b warn amber */
```

Use for CLI tools, developer-facing products, infrastructure platforms. The lowercase monospace heading + cursor reads as "we ship code."

### Playful Consumer (for social apps, games, anything that should feel fun)

```css
@import url('https://fonts.googleapis.com/css2?family=Funnel+Display:wght@400;500;600;700&family=Inter:wght@400;500;600&display=swap');

body {
  font-family: 'Inter', sans-serif;
  background: linear-gradient(135deg, #fef3c7, #fce7f3);
  color: #1a1a1a;
}
.playful-heading {
  font-family: 'Funnel Display', sans-serif;
  font-weight: 600;
  letter-spacing: -0.03em;
  line-height: 1;
}
/* Use bright non-neutrals liberally: #f97316, #ec4899, #8b5cf6, #22c55e */
/* Border-radius generous: 20px on cards, 9999px on everything pill-shaped */
```

Use for consumer-social, games, creator tools, anything explicitly rejecting the enterprise-minimal aesthetic.

---

## Animation Patterns

### 1. Word-by-word blur reveal (hero headlines)

```css
@keyframes blur-word {
  from {
    filter: blur(10px);
    opacity: 0;
    transform: translateY(50px);
  }
  50% {
    filter: blur(5px);
    opacity: 0.5;
    transform: translateY(-5px);
  }
  to {
    filter: blur(0px);
    opacity: 1;
    transform: translateY(0);
  }
}
```

```javascript
// Split headline into word spans with staggered animation
function animateHeadline(element) {
  const words = element.textContent.split(' ');
  element.innerHTML = words
    .map((word, i) => `<span style="
      display: inline-block;
      animation: blur-word 0.5s ease-out ${i * 100}ms both;
    ">${word}</span>`)
    .join(' ');
}
document.querySelectorAll('.headline-blur').forEach(animateHeadline);
```

**How it works:** Each word starts as a blurred, invisible blob 50px below its final position. It passes through a midpoint that is slightly above the resting position (the -5px overshoot gives it a satisfying snap). The stagger of 100ms per word means a 5-word headline takes 500ms + 500ms duration = about 1 second total. Plays on page load, not on scroll.

### 2. Blur-in (hero subtext and CTAs)

```css
@keyframes blur-in {
  from { filter: blur(8px); opacity: 0; transform: translateY(16px); }
  to   { filter: blur(0px); opacity: 1; transform: translateY(0); }
}
/* Usage:
   Hero subtext: animation: blur-in 0.7s ease-out [headline-end-delay]ms both;
   Hero CTAs:    animation: blur-in 0.6s ease-out [subtext-delay + 200]ms both;
   Calculate delays: headline-end = (word-count × 100) + 300ms */
```

### 3. Fade-rise (all below-fold sections)

```css
@keyframes fade-rise {
  from { opacity: 0; transform: translateY(28px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

```javascript
// IntersectionObserver for scroll-triggered animations
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const children = entry.target.querySelectorAll('.animate-child');
      children.forEach((el, i) => {
        el.style.animation = `fade-rise 0.65s ease-out ${i * 120}ms both`;
      });
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.12 });

document.querySelectorAll('.animate-section').forEach(s => observer.observe(s));
// Add class="animate-section" to each section wrapper
// Add class="animate-child" to each element within sections that should stagger
```

**How it works:** The IntersectionObserver fires when 12% of the section is visible (threshold: 0.12). Each child element gets a 120ms stagger, so a section with 4 children spans 360ms total. The animation is applied once and the section is unobserved so it does not replay on scroll back.

### 4. Hover reveal (product demo card)

```css
.reveal-card {
  position: relative;
  overflow: hidden;
  cursor: pointer;
  border-radius: 20px;
}
.reveal-screenshot {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1),
              opacity 0.4s ease;
  z-index: 2;
}
.reveal-video {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 1;
}
.reveal-card:hover .reveal-screenshot {
  transform: translateY(-105%);
  opacity: 0;
}
```

**How it works:** The screenshot sits on top (z-index 2) and the video plays silently underneath (z-index 1). On hover, the screenshot slides upward out of frame while fading, revealing the live video behind it. The `-105%` prevents a 1px gap at the edge. The `cubic-bezier(0.4, 0, 0.2, 1)` easing is Material Design's "standard" curve — fast out, slow into the end position, feels physical.

### 5. Video loop fade (smooth looping videos)

```javascript
// Prevents jarring hard cut when a looping video restarts
function smoothVideoLoop(videoEl) {
  videoEl.addEventListener('timeupdate', () => {
    const timeRemaining = videoEl.duration - videoEl.currentTime;
    if (timeRemaining < 0.4 && !videoEl.dataset.fading) {
      videoEl.dataset.fading = 'true';
      videoEl.style.transition = 'opacity 0.3s ease';
      videoEl.style.opacity = '0';
      setTimeout(() => {
        videoEl.style.opacity = '1';
        delete videoEl.dataset.fading;
      }, 400);
    }
  });
}
document.querySelectorAll('video[data-smooth-loop]').forEach(smoothVideoLoop);
// Add data-smooth-loop attribute to any video that needs smooth looping
```

---

## Color Tokens

### Dark/Cinematic

```css
:root {
  --bg: #09090b;
  --surface: rgba(255, 255, 255, 0.03);
  --text: #fafafa;            /* contrast vs --bg: 19.8:1 — passes AAA */
  --text-muted: rgba(255, 255, 255, 0.55);  /* ~10.5:1 vs --bg — passes AA, fails AAA on body text below 18px */
  --text-dim: rgba(255, 255, 255, 0.25);    /* ~4.6:1 vs --bg — passes AA on large text only (18px+/14px+ bold), FAILS for body */
  --border: rgba(255, 255, 255, 0.08);
  --border-bright: rgba(255, 255, 255, 0.18);
  --glass-bg: rgba(255, 255, 255, 0.01);
  --glass-border: rgba(255, 255, 255, 0.25);
  --radius-card: 20px;
  --radius-pill: 9999px;
}
```

**WCAG note:** `--text-dim` is for large display elements only — section labels in 11–14px tracked-wide caps, decorative numbers. Do not use it on body text. For body text, use `--text-muted` (passes AA at 14px+) or `--text` (passes AAA everywhere). When the dark background is replaced with a video, contrast can drop further — re-check before shipping. See `12_error_recovery.md` entry on a11y failures.

### Clean SaaS (light)

```css
:root {
  --bg: #ffffff;
  --bg-secondary: #f4f6f8;
  --text-primary: #0D1B2A;
  --text-muted: #64748b;
  --accent: #0D1B2A;
  --accent-light: #e4edf6;
  --border: #e2e8f0;
  --success: #15803d;
  --success-bg: #f0fdf4;
  --success-border: #bbf7d0;
  --radius-card: 16px;
  --radius-pill: 9999px;
}
```
