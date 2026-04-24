# Claude Design PM Prompt Toolkit
## Prompt 3: The Feature Flow Wireframe

**Use case:** PRD reviews, engineering handoffs, design feedback sessions, and stakeholder alignment. Gets everyone looking at the same thing before a single line of production code is written.

**What you get:** 4-screen interactive prototype with a clickable flow. Claude Code handoff ready. The kind of thing you used to wait 3 days for from a designer.

**How to use:** Fill in the context block honestly. The more specific you are about the user, the entry point, and what each screen should show, the better the output. Then use Prompt 3b (refinement) after you see the first generation.

> **⚠️ Before sending:** This prompt contains inline "Example:" blocks (italicized text after each screen description). Scrub those out before you hit Send, or Claude will merge your real context with the hiring-example context and produce a Frankenstein output. Search-and-replace `Example: "..."` with empty strings once you've filled in your own context.

---

## Prompt 3a — Initial Build

```
Build an interactive hi-fidelity prototype for [FEATURE NAME] in [YOUR PRODUCT NAME].

CONTEXT:
- Product: [WHAT YOUR PRODUCT DOES — 1 sentence]
- User: [WHO USES THIS — job title or persona, e.g. "a hiring manager setting up a new role"]
- Feature: [WHAT THIS FEATURE DOES — 1-2 sentences, be specific about the job it does]
- Entry point: [WHERE DOES THE USER START — e.g. "clicks 'New Role' from the Roles dashboard"]
- Exit point: [WHAT SUCCESS LOOKS LIKE — e.g. "role is live and first candidates are being scored"]

DESIGN DIRECTION:
[Describe your product's visual style in 2-3 sentences. Examples below — pick the one closest to yours or write your own:]

Option A (Clean SaaS): "Clean, white background, navy (#0D1B2A) primary color. Sidebar navigation with icon + label, content area fills the right 80%. Similar to Notion or Linear. Desktop-first at 1440px."

Option B (Dark Mode): "Dark theme, #0f0f11 background, white text. Monospace accents for data/code elements. Dense information layout. Similar to Vercel or Raycast. Desktop-first at 1440px."

Option C (Consumer): "Light, airy, lots of white space. Rounded corners everywhere (border-radius 16px+). Friendly typography, Inter or similar. Mobile-first at 375px with responsive desktop."

FONTS:
Import Readex Pro weights 300/400/500/600 from Google Fonts. Apply letter-spacing: -0.03em to all headings. Line-height 0.95 on large display text.

Or import your own brand fonts if you have a GitHub repo or Figma file attached to your design system.

ANIMATIONS:

@keyframes screen-enter {
  from { opacity: 0; transform: translateX(12px) scale(0.99); }
  to   { opacity: 1; transform: translateX(0) scale(1); }
}
@keyframes fade-up-quick {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}
@keyframes progress-fill {
  from { width: 0%; }
  to   { width: var(--progress-target); }
}

Apply animations:
- Screen transitions: when the user clicks a CTA that advances to the next screen, the current screen fades out (opacity 1→0, 0.2s ease-in), then the next screen plays screen-enter (0.35s ease-out). This makes the prototype feel like a real product, not a static slide.
- Content within each screen: all major elements (headings, forms, cards, CTAs) get fade-up-quick staggered at 60ms per element. Plays once per screen when that screen enters.
- Progress indicator (if your flow has one): progress bar uses progress-fill animation, CSS transition 0.4s ease, triggered when the user advances to each new screen. Set --progress-target as a CSS variable per screen (e.g. 25%, 50%, 75%, 100%).
- Form field focus states: border-color transitions from border to accent over 0.15s, subtle box-shadow appears (0 0 0 3px rgba(accent-color, 0.15))
- Primary CTA hover: transform: translateY(-2px), transition 0.15s ease
- Secondary/ghost button hover: background-color fades in, 0.15s ease

SCREENS TO BUILD (4 screens, fully clickable):

Screen 1 — Entry State:
[DESCRIBE what the user sees before they trigger the feature. Include: what the nav/sidebar shows, what the main content area shows, which button/link they click to start. Be specific about real UI elements, not placeholders.]

Example: "The Roles dashboard. Sidebar shows company logo, then nav items: Roles (active), Candidates, Pipeline, Reports, Settings. Main area shows a table of existing roles with columns: Role title, Department, Status (badge), Candidates, Last updated. A blue 'New Role' button in the top-right corner is the entry point. Clicking it advances to Screen 2."

Screen 2 — Setup / Configuration:
[DESCRIBE the input or configuration step. What fields, choices, or actions does the user take? What is required vs. optional? What should the form/UI look like?]

Example: "Role setup form. Full-screen modal or new page. Fields: Role title (text input), Department (dropdown), Hiring manager (user picker), Job description (large textarea — this is where the AI parsing happens). Below the textarea: a 'Parse with AI' button that shows a loading state, then reveals extracted criteria in a collapsible panel below. Required fields are marked. Footer: Back button (ghost) + 'Continue' primary CTA."

Screen 3 — Preview / Confirm:
[DESCRIBE the review step. What does the user see before committing? What can they still change?]

Example: "Review screen showing two columns: left column 'Your role summary' with the extracted criteria in tag format (each criterion is an editable pill — click to remove or add). Right column 'Scoring preview' showing 3 mock candidate cards scored against the criteria. Edit link in top-right. Footer: 'Go back' ghost + 'Launch role' primary CTA in green."

Screen 4 — Success State:
[DESCRIBE the confirmation. What does the user see? What is the next obvious action?]

Example: "Full-screen success state. A large animated checkmark (draw-in SVG animation, 0.6s). Headline: 'Your role is live.' Sub-copy: 'Candidates will be scored as they apply. You'll get a weekly digest every Monday.' Two CTAs: 'View role' (primary) + 'Create another' (ghost). Confetti particle animation (CSS only, 20 particles, 1s duration, fade-out after 2s)."

INTERACTIVE REQUIREMENTS:
- Every primary CTA must advance to the next screen
- Back buttons must return to the previous screen
- Minimum 1 interactive element per screen that is not navigation (a form field, a toggle, a dropdown, a hover state)
- Screen indicator: small pill or dots showing current step (1 of 4) visible on all screens
- Keyboard accessible: Tab through form fields, Enter submits primary action

OUTPUT: Interactive prototype. Clickable flow from Screen 1 through Screen 4. Export-ready for Claude Code handoff. Include a handoff README that specifies: [YOUR TECH STACK — e.g. "React + TypeScript + Tailwind, connects to REST API at /api/roles"], mobile responsive to 768px, WCAG 2.1 AA accessible.
```

---

## Prompt 3b — Refinement (use after first generation)

```
Good start. Three specific changes before we hand this off to engineering:

1. [ELEMENT TO FIX — be surgical, reference the exact screen and element]
Example: "Screen 2 — the job description textarea is too small. Make it at least 200px tall with a character counter in the bottom-right. The 'Parse with AI' button should show a spinner and 'Parsing...' text while the animation runs, not just a static loading state."

2. [SECOND ELEMENT — same level of specificity]
Example: "Screen 3 — the candidate preview cards show placeholder names. Replace with realistic mock data: real-looking names, specific scores (e.g. 87%, 72%, 91%), and 2-3 specific criteria tags per candidate (e.g. 'React', 'Led team of 5+', '3+ years SaaS')."

3. [THIRD ELEMENT]
Example: "Screen 4 — add a subtle detail below the success state: a small timeline showing 'Role created → AI scoring active → First digest Monday 9am'. Makes the success state feel like the beginning of something, not an end state."

Once these are applied, prepare the Claude Code handoff bundle. The README should specify:
- Framework: [YOUR STACK]
- API endpoints needed: [LIST THEM]
- Auth: [HOW USERS ARE AUTHENTICATED]
- Design system: [YOUR DESIGN TOKENS REPO OR FIGMA FILE LINK]
- Mobile: responsive down to 375px
- Accessibility: WCAG 2.1 AA
```

> See `11_claude_code_handoff.md` for the full README template.

---

## Localization / i18n note

If your product ships in more than one language, add this refinement prompt before handoff:

```
Wrap every piece of user-facing copy in an i18n-ready function call
using the pattern t('namespace.key'). Example: instead of
<button>Create role</button>, output
<button>{t('onboarding.create_role_cta')}</button>. Group keys by
screen (onboarding.screen1.headline, etc.). Extract all strings to a
single en.json file at the top of the output.

Handle RTL (right-to-left) layouts: add `dir="auto"` to the <html>
tag and use logical CSS properties (padding-inline-start instead of
padding-left). Icons that indicate direction (arrows, chevrons) get
`rtl:rotate-180` classes so they mirror in Arabic and Hebrew.
```

This adds ~60 seconds to the generation but saves hours of retrofit when an engineer has to internationalize the prototype later.
