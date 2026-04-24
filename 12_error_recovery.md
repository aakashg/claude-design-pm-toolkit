# Claude Design PM Prompt Toolkit
## Reference: Error Recovery — Common Failures + Fix Prompts

When Claude Design produces something broken, the fix almost always falls into one of these 14 patterns. Each has a copy-paste fix prompt. Use these before trying to rebuild from scratch.

---

## 1. Liquid glass effect is not showing

**Symptom:** The glass cards look like flat gray boxes. No blur, no gradient border.

**Root cause:** `backdrop-filter` does not work against a transparent page background. It needs something behind it to blur.

**Fix prompt:**
```
The liquid glass cards are not showing a blur effect. This is because backdrop-filter needs content behind the element to blur. Fix by ensuring the parent of any .liquid-glass element has a non-transparent background — either a solid color (#09090b), a gradient, or a background video. Check that the z-index stacking is correct: the video/background is z-0, the glass element is z-10+.
```

---

## 2. Mobile layout is broken

**Symptom:** Horizontal scroll on mobile. Text overflowing cards. Hero headline is too big.

**Fix prompt:**
```
The page is not mobile-responsive. Apply these fixes globally:
- Any headline over 48px on desktop caps at 48px on screens below 768px
- All 2-column and 3-column grids collapse to 1 column below 768px
- All card padding reduces from p-8 to p-5 below 768px
- The navbar shows only the logo and primary CTA below 768px (hide center nav links)
- No element should cause horizontal scroll at 375px width
- Test mentally at 320px, 375px, 768px — if any layout breaks, fix before returning
```

---

## 3. Video background will not load

**Symptom:** Black box where the hero video should be. Or the video flashes once then disappears.

**Fix prompts by cause:**

**If using an MP4 URL:**
```
The video tag is not loading the video. Check: 1) The URL returns a 200 when opened in a browser. 2) The tag has autoPlay, muted, playsInline, AND loop attributes — all four are required for iOS. 3) The type attribute matches the URL extension. If the URL is .mp4, type="video/mp4". If .m3u8, use HLS.js to load it (browsers cannot play HLS natively without a library).
```

**If the URL is from Mux:**
```
The Mux URL is an HLS stream (.m3u8) which browsers cannot play natively. Either: convert to the Mux MP4 URL (replace stream.mux.com/ID.m3u8 with stream.mux.com/ID/high.mp4) OR import HLS.js and attach it to the video element. Prefer the MP4 URL for simplicity.
```

---

## 4. Animations are too slow / janky / don't play

**Fix prompt (too slow):**
```
The animations are too slow. Reduce these durations globally:
- fade-rise: 0.65s → 0.4s
- blur-word: 0.5s → 0.4s
- stagger delay: 120ms → 80ms
Total hero reveal should feel under 1 second, not 2+ seconds. Speed matters more than smoothness on landing pages.
```

**Fix prompt (janky):**
```
The animations stutter. Likely causes: 1) Too many elements animating at once — reduce stagger group size to max 5 elements per trigger. 2) Animating box-shadow instead of using a pseudo-element — box-shadow is expensive on paint. 3) Missing will-change hints — add will-change: transform, opacity to any element that animates on scroll.
```

**Fix prompt (doesn't play):**
```
The scroll-triggered animations are not firing. Verify: 1) The IntersectionObserver is actually attached — console.log the observed elements. 2) The threshold is reasonable (0.12 is good; 0.5 can miss if sections are short). 3) The .animate-child elements have animation-fill-mode: both, otherwise they return to invisible after completing.
```

---

## 5. Fonts are wrong / falling back to Times

**Symptom:** Headings render in Times New Roman instead of Instrument Serif. Body is Arial instead of Barlow.

**Fix prompt:**
```
The custom Google Fonts are not loading. Check: 1) The <link> tag is inside <head>, not <body>. 2) The Google Fonts URL is complete — ending with "&display=swap". 3) The font-family CSS property spells the font name exactly as Google Fonts names it (case-sensitive). 4) If using a licensed brand font, check that the @font-face src URL is publicly accessible, not a localhost or auth-gated path.
```

---

## 6. Hover reveal card shows the video but not the screenshot

**Symptom:** The default state shows the video, not the screenshot. Or the screenshot never slides away on hover.

**Fix prompt:**
```
The hover reveal is inverted. Fix the z-index stacking: .reveal-screenshot should have z-index: 2, .reveal-video should have z-index: 1. On :hover of the container, .reveal-screenshot gets transform: translateY(-105%) and opacity: 0. Current code may have the layers reversed or missing the :hover selector on the right parent.
```

---

## 7. Word-by-word blur animation does not trigger

**Symptom:** Headline appears all at once instead of animating word-by-word.

**Fix prompt:**
```
The word-splitting JS is not running. Verify: 1) The script runs after DOMContentLoaded. 2) The headline element has the class or selector the script is targeting (class="headline-blur" or similar). 3) The script is in a <script> tag with defer attribute, OR placed at the end of <body>. 4) The @keyframes blur-word is defined before the animation is applied — check order in the <style> block.
```

---

## 8. Liquid glass looks different on Safari vs Chrome

**Symptom:** The gradient border is crisp on Chrome, blurry / missing on Safari.

**Fix prompt:**
```
The liquid glass gradient border uses mask-composite which requires both -webkit-mask-composite: xor AND mask-composite: exclude. Verify both are present in the CSS. Also verify -webkit-backdrop-filter is set alongside backdrop-filter (Safari requires both). If still broken on Safari, the padding trick may be hitting a Safari bug — reduce padding from 1.4px to 1px and test again.
```

---

## 9. Colors drifted from the Design System

**Symptom:** Claude used purple when your brand is navy. Used Lucide icons when your system is Phosphor.

**Fix prompt (use Tweaks panel first — it is free):**
```
Do NOT prompt Claude for this. Open the Tweaks panel (right sidebar). Change the accent color globally via the Tweaks color picker. This resets every prototype screen at once, costs zero tokens. Only use a prompt if Tweaks cannot reach the specific color (rare).
```

**If Tweaks does not fix it:**
```
The page uses colors that are not in our brand palette. Remove all of: [list offending colors — e.g. purple, gradients, teal]. Replace with: primary #0D1B2A, accent #E85D2F, neutral grays only. No gradient backgrounds anywhere. No colored shadows.
```

---

## 10. Sample data is placeholder / looks fake

**Symptom:** "John Doe" names. "Lorem ipsum" anywhere. Numbers like "$XX.XX" or "123,456".

**Fix prompt:**
```
Replace all placeholder data with realistic sample data. Rules:
- Names: use a mix of cultures (e.g. Priya Ramachandran, Ade Okonkwo, Wei Chen, Maria Lopez, Idris Haidari). 8 names minimum across the page.
- Numbers: use plausible specific values, not round numbers. E.g. "$4,237" not "$5,000". "87%" not "90%". "23 candidates" not "many".
- Copy: use sentences a real PM at a Series B company would write, not marketing fluff.
- Any remaining "Lorem ipsum" is an immediate rebuild trigger — scan for it and replace.
```

---

## 11. The page is visually stiff / feels like a template

**Symptom:** Everything lines up perfectly, predictable card grid, no hierarchy. Looks like a Tailwind starter.

**Fix prompt:**
```
The page is too rigid. Break the grid in specific ways:
- Asymmetric hero: headline max-width 600px, sub-copy max-width 480px, offset left — not centered
- One card in the feature grid should be 1.5x the width of the others, not a uniform 3-col
- Mix typography weights within a single headline — "The old way" in Instrument Serif italic, "vs. our way" in Barlow 500 caps
- Add one unexpected element — an ambient background glow, a rotating tag pill, a subtle scroll-linked parallax on the hero
The goal is "intentionally designed" not "template".
```

---

## 12. Accessibility scan fails (WCAG, Axe, Lighthouse a11y)

**Symptom:** You ran an Axe scan or Lighthouse audit on the generated page and got 5+ violations: low contrast, missing alt text, no focus rings, missing labels.

**Fix prompt (general — covers ~80% of common failures):**
```
Run an accessibility pass. Apply globally:

1. Color contrast: every text element must hit WCAG 2.1 AA — 4.5:1 for body text, 3:1 for large text (18px+, or 14px+ bold). If the current --text-muted (white/55) fails on the dark background, bump to white/72 globally. Check overlay text on video backgrounds — increase the dark overlay from bg-black/25 to bg-black/40 if needed.

2. Focus states: every interactive element gets a visible focus ring on :focus-visible. Use a 2px outline in the accent color with a 2px offset. No default browser outline-none anywhere.

3. Alt text: every <img> tag has a meaningful alt attribute. Decorative images get alt="". Icon-only buttons get aria-label. SVG icons get role="img" with a <title> child.

4. Form labels: every input has a corresponding <label> with htmlFor. Placeholder text is not a label substitute — required fields get a visible asterisk and aria-required="true".

5. Heading hierarchy: one <h1> per page. No skipped levels (no h1 → h3). Headings describe the section they label.

6. Keyboard nav: tab order follows visual order. All interactive elements reachable. Esc closes modals. Enter submits primary action.

7. Reduced motion: wrap all animations in @media (prefers-reduced-motion: reduce) — replace transforms with opacity-only fades.

After applying, re-run Axe — there should be 0 critical or serious violations.
```

**Fix prompt (low-contrast text on video backgrounds specifically):**
```
The hero text overlaying the video background fails WCAG contrast.
Two options, pick one based on aesthetic preference:

Option A (preserve dark video, increase overlay): Increase the dark
gradient overlay from bg-black/25 to bg-black/45. This shifts the
video's exposed mid-tones darker and lifts the white text contrast
above 4.5:1 on most frames.

Option B (text shadow): Add a subtle text-shadow to all overlaying
text: text-shadow: 0 2px 8px rgba(0,0,0,0.5). This gives white text
edge contrast even on bright video frames. Use 0.5 opacity at most —
heavier reads as 2010s.

Test by pausing the video at 3-4 different moments (extract still
frames, run through a contrast checker against the overlaying text
color). All passes? Ship. Any failures? Increase further.
```

---

## 13. prefers-reduced-motion is not respected

**Symptom:** You enabled "Reduce motion" in your OS settings, reloaded the page, and the word-by-word blur animation still runs. Vestibular-disorder reviewers will not trust the page.

**Fix prompt:**
```
The page does not honor prefers-reduced-motion. Add to the global
CSS:

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}

Then specifically: pause the background video on mount if matchMedia(
'(prefers-reduced-motion: reduce)').matches is true — replace the
playing video with a poster image of frame 0. Show a small "Play
background" button in the corner that lets the user opt back in.

The word-by-word blur animation should become a single opacity fade
of 200ms on the whole headline, no per-word stagger, no blur, no
translateY.
```

---

## 14. Claude keeps regenerating the same wrong thing

**Symptom:** You used Comments 3 times to fix the same element. Claude keeps reverting.

**Root cause:** Context drift. After enough Comments, the conversation has too many competing directives. Claude starts averaging them.

**Fix — do not prompt your way out of this. Do this instead:**

1. Open the Tweaks panel. Fix what you can globally, free.
2. Use Edit directly on the stuck element. Click, change, done. No tokens.
3. If the problem is structural (needs a layout change), duplicate the project (Share → Duplicate project), open the copy, and re-prompt from scratch with the clarifying questions done better this time (see `10_clarifying_questions.md`).

Regenerating from scratch with better inputs is almost always faster than fighting a 15-Comment session. Your first week of Claude Design, you will try to fight the session. By week three, you will duplicate and re-prompt. Duplicate early.

---

## The meta-pattern — when to stop prompting

If you have:
- Made 3+ Comments that did not stick, OR
- Made 5+ Edits on the same section, OR
- Spent more than 10 minutes on a single fix

**Stop.** Duplicate the project. Use Tweaks for global fixes. Re-prompt if structural. Edit everything else in the duplicate. This is the 90-second reset that keeps your weekly token quota intact.
