# Claude Design PM Prompt Toolkit
## Reference: The Claude Code Handoff README Template

When you hit **Share → Handoff to Claude Code** in Claude Design, it generates a handoff bundle: the design files + a README that tells the coding agent exactly how to match your output in your stack.

The default README is serviceable. A hand-crafted one is the difference between "engineering ships it this week" and "engineering throws it out and rewrites from scratch."

Copy this template. Edit the brackets. Drop it into the handoff bundle.

---

## The template

```markdown
# [FEATURE NAME] — Claude Code Handoff

This bundle contains the Claude Design output for [FEATURE NAME]. The design intent, component choices, and interaction patterns are captured in the HTML/CSS output. Your job as Claude Code is to re-implement this in our production stack while preserving the design intent.

## What is in this bundle

- `design.html` — the Claude Design output, standalone HTML + inline CSS + JS
- `screenshots/` — PNG captures of each state for visual reference
- `design-notes.md` — PM-annotated notes on the design decisions
- This README

## Our production stack

- **Framework:** [e.g. Next.js 14 App Router, React 18, TypeScript strict]
- **Styling:** [e.g. Tailwind CSS v3.4, our custom plugin at `/plugins/tokens.ts`]
- **Component library:** [e.g. our internal `@acme/ui` at `/packages/ui`]
- **State:** [e.g. Zustand for local state, React Query for server state]
- **Routing:** [e.g. Next.js file-based routing]
- **Testing:** [e.g. Vitest for unit, Playwright for e2e — add tests for any new interactive elements]

## Design tokens source of truth

- Colors: `/packages/tokens/colors.ts`
- Typography: `/packages/tokens/typography.ts`
- Spacing: `/packages/tokens/spacing.ts`
- Do NOT hard-code hex codes from the design HTML. Map every color to a token. If the design uses a color that is not in our tokens, flag it in your PR — do not add it silently.

## Component reuse — check these first

Before building anything new, check if these already exist:
- Buttons: `@acme/ui/Button` (variants: primary, secondary, ghost)
- Cards: `@acme/ui/Card`
- Form inputs: `@acme/ui/Input`, `@acme/ui/Select`, `@acme/ui/Textarea`
- Modals: `@acme/ui/Dialog`
- [Add your own component library paths]

The design HTML uses inline Tailwind-like classes. Your job is to map those to our component props. Do not render the design 1:1 in raw HTML — compose from existing components.

## Data this feature needs

- API endpoints:
  - `POST /api/[resource]` — [brief description]
  - `GET /api/[resource]/:id` — [brief description]
- Data shapes: see `types/[resource].ts`
- Auth: the user must be authenticated; wrap the page in `<AuthGate>`

## Interactions to preserve

The design HTML has these interactions — re-implement them with equivalent behavior:
1. [Interaction 1 — e.g. "Hover on feature card: translateY(-4px) + shadow. Use our `hover:translate-y-[-4px]` utility."]
2. [Interaction 2 — e.g. "Form submit on 'Create role' button: optimistic update, then toast on success. Use our `toast.success()` pattern."]
3. [Interaction 3 — e.g. "Screen transitions: fade out + fade in. Use Framer Motion, match existing patterns at `/app/onboarding`."]

## Animations

The design uses these @keyframes (see `design.html`):
- [list them from the design HTML]

Do NOT re-implement as CSS @keyframes — we use Framer Motion for all animations. Convert each to a `<motion.div>` with matching timing:
- `duration` = Claude Design's animation duration
- `ease` = match Claude Design's easing curve
- Stagger = use `staggerChildren` on the parent

## Accessibility

- All interactive elements need visible focus states (our `focus-visible:ring-2` pattern).
- Color contrast: WCAG 2.1 AA minimum on all text. If the design uses white/55 or similar low-opacity text on dark backgrounds, increase to white/75 — we have failed Axe audits on this before.
- Keyboard navigation: Tab order must follow reading order. Every button reachable by keyboard. Enter submits primary CTA.
- Screen reader labels on all icons. No icon-only buttons without `aria-label`.

## Responsive behavior

- Breakpoints: sm 640, md 768, lg 1024, xl 1280, 2xl 1536
- Mobile-first: write mobile styles first, layer up.
- Specific mobile considerations for this feature:
  - [e.g. "On mobile, the 3-column feature grid stacks to 1 column. The hero headline caps at 48px."]
  - [e.g. "The stepper indicator collapses to a progress bar on mobile (we have `<Stepper mobile='bar'>` for this)."]

## What I do NOT want you to do

- Do not add a loading skeleton to the page shell — we have `<PageShell>` that handles this globally.
- Do not add your own analytics — our `useTrack` hook wraps every primary CTA automatically.
- Do not install new dependencies without asking — we have strict budget on bundle size.
- Do not change the design. If something looks wrong, flag it in your PR and ask. Design was approved by [DESIGNER / PM] on [DATE].

## Definition of done

- [ ] Renders at 375px, 768px, 1280px without horizontal scroll
- [ ] All interactions from the design work
- [ ] Axe accessibility scan passes with 0 violations
- [ ] Lighthouse performance score ≥ 90
- [ ] All new components have Storybook stories
- [ ] All new interactive elements have `data-testid` attributes
- [ ] PR includes before/after screenshots at all 3 breakpoints

## Questions to ask before coding

If any of the following are unclear from the design, stop and ask in the PR before implementing:
1. What happens on error state? (design shows success path only)
2. What is the empty state? (design shows populated state)
3. What is the loading state for [slow API call]?
4. Does this feature need analytics events I should wire up?
5. Is this shipping behind a feature flag? If so, which one?
```

---

## Why a hand-crafted README beats the default

The default Claude Code handoff README covers the obvious: "use React, match the design." A good handoff README captures the *context the coding agent cannot infer from the HTML*:

- Which existing components to reuse (saves 30% of the PR)
- Which tokens are the source of truth (prevents drift)
- Which interactions need special care (prevents regressions)
- What NOT to do (prevents scope creep)
- Definition of done (prevents endless PR cycles)

A PM who writes a good handoff README cuts engineering's implementation time roughly in half and gets their feature shipped the same week. A PM who ships the default README gets a PR on Friday with 40 comments and a rollback on Monday.

---

## Where this file fits in the workflow

1. Build prototype in Claude Design (Prompts 01–08 in this toolkit)
2. Refine with Tweaks → Edit → Comments
3. **Share → Handoff to Claude Code**
4. Before hitting "Send to Claude Code Web" — paste this template into the message box, fill in the brackets for your stack
5. Claude Code receives the bundle + your README, generates the PR

The handoff is the step where most PMs lose the output quality they just built. Do not skip it.
