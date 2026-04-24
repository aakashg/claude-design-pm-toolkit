# Claude Design PM Prompt Toolkit
## Prompt 9: Design System Setup + SKILL.md Template

**Use case:** The one-hour investment that makes every prompt in this toolkit look like your actual product instead of a Claude default. Do this once. Every prototype after that inherits from it.

**What you get:** A custom Design System registered in Claude Design. Every future prototype you generate pulls from it automatically — your colors, your fonts, your component styles. Plus a SKILL.md file that tells Claude who your brand is in plain English.

**Time:** 45–60 minutes of setup. Pays off on every project after.

---

## Part 1 — Create the Design System in Claude Design

1. Go to `claude.ai/design` → **Design systems** (top nav) → **New design system**
2. Fill in company name + a 2-sentence product description. Be specific: what you build, who uses it, and the design language (clean SaaS / premium editorial / friendly consumer / technical dark).
3. Attach **all four** context sources if you have them:
   - **GitHub repo** — paste the frontend *subfolder* URL (e.g. `github.com/acme/web/tree/main/apps/frontend`), not the root. Claude only needs frontend-relevant files.
   - **Figma file** — trim to core elements before uploading. Remove page templates, archived versions, sandbox frames. Target under 75 pages. Large files burn tokens before generation starts.
   - **Brand assets** — logos (SVG preferred), fonts if licensed, any PDF brand guide.
   - **Any other notes** — one sentence on what the brand *is not* does as much work as the whole rest of the field. Example: "We do not use gradients. We do not use drop shadows. We never put serifs on buttons."
4. Click **Generate**. Claude runs a web search on your company, audits every file, builds the system. ~5 minutes. Leave the tab open in the background.

---

## Part 2 — Validate before you trust it

Every category gets a **Looks good** / **Needs work** toggle. Do not skip this. Go through them in this order — these are where Claude makes the most mistakes:

### Typography (highest failure rate)
Claude will substitute a free web font for a licensed typeface. If your brand uses a custom font (e.g. Söhne, ABC Favorit, a custom Monotype commission), Claude will replace it with the nearest Google Fonts match. Override this category first.

### Colors (second highest failure rate)
Claude drifts on *semantic* color rules. Your system might say "green = success state only" — Claude will generate green primary CTAs anyway. Validate every semantic slot:
- Primary action
- Success state
- Error state
- Warning state
- Info state

### Components
Check buttons, cards, form inputs against your actual live components. The most common failure points are:
- **Border-radius** — Claude picks a generic 8px; your system might be 4px or 12px.
- **Icon set** — Claude defaults to Lucide. Your product might use Phosphor or a custom set.
- **Shadow style** — Claude loves `0 4px 12px rgba(0,0,0,0.1)`. Your system might be flat.

### Everything else
Tap through quickly. The three above are where 80% of misreads happen.

---

## Part 3 — Write your SKILL.md

This is the file Claude reads at the start of every prototype generation in your design system. It is the single highest-leverage file in your setup. Every new prototype gets better when this file gets better.

Copy this template, fill it in, paste it into the SKILL.md editor in Claude Design.

```markdown
---
name: [COMPANY-NAME]-design
description: Use this skill to generate well-branded interfaces and assets for [COMPANY NAME].
---

# [COMPANY NAME] Design

In this SKILL.md file — we summarize the full brand story, voice, visual foundations, and component rules. Then sections:

- [colors.md](colors.md) — every color and typography token we should reference for consistent branded work.
- (your other linked files)

## Who we are

[ONE-PARAGRAPH STORY: what you build, who uses it, the problem you solve, what makes you different. Write this in the voice of the product, not a marketer. Example: "Arcline is an AI-powered onboarding platform for B2B SaaS teams. We replace the three-week handoff between sales, product, and CS with a single flow that configures itself from the customer's existing Notion or Linear. Our users are heads of CS and implementation engineers, and they tell us the product feels like Linear merged with a really good IDE."]

## How we sound

[5-7 BULLETS on voice. Examples:]
- Short sentences. Active voice. No hedging.
- Specific numbers, never ranges.
- We never say "seamless", "synergy", "powerful", or "revolutionary".
- We are direct with the customer even when the answer is no.
- Labels are nouns, buttons are verbs. Never "Click here".

## What we look like — visual foundations

[KEY RULES. Examples:]
- Primary brand color: `#0D1B2A` (navy). Used for text and primary CTAs only.
- Accent color: `#E85D2F` (orange). Used sparingly — success states and one element per page, max.
- Background: white (`#ffffff`) or off-white (`#f4f6f8`). Never colored backgrounds.
- Typography: Söhne for display, Inter for body. No italics except in testimonial quotes.
- Border-radius: 8px for cards, 9999px for pills. Never 4px, never 16px.
- No gradients. No drop shadows on cards. Single hairline borders only.

## Component rules

- Primary button: `bg-[#0D1B2A] text-white rounded-full px-5 py-2.5 font-medium 14px`
- Card: `bg-white border border-[#e2e8f0] rounded-xl p-6`
- Icons: Phosphor Icons (regular weight, 20px default). Never Lucide, never filled variants, never emoji.
- Form inputs: `border border-[#e2e8f0] rounded-lg px-4 py-2.5`, focus ring in the accent color.

## Illustration style

[HOW IMAGES, ILLUSTRATIONS, ABSTRACT VISUALS SHOULD LOOK. Example: "Abstract geometric compositions in navy + one accent color. Never photography of people. Never 3D. Never gradient mesh. Think Stripe's illustration library, not Mailchimp's."]

## When I'm used for production design

- Use [framework — e.g. "React + Tailwind, Next.js 14, our component library at `@arcline/ui`"]
- Reference our tokens in [token source — e.g. "`packages/tokens/index.ts`" or "CSS variables defined in `globals.css`"]
- Before generating a prototype, check if an existing component in `@arcline/ui` already solves the problem. Reuse over re-create.
- Do not scope out-of-band things (like a marketing site) using our production component library — that uses a separate design system.

## When I'm used for production code

- All text needs to be localizable — wrap in `<Trans>` tags, keys in kebab-case.
- All interactive elements need a `data-testid` that matches the component name.
- Accessibility baseline is WCAG 2.1 AA. Color contrast, keyboard nav, focus states — non-negotiable.

## What we never do

- We do not use motion-heavy animations on our product. Subtle only.
- We do not use stock photography.
- We do not write copy that tries to sound clever. Clarity beats cleverness every time.
- We do not use dark mode on our marketing site.
```

---

## Part 4 — Use the Design System on every new prototype

1. Go back to **Prototype** and click **Create new project**.
2. In the dropdown, select the Design System you just created.
3. Every prototype built from here starts with your colors, fonts, component styles, and SKILL.md brand rules.

---

## Part 5 — The maintenance loop

The SKILL.md compounds. Every time Claude gets something subtly wrong in a generation (wrong icon set, wrong semantic color usage, wrong voice), do not correct it in Comments. Add a line to SKILL.md instead.

Example:
- First generation: Claude uses "Get Started" as a button label.
- Your brand never says "Get Started" — you say "Try it free."
- Don't fix it in Comments. Add one line to SKILL.md under "How we sound": *"Our CTA vocabulary: 'Try it free', 'Book a demo', 'See pricing'. Never 'Get Started', never 'Learn more'."*
- Every future generation gets it right on the first try.

Your SKILL.md gets better every week. By month 3, your Claude Design output is more on-brand than your first generations with any other tool.

---

## The order that matters

Do NOT build prototypes first and try to retrofit a design system. The strict design-system-first approach also reduces output quality on the first pass — see `06_pm_tips.md` point 4.

The correct sequence:
1. Set up the Design System (this file).
2. Build your first prototype **free-form** without forcing the Design System.
3. Apply the Design System in a *second* prompt: `"Apply our design system. Use [hex] for primary, [font] for headings, [radius] for cards. Remove any gradients not in our palette."`

Free-form first. System second. This is the correct order.

---

## Honest cost

Design System generation costs ~$2-3 in tokens. Validation is free (no tokens burned clicking toggles). SKILL.md iteration is free. Every future prototype saves ~5 minutes of cleanup that would otherwise happen in Tweaks + Edit. Payback on the first prototype.
