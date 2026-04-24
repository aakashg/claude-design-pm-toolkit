# Claude Design PM Prompt Toolkit
## Prompt 1: The Investor Demo Page

**Use case:** Series A decks, board updates, VC calls, and any moment where you need your product to look like it deserves the raise.

**What you get:** Dark premium single-page demo. Liquid glass cards, cinematic typography, animated metrics strip, before/after section. Goes from prompt to shareable link in roughly 8 minutes.

**Customize 3 things only:**
- `[YOUR COMPANY NAME]` — appears 3 times
- `[ONE-LINE DESCRIPTION]` — e.g. "AI-powered contract review for legal teams"
- The 4 `[METRIC]` slots — e.g. "2,400+ users", "94% retention", "3x faster", "$2.1M ARR"

---

## The Prompt

```
Build a dark premium single-page investor demo for [YOUR COMPANY NAME], a [ONE-LINE DESCRIPTION OF WHAT YOU DO].

AESTHETIC: Dark, cinematic, editorial. Black background (#09090b), white text, liquid glass card effects. Feels like a Series A deck turned into a living webpage.

FONTS:
Import from Google Fonts:
https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Barlow:wght@300;400;500;600&display=swap

- Headings: Instrument Serif (italic) — all hero text, section titles, stat numbers
- Body: Barlow weight 300/400/500 — all body copy, captions, nav links

LIQUID GLASS EFFECT (apply to all cards, nav pill, and badges):

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

The ::before pseudo-element creates a gradient border using mask-composite — a thin glowing edge that is bright at the top and bottom, fades in the middle. The backdrop-filter blur gives the glass effect its depth against dark backgrounds.

LIQUID GLASS STRONG (for CTA buttons and icon circles — more prominent):

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

ANIMATIONS:

@keyframes fade-rise {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}
@keyframes blur-in {
  from { filter: blur(8px); opacity: 0; transform: translateY(16px); }
  to   { filter: blur(0px); opacity: 1; transform: translateY(0); }
}
@keyframes counter-up {
  from { opacity: 0; transform: translateY(12px); }
  to   { opacity: 1; transform: translateY(0); }
}

Apply animations as follows:
- Navbar: no animation, always visible
- Hero badge pill: blur-in, 0.5s ease-out, delay 0s
- Hero headline (word-by-word): split the headline text into individual <span> elements, one per word. Each word gets blur-in animation, duration 0.5s, staggered by 80ms per word (word 1 delay 0ms, word 2 delay 80ms, word 3 delay 160ms, etc.). This creates a cinematic word-reveal where the headline assembles itself on load.
- Hero subtext: blur-in, 0.7s ease-out, delay equal to (number of headline words × 80ms + 200ms)
- Hero CTA buttons: fade-rise, 0.6s ease-out, delay 100ms after subtext
- Metrics strip: each stat card gets counter-up, 0.5s ease-out, staggered 100ms per card, triggered by IntersectionObserver when the strip enters the viewport
- All sections below fold: fade-rise on scroll, triggered by IntersectionObserver (threshold 0.15), duration 0.6s ease-out, staggered 120ms per child element
- Card hover states: transform: translateY(-3px), box-shadow intensifies slightly, transition 0.2s ease

SECTIONS TO BUILD:

1. NAVBAR: Fixed position, floating. Liquid-glass rounded-full pill containing: company name left (Instrument Serif italic, 18px), 3 nav links center (Barlow 500, 13px, white/70, hover → white), "Book a Demo" CTA right (liquid-glass-strong rounded-full, px-4 py-2, Barlow 500 13px).

2. HERO: Centered, paddingTop 160px. 
   - Badge pill: liquid-glass rounded-full px-4 py-1.5 — "Series A Ready" or similar, Barlow 600 11px uppercase white/60
   - Headline: Instrument Serif italic, 80px desktop / 48px mobile, line-height 0.9, letter-spacing -0.03em. 2 lines max: "[YOUR COMPANY NAME] is [BOLD CLAIM]". Split into word spans for stagger animation.
   - Subtext: Barlow 300, 16px, white/60, max-width 520px, line-height 1.7
   - CTAs: "See the Product" (liquid-glass-strong, rounded-full, px-6 py-3, ArrowUpRight icon) + "Book a Demo" (bg-white text-black rounded-full px-6 py-3)

3. METRICS STRIP: Full-width liquid-glass card, rounded-2xl, p-8. 4-column grid. Each column: number in Instrument Serif italic 52px + label in Barlow 300 13px white/50. Use: [METRIC 1 number + label], [METRIC 2], [METRIC 3], [METRIC 4]. Thin vertical dividers (1px, white/10) between columns.

4. PROBLEM SECTION: 2-column, gap-16. Left: "The problem with how [YOUR INDUSTRY] works today" as heading + 3 pain-point lines (each with a × icon in red/70). Right: liquid-glass card showing before/after — left half "Before" (gray/40 bg, pain summary) vs right half "After" (your solution, white text). Simple visual divider between them.

5. TRACTION: "What we have built" centered heading. 3 liquid-glass cards in a row (rounded-2xl p-8): product screenshot placeholder (left), key milestone text (center, Instrument Serif italic large number), testimonial quote (right, Barlow 300 italic white/70 + attribution).

6. CTA FOOTER: Dark section (#000). "Ready to see it?" in Instrument Serif italic 64px. "Book a Demo" white button centered. Footer line: © 2026 [Company]. white/20.

OUTPUT: Single HTML file. All CSS inline. No external dependencies except Google Fonts.
```

---

## What to put in each slot

| Slot | Example |
|---|---|
| Company name | Arcline |
| One-line description | AI-powered onboarding platform for B2B SaaS teams |
| Metric 1 | 2,400+ / active workspaces |
| Metric 2 | 94% / 90-day retention |
| Metric 3 | 3.2x / faster time-to-value |
| Metric 4 | $2.1M / ARR |
| Industry (problem section) | B2B SaaS onboarding |
| Bold claim | the fastest path from signup to activation |

---

## Board-facing variant (CTA copy swap)

The default CTAs ("See the Product" + "Book a Demo") read consumer / prospect-facing. If you are sending this link to your board or investors rather than prospects, swap the hero CTAs:

- Primary: **"Read the board memo"** (linked to a Google Doc) or **"Open the update"** (linked to a Notion page)
- Secondary: **"Book 15 min with [founder name]"**

Board members do not "book a demo." They want a deep-dive memo and time with the founder. Same layout, different CTA pattern.

---

## Accessibility note — WCAG contrast on dark video backgrounds

The default text-on-dark in this prompt uses `white/60` and `white/55` against a black background. This is fine on flat black. It may fail WCAG 2.1 AA on some sections where the underlying video is light or varied.

Before sharing the link externally:

1. Open the page at the intended viewing size (stakeholders often open on a laptop, not 4K).
2. Screenshot and run through a contrast checker (WebAIM's tool or the Stark Figma plugin).
3. If body copy at white/55 fails: bump to white/75 globally via Tweaks (free, one click). The page stays legible without losing the dark-premium feel.
4. For any text that overlays a video background directly, increase the dark overlay from `bg-black/25` to `bg-black/40` — this protects legibility on brighter Kling frames.

Do not skip this. A "premium" demo that fails a screen reader or a low-vision reader is not premium. It just failed.
