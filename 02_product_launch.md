# Claude Design PM Prompt Toolkit
## Prompt 2: The Product Launch Page

**Use case:** Feature announcements, beta launches, waitlists, and Product Hunt days. High-conversion, clean SaaS aesthetic. The kind of page you used to spend a week building with a designer and an engineer.

**What you get:** White/navy launch page. Badge + headline + email capture. Feature grid. Before/after comparison. Social proof bar. Goes from prompt to shareable link in roughly 6 minutes.

**Customize 4 things:**
- `[FEATURE OR PRODUCT NAME]` — the thing you are launching
- `[ONE SENTENCE]` — who it is for and what it does
- 3 `[FEATURE N]` slots — name + 2-sentence description each
- The before/after pain points — real problems your product solves

---

## The Prompt

```
Build a product launch landing page for [FEATURE OR PRODUCT NAME], which [ONE SENTENCE: WHAT IT DOES AND WHO IT IS FOR].

AESTHETIC: Clean, modern, high-contrast. White background with deep navy (#0D1B2A) accents. Premium SaaS feel — not startup hustle. Feels like Vercel or Linear shipped this page.

FONTS:
Import from Google Fonts:
https://fonts.googleapis.com/css2?family=Readex+Pro:wght@300;400;500;600;700&display=swap

Set body: font-family: 'Readex Pro', system-ui, sans-serif; background: #fff; color: #0D1B2A; -webkit-font-smoothing: antialiased;

Add a utility class:
.hero-title {
  letter-spacing: -0.04em;
  line-height: 0.95;
}

COLOR SYSTEM:
--bg: #ffffff
--bg-secondary: #f4f6f8
--text-primary: #0D1B2A
--text-muted: #64748b
--accent: #0D1B2A
--accent-light: #e4edf6
--border: #e2e8f0
--success: #15803d
--success-bg: #f0fdf4
--success-border: #bbf7d0

ANIMATIONS:

@keyframes fade-up {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
@keyframes fade-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}
@keyframes slide-in-left {
  from { opacity: 0; transform: translateX(-16px); }
  to   { opacity: 1; transform: translateX(0); }
}
@keyframes slide-in-right {
  from { opacity: 0; transform: translateX(16px); }
  to   { opacity: 1; transform: translateX(0); }
}

Apply animations:
- Launch badge: fade-up, 0.5s ease-out, delay 0s, plays on page load
- Hero headline: fade-up, 0.7s ease-out, delay 0.1s. Apply .hero-title class. Font-weight 500. Font size 80px desktop / 48px mobile.
- Subheadline: fade-up, 0.6s ease-out, delay 0.25s
- CTA buttons row: fade-up, 0.6s ease-out, delay 0.4s
- "No credit card required" micro-copy: fade-in, 0.4s ease-out, delay 0.6s
- Social proof bar: fade-in, 0.5s ease-out, delay 0.2s after it enters viewport (IntersectionObserver, threshold 0.2)
- Feature cards: each card gets fade-up with staggered delay. Card 1: 0ms, Card 2: 100ms, Card 3: 200ms. All triggered by IntersectionObserver when the grid enters viewport.
- Before/after columns: left column slides in from left (slide-in-left, 0.6s), right column slides in from right (slide-in-right, 0.6s), both triggered simultaneously when the section enters viewport. Adds tension to the comparison.
- CTA section: fade-up on all children, staggered 120ms, triggered on scroll

Hover states (no animation library needed, CSS only):
- Feature cards: transform: translateY(-4px), box-shadow: 0 8px 24px rgba(13,27,42,0.08), transition 0.2s ease
- CTA primary button: background darkens to #1a2f4a, transition 0.15s ease
- Nav links: color transitions from text-muted to text-primary, 0.15s ease
- "Watch demo" text link: underline appears, 0.15s ease

SECTIONS TO BUILD:

1. NAVBAR: Simple, not sticky. Max-width 7xl, mx-auto, px-6 py-5. Logo text left (company name, font-weight 600, 18px). Nav links center (hidden on mobile): "Product", "Pricing", "Docs", "Blog" — text-muted, font-medium 14px, hover → text-primary, transition. CTA right: "Get Early Access" — bg #0D1B2A white text rounded-full px-5 py-2.5 font-medium 14px, hover:bg-[#1a2f4a].

2. HERO: Centered, pt-28 pb-20.
   - Launch badge: inline-flex items-center gap-2, bg success-bg text success border success-border rounded-full px-3 py-1.5, font-medium 13px. A 6px green dot + "Now Available" text.
   - Headline: .hero-title class, font-weight 500, 80px desktop / 48px mobile, max-width 800px, color text-primary. The product name should be on its own line if possible.
   - Subheadline: text-muted, 18px, font-weight 300, max-width 520px, line-height 1.6, mt-6
   - CTAs (mt-10): "Start for free" (bg #0D1B2A white text rounded-full px-6 py-3 font-medium 15px) + "Watch 2-min demo" (text-link with Play icon, text-muted, hover → text-primary). Gap-4 between buttons.
   - Micro-copy below CTAs: "No credit card required. Setup in 5 minutes." text-muted text-sm mt-4

3. SOCIAL PROOF BAR: mt-16, py-8, border-y border-[--border]. "Trusted by teams at" left in text-muted 13px font-medium. Then 5 company names right: font-weight 500, 15px, text-muted, gap-10. Simple horizontal flex.

4. FEATURE GRID: pt-24 pb-16. Section heading: "Everything you need. Nothing you don't." — .hero-title, font-weight 500, 42px, centered, mb-4. Sub-heading: text-muted, 16px, font-weight 300, centered, mb-16, max-width 480px. Grid: grid-cols-1 md:grid-cols-3 gap-6. Each card: bg bg-secondary rounded-2xl p-7, border border-[--border]. Icon in a 40px circle (bg accent-light, text accent, rounded-full flex items-center justify-center) + Feature name (font-weight 600, 16px, mt-4 mb-2) + 2-sentence description (text-muted, 14px, font-weight 300, line-height 1.7). Features: [FEATURE 1 NAME + DESCRIPTION], [FEATURE 2 NAME + DESCRIPTION], [FEATURE 3 NAME + DESCRIPTION].

5. BEFORE/AFTER: py-24. "The old way vs. the right way" heading centered. 2-column grid gap-8 mt-16. Left card (bg bg-secondary, rounded-2xl p-8, border): "Before [PRODUCT NAME]" heading in text-muted 14px uppercase tracking-wide font-medium. Then 3 pain points, each with a red × icon (text-red-500) + pain statement in text-primary 15px font-weight 300. Right card (bg #0D1B2A, rounded-2xl p-8, text-white): "With [PRODUCT NAME]" heading in white/60 14px uppercase. Then same 3 problems solved with green ✓ icons (text-green-400) + solution in white 15px font-weight 300.

6. EMAIL CTA: bg #0D1B2A, py-24, text-center. Heading: "Start [doing the thing] today." — .hero-title, white, font-weight 500, 52px. Sub: "Free to start. Scales with your team." white/60, 16px font-weight 300, mt-4. Email + button row: inline-flex gap-3 mt-10. Input: bg-white/10 border border-white/20 rounded-full px-5 py-3 text-white placeholder:text-white/40 w-72. Button: bg-white text-[#0D1B2A] rounded-full px-6 py-3 font-medium 15px, hover:bg-neutral-100.

OUTPUT: Single HTML file. All CSS inline as <style> block in <head>. Only external dependency: Google Fonts.
```

---

## What to put in each slot

| Slot | Example |
|---|---|
| Feature/product name | HireIQ Onboarding Flow |
| One sentence | An interactive onboarding experience builder for B2B SaaS teams that cuts time-to-activation by half |
| Feature 1 | AI-Parsed Job Descriptions / Paste any JD and HireIQ extracts role requirements, seniority, and scoring criteria in 3 seconds |
| Feature 2 | Automated Candidate Scoring / Every applicant is scored against your extracted criteria before a human reviews anything |
| Feature 3 | Live Pipeline View / See every candidate's stage, score, and next action in one screen — no spreadsheet toggling |
| Pain point 1 | Manually read through 40+ applications every Monday morning |
| Solution 1 | Pre-scored stack ranked by fit before you open your laptop |

---

## Analytics hook variants (use as refinement prompts after first generation)

The default page has no analytics wiring. Pick the one matching your stack and paste as a follow-up prompt:

**PostHog:**
```
Add PostHog event tracking. Primary CTA click: posthog.capture('launch_hero_cta_clicked', {variant: 'A'}). Email submit: posthog.capture('launch_email_submitted'). Secondary "Watch demo" click: posthog.capture('launch_demo_opened'). Feature card hover: posthog.capture('launch_feature_hovered', {feature_name}). Use the posthog-js library loaded via <script> tag.
```

**Segment:**
```
Add Segment tracking via window.analytics. Wrap every primary CTA click with analytics.track('CTA Clicked', {location: 'launch-hero', variant: 'primary'}). Email submit: analytics.track('Email Captured', {source: 'launch-page'}). Scroll depth: analytics.track('Scroll Depth Reached', {percentage: 50|75|100}).
```

**Google Analytics 4:**
```
Add GA4 tracking via gtag. Primary CTA: gtag('event', 'cta_click', {location: 'launch-hero'}). Email submit: gtag('event', 'generate_lead', {method: 'email-capture'}). Include the GA4 gtag bootstrap snippet in <head> with GA_MEASUREMENT_ID as a placeholder I can replace.
```

---

## Email capture integration variants (use as refinement prompts)

**ConvertKit:**
```
Wire the email input to ConvertKit. Form action: https://app.convertkit.com/forms/[FORM_ID]/subscriptions. Method: POST. On submit: show a success state replacing the form — "You are on the list. Check [email] for a confirmation." with a 400ms fade-in animation. On error: inline error message in red, keep the form visible.
```

**HubSpot Forms:**
```
Wire the email input to a HubSpot Form. Use the hbspt.forms.create script with portalId: [PORTAL], formId: [FORM_ID]. On successful submit: smooth scroll back to the hero and replace the form with the confirmation block. On error: inline error message, retry button.
```

**Resend (transactional, self-rolled):**
```
Wire the email form to POST to /api/capture with {email, source: 'launch'}. On success, show a confirmation block with the user's email. On error, show the error message with a "Try again" link. Include the relevant fetch() code with loading, error, and success states.
```

Pick one based on your stack. Paste as a follow-up prompt. Claude Design wires it in without re-rendering the page.
