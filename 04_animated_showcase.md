# Claude Design PM Prompt Toolkit
## Prompt 4: The Animated Product Showcase

**Use case:** Product Hunt launches, conference demos, investor pitches, and any moment where you need to stop someone mid-scroll. Cinematic video background, liquid glass effects, word-by-word blur animations, hover reveal effects.

**What this used to require:** A frontend engineer, a motion designer, and about a week.

**What it requires now:** A Claude seat, a Mux-hosted video URL, and roughly 45 minutes.

**Before you use this prompt — the video workflow:**

1. **Generate your background video** using Kling 3.0 or Sedance 2.0. Use this universal animation prompt: `looping animation no camera movement no extra elements to be added no zoom in or zoom out looping animation`. Keep it under 8 seconds. If you want a transition effect, generate two versions of your image (e.g. plain surface + textured surface) and feed both into Kling as a start/end frame.

2. **Fix jarring loops** — if the video has a hard cut when it restarts, add a CSS fade system after generating: `add a JavaScript fade system that fades the video to opacity 0 over 0.3s at the end of each loop, holds for 0.1s, then fades back to opacity 1 over 0.3s as it restarts. Use a timeupdate event listener.`

3. **Host on Mux or Cloudflare** — Claude Design needs a live URL it can load in a browser. Upload your video to Mux.com (free tier works) or Cloudflare Stream. Mux gives you a streaming URL like `https://stream.mux.com/[ID].m3u8`. Cloudflare gives you a direct MP4 URL. Either works.

4. **Paste the URL** where you see `[YOUR HERO VIDEO URL]` in the prompt below.

---

## The Prompt

```
Build a cinematic single-page product showcase for [PRODUCT NAME]. This is for [CONTEXT — e.g. "a Product Hunt launch" / "a conference demo" / "a board presentation"].

BACKGROUND VIDEO:
Hero section uses this looping video as its background: [YOUR HERO VIDEO URL]

Video implementation:
<video autoPlay loop muted playsInline style="position:absolute;inset:0;width:100%;height:100%;object-fit:cover;z-index:0">
  <source src="[YOUR HERO VIDEO URL]" type="video/mp4" />
</video>

Add gradient fades over the video:
- Top fade: absolute, top 0, height 200px, background: linear-gradient(to bottom, rgba(0,0,0,0.7), transparent), pointer-events-none, z-index 1
- Bottom fade: absolute, bottom 0, height 300px, background: linear-gradient(to top, rgba(0,0,0,1), transparent), pointer-events-none, z-index 1
- Dark overlay: absolute inset-0 bg-black/25 z-index 1 (reduces video brightness for text legibility)

AESTHETIC: Luxury editorial. Black background (#09090b), white text, cinematic. Think A24 film titles merged with a SaaS product. Every section should feel intentional.

FONTS:
Import from Google Fonts:
https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Barlow:wght@300;400;500;600&display=swap

- All headings: Instrument Serif italic — sizes 48–96px, line-height 0.85–0.95, letter-spacing -0.03em
- All body text: Barlow 300 — 14–16px, line-height 1.65–1.75, color white/60
- Nav links: Barlow 500 — 13px, white/80
- Labels/caps: Barlow 600 — 11px, uppercase, letter-spacing 0.08em, white/40

COLOR SYSTEM:
--bg: #09090b
--surface: rgba(255,255,255,0.03)
--text: #fafafa
--text-muted: rgba(255,255,255,0.55)
--text-dim: rgba(255,255,255,0.25)
--border: rgba(255,255,255,0.08)
--border-bright: rgba(255,255,255,0.18)

LIQUID GLASS EFFECT (apply to navbar, cards, badges, all pills):

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

The ::before creates a thin gradient border — bright at top/bottom, fades to invisible in the middle. Combined with backdrop-filter blur, this produces the liquid glass effect against the dark video background.

LIQUID GLASS STRONG (CTA buttons, icon circles — 50px blur for more visual weight):

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

FULL ANIMATION SYSTEM:

/* 1. WORD-BY-WORD BLUR REVEAL — hero headline */
/* Split headline text into individual word <span> elements in JavaScript:
   const words = headlineEl.textContent.split(' ');
   headlineEl.innerHTML = words.map((w, i) =>
     `<span style="display:inline-block;animation:blur-word 0.5s ease-out ${i * 100}ms both">${w}</span>`
   ).join(' ');
*/
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
/* Each word: duration 0.5s, staggered by 100ms per word index.
   Word 1 starts at 0ms, word 2 at 100ms, word 3 at 200ms, etc.
   Result: the headline assembles itself word-by-word from a blurred fog.
   This is triggered once on page load, not on scroll. */

/* 2. BLUR-IN — hero subtext and CTA buttons */
@keyframes blur-in {
  from { filter: blur(8px); opacity: 0; transform: translateY(16px); }
  to   { filter: blur(0px); opacity: 1; transform: translateY(0); }
}
/* Hero subtext: blur-in 0.7s ease-out, delay = (number of headline words × 100ms + 300ms)
   Hero CTAs: blur-in 0.6s ease-out, delay = subtext delay + 200ms
   Both play on load, not on scroll. */

/* 3. FADE-RISE — all sections below the hero fold */
@keyframes fade-rise {
  from { opacity: 0; transform: translateY(28px); }
  to   { opacity: 1; transform: translateY(0); }
}
/* Apply to every section below the hero using IntersectionObserver:
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
   Add class="animate-section" to each section wrapper, class="animate-child" to each child element. */

/* 4. HOVER REVEAL — the interactive product demo card */
/* This is the signature interaction. A static screenshot of your product is visible by default.
   On hover, it slides away to reveal a short looping demo video behind it.
   Implementation: two absolutely-positioned layers inside a relative container.
   Layer 1 (top, default visible): product screenshot image
   Layer 2 (below): <video> tag with your demo video, autoPlay loop muted playsInline
   On hover of the container: Layer 1 gets transform: translateY(-100%), opacity: 0, transition 0.4s ease-in-out
   Layer 2 becomes visible underneath.
   On hover exit: Layer 1 slides back down, transition 0.35s ease-in-out. */

/* 5. CARD HOVER STATES */
/* All liquid-glass cards: 
   transition: transform 0.2s ease, box-shadow 0.2s ease;
   :hover { transform: translateY(-4px); box-shadow: 0 16px 40px rgba(0,0,0,0.3); }
   CTA buttons (liquid-glass-strong):
   :hover { transform: scale(1.03); } transition 0.15s ease
   Secondary (white bg) buttons:
   :hover { background: rgba(255,255,255,0.9); } transition 0.15s ease */

/* 6. FRAMER MOTION (if using React) — add for smoother carousels and scroll effects */
/* After generating the base HTML, apply this refinement prompt:
   "Add Framer Motion (motion/react) to the interactive section. The product showcase 
   card should use motion.div with whileHover={{ y: -6, scale: 1.01 }} and 
   transition={{ type: 'spring', stiffness: 300, damping: 25 }}. 
   The feature cards should use motion.div with initial={{ opacity: 0, y: 24 }}, 
   whileInView={{ opacity: 1, y: 0 }}, viewport={{ once: true, amount: 0.2 }}, 
   and transition={{ duration: 0.5, delay: index * 0.1 }}." */

SECTIONS TO BUILD:

1. NAVBAR: Fixed, floating. Full-width, px-8 lg:px-16, py-4.
   Left: [PRODUCT NAME] in Instrument Serif italic 20px
   Center (desktop only, hidden on mobile): 3-4 nav links inside a liquid-glass rounded-full pill (px-1.5 py-1). Each link: Barlow 500 13px white/80 px-4 py-2. Last link is "Get Access" — solid white bg black text rounded-full px-4 py-2.
   Nav has no border, no background — floats above the hero video.

2. HERO: min-height 100vh, flex items-center justify-center, text-center. Content z-index 10. pt-24.
   - Context badge: liquid-glass rounded-full px-4 py-2. A small colored dot (4px, matches your brand accent) + label text in Barlow 600 11px uppercase letter-spacing-wide white/60. E.g. "Now on Product Hunt" or "Launching April 2026".
   - Headline: Instrument Serif italic, 80px desktop / 52px mobile, line-height 0.88, letter-spacing -0.03em, max-width 800px. 2-3 lines. [YOUR BOLD CLAIM — make this the most compelling sentence you know about your product].
   - Subtext: Barlow 300, 16px, white/55, max-width 500px, line-height 1.7, mt-6.
   - CTAs (mt-10 flex gap-4 justify-center):
     Primary: liquid-glass-strong rounded-full px-7 py-3.5 Barlow 500 15px + ArrowUpRight icon right
     Secondary: Barlow 300 15px white/60 flex items-center gap-2 + Play icon (filled, white, 16px)

3. HOVER REVEAL SECTION: py-28. "animate-section" class.
   Container: relative, max-w-4xl mx-auto.
   Heading: Instrument Serif italic, 52px, mb-4. "[FEATURE NAME] in action."
   Subtext: Barlow 300, 15px, white/55, max-width 480px, mb-12.
   The interactive card: liquid-glass rounded-3xl overflow-hidden, aspect-ratio 16/9, relative cursor-pointer.
   — Default state: your product screenshot fills the card. Small "Hover to see it live" label in bottom-left (Barlow 500 12px, liquid-glass pill, white/60).
   — Hover state: screenshot slides up and away (translateY -100%, opacity 0, 0.4s ease), demo video revealed underneath (autoPlay loop muted playsInline, object-cover, w-full h-full).
   — The contrast between static and live is what makes this section memorable.

4. FEATURE CARDS: py-24. "animate-section" class.
   Section label: Barlow 600 11px uppercase white/30 letter-spacing-wide mb-4. E.g. "Capabilities"
   Section heading: Instrument Serif italic 56px mb-16.
   3-column grid (stacks to 1 column on mobile). Each card: liquid-glass rounded-2xl p-8 "animate-child":
   — Icon: liquid-glass-strong rounded-full w-11 h-11 flex items-center justify-center + SVG icon white 18px
   — Feature name: Instrument Serif italic 22px mt-6 mb-3
   — Description: Barlow 300 14px white/55 line-height 1.75
   Features: [FEATURE 1 NAME + 2-sentence description], [FEATURE 2], [FEATURE 3]

5. CTA FOOTER: Second video background using [YOUR HERO VIDEO URL] (or a different Mux URL if you have one). Same gradient fades as hero (200px top, 300px bottom). "animate-section" on content.
   Heading: Instrument Serif italic 72px desktop / 44px mobile, line-height 0.88, max-width 700px, centered.
   Subtext: Barlow 300 16px white/50 max-width 460px mt-6.
   CTAs (mt-12 flex gap-4 justify-center):
   Primary: liquid-glass-strong rounded-full px-8 py-4 Barlow 500 15px
   Secondary: bg-white text-black rounded-full px-8 py-4 Barlow 500 15px hover:bg-white/90

MOBILE RESPONSIVENESS:
After generating, inspect on mobile. If anything breaks, use this fix prompt:
"Make the entire page fully responsive. On screens below 768px: headline font sizes should be 48px max, all multi-column grids should stack to 1 column, the navbar center pill should be hidden (show only logo + CTA button), and card padding should reduce to p-5. The video background should remain fullscreen on mobile."

OUTPUT: Single HTML file. All CSS in a <style> block in <head>. All animations as @keyframes in CSS. JavaScript only for: IntersectionObserver scroll triggers, word-splitting on headline, hover reveal video swap. No external dependencies except Google Fonts.
```

---

## Quick reference: what to customize

| Slot | What to put here |
|---|---|
| `[PRODUCT NAME]` | Your product name — appears in navbar, hero, and CTA |
| `[YOUR HERO VIDEO URL]` | Your Mux stream URL or CloudFront MP4 direct URL |
| `[YOUR BOLD CLAIM]` | The best 2-line sentence you know about your product — this is the most important slot |
| `[FEATURE NAME]` (hover section) | The specific feature or capability you are showcasing in the reveal |
| 3 feature card slots | Name + 2-sentence description for each |
| CTA footer heading | "Your next [thing] starts here." — customize the [thing] |

---

## No-video fallback path

If you do not have a Kling or Sedance video ready, or your deadline does not allow for the Mux upload, use this fallback. The page will still look premium — a tasteful CSS-only alternative that ships in 6 minutes instead of 45.

Replace the `BACKGROUND VIDEO` section of the prompt with this:

```
BACKGROUND (no video):
Hero section uses an animated CSS gradient background instead of video. Specification:

- Base: radial-gradient at 20% 30% with colors rgba(90,40,150,0.4) fading to transparent over 800px, layered over a linear-gradient from #09090b to #1a1625.
- Add a subtle animated noise texture via SVG filter (feTurbulence baseFrequency=0.9, opacity 0.03) — creates film-grain feel.
- Add 3-5 blurred orb shapes (border-radius 50%, backdrop-filter blur 120px, background rgba(accent, 0.15)) positioned absolutely, slowly drifting via CSS animation (translate X/Y by 40px over 20s, ease-in-out, infinite alternate).

The effect should feel like motion without being video. No jumpy loops, no hosting dependency, no mobile bandwidth penalty. Still uses the same gradient fades at top (200px) and bottom (300px) for text legibility.
```

This fallback is also what to use if you are embedding the prototype in a context where autoplay video is blocked (some email clients, some CMS embeds, iOS low-power mode).

---

## Accessibility — respect `prefers-reduced-motion`

Users with vestibular disorders, migraine triggers, or simply "I find animation distracting" settings need the page to work without the blur/rise/scroll animations. WCAG 2.1 requires this.

Add this refinement prompt after the initial generation:

```
Add prefers-reduced-motion media query support globally. Inside a
@media (prefers-reduced-motion: reduce) { ... } block:

- All @keyframes animations get replaced with opacity-only transitions (no transform, no filter, no scale).
- The word-by-word blur-word animation becomes a simple opacity fade-in with no blur, no translateY, no stagger greater than 30ms.
- The hover reveal card does not animate — it swaps the screenshot and video on hover instantly, no slide transition.
- The background video gets paused by default and replaced with the first frame as a static poster image. Add a small "Play background" button in the corner that unpauses it if the user explicitly wants motion.
- Scroll-triggered fade-rise becomes a simple opacity fade-in, no translateY.

Test by setting macOS System Settings → Accessibility → Display →
Reduce motion, then reloading the page. Nothing should animate
beyond a gentle fade.
```

This is 30 seconds of prompting that prevents your beautiful page from giving a reviewer a migraine. Do not skip it.

---

## The Framer Motion refinement prompt

Use this after the initial HTML generation if you want smoother, spring-physics animations on the interactive elements:

```
Convert the feature cards and hover-reveal section to use Framer Motion (motion/react).

For the feature cards: wrap each card in <motion.div initial={{ opacity: 0, y: 24 }} whileInView={{ opacity: 1, y: 0 }} viewport={{ once: true, amount: 0.2 }} transition={{ duration: 0.5, delay: index * 0.1 }}>

For the hover-reveal card: use <motion.div whileHover={{ scale: 1.01 }} transition={{ type: 'spring', stiffness: 280, damping: 22 }}>. The inner image layer should use <motion.img animate on parent hover state: { y: '-105%', opacity: 0 } transition={{ duration: 0.4, ease: [0.4, 0, 0.2, 1] }}>

For the hero headline: use a custom useEffect that splits the text and renders word spans with motion.span, each getting initial={{ filter: 'blur(10px)', opacity: 0, y: 50 }} animate={{ filter: 'blur(0px)', opacity: 1, y: 0 }} transition={{ duration: 0.5, delay: index * 0.1, ease: 'easeOut' }}

Import: import { motion } from 'motion/react'
```
