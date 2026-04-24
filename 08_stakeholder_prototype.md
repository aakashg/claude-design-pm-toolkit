# Claude Design PM Prompt Toolkit
## Prompt 8: The Stakeholder Review Prototype

**Use case:** The review where VP Design, Head of Engineering, and the CEO all need to poke around the same flow at their own pace. Not a Figma file — stakeholders do not install Figma. A live URL they can click through, comment on, and send back with feedback.

**What you get:** Fully clickable prototype with real-looking sample data, step indicator, mobile-responsive, shareable link. ~10 minutes from prompt to URL.

**Why this is different from Prompt 3 (Feature Flow):**
- Prompt 3 is *exploratory*: you are figuring out the flow with your team.
- Prompt 8 is *decisional*: you have the flow, you need a yes/no.

Stakeholders disengage the moment they see placeholder text. This prompt forces real-looking data.

---

## The Prompt

```
Build an interactive prototype of [FLOW NAME] in [PRODUCT NAME] for stakeholder review.

REVIEWER: [WHO IS REVIEWING — e.g. "VP of Design, Head of Engineering, CEO"]. Note: they all review independently, then converge in a single 30-minute meeting. The prototype needs to communicate without me narrating it.

KEY DECISION THEY ARE REVIEWING: [WHAT SPECIFIC FEEDBACK YOU NEED — e.g. "Is the new onboarding 2-step flow clearer than the current 4-step? Specifically, does the 'Paste job description' step feel like enough input, or does it need a second field?"]

CONTEXT THEY NEED:
- Product: [WHAT YOUR PRODUCT DOES — 1 sentence]
- User: [WHO USES THIS — persona or job title]
- Current state: [WHAT EXISTS TODAY — 1 sentence, the thing we are replacing]
- Proposed state: [WHAT THIS PROTOTYPE SHOWS — 1-2 sentences]

SCREENS (3-5 max — more than that and stakeholders bounce):
- Screen 1: [SCREEN NAME + ONE-LINE OF WHAT IT DOES]
- Screen 2: [SCREEN NAME + ONE-LINE OF WHAT IT DOES]
- Screen 3: [SCREEN NAME + ONE-LINE OF WHAT IT DOES]
- (Optional) Screen 4: ...
- (Optional) Screen 5: ...

HARD REQUIREMENTS — do not skip any of these:

1. FULLY CLICKABLE
   Every primary CTA advances to the next screen. Every "Back" returns. Every secondary link at least shows a hover state. No dead buttons.

2. REAL-LOOKING SAMPLE DATA
   No "Lorem ipsum". No "Jane Doe". No "$XX.XX". Use plausible names (mix of cultures), realistic numbers (e.g. "87%", "$4,240", "23 candidates"), actual UI copy for the domain. If you do not know the domain copy, match the style of competitor products — not a generic SaaS template.

3. STEP INDICATOR ON EVERY SCREEN
   Small pill or dot row top-center, showing "Step 2 of 4" equivalent. Stakeholders need to know where they are without scrolling. Use the brand accent color for the active step.

4. REVIEWER HINTS (subtle, dismissable)
   On each screen, a small "i" icon in the top-right corner. Click it: reveals a 2-line caption explaining what to look for on this screen — e.g. "Note: this screen replaces the existing 4-step setup. Watch for: does the AI parse button feel like it is doing something?" These hints are optional for the reviewer but they remove my need to narrate a Loom.

5. COMMENT-READY
   Every major UI element has a data-element="..." attribute so reviewers can reference them ("the parse button on screen 2"). Include a short "How to leave feedback" banner on screen 1 only — "Click the link-sharing comment feature to leave feedback on any element."

6. MOBILE RESPONSIVE
   The prototype must work down to 375px. Many stakeholders will open the link on their phone first. Test mentally at 375px before generating.

7. NO CHROME / NO BROWSER FRAME
   Do not add a fake browser URL bar or macOS chrome — distracts from the content.

DESIGN DIRECTION:
Use our Design System (attached). Match component styles exactly — this is for internal review, consistency beats creativity. If no Design System is attached, default to:
- Clean SaaS aesthetic: white background, #0D1B2A primary, rounded-xl cards
- Readex Pro typography
- Subtle animation only — fade-up on screen enter (0.3s), no motion-heavy effects

NOT NEEDED:
- No marketing hero
- No "Trusted by" bar
- No animated video backgrounds
- No founder/team section
- No footer with 47 links
This is a product review artifact, not a landing page. Keep the surface area tight.

OUTPUT: Interactive prototype, single shareable URL via Share → Copy link. Include in the output README: a 3-line "What to review" note I can paste into my Slack message when I send the link.
```

---

## The Slack message template to send with the link

After generating, paste this into your Slack DM or channel message alongside the prototype URL:

```
Hi [REVIEWER],

Prototype link for [FLOW NAME]: [CLAUDE DESIGN URL]

The specific decision I need from you: [1 SENTENCE]

Takes ~3 minutes to click through. Leave feedback as comments directly in the prototype — no account needed. Would love your take by [DEADLINE].
```

Three lines. No Loom, no "please review." Stakeholders open the link because the ask is scoped.

---

## What to put in each slot

| Slot | Example |
|---|---|
| Flow name | Mobile onboarding redesign |
| Product name | Arcline |
| Reviewer | VP Design (Mira), Head of Eng (Karthik), CEO (Elena) |
| Key decision | Is the 2-step flow clearer than our current 4-step? Specifically: does "Paste job description" feel like enough input, or should it be split into role + JD? |
| Current state | 4-step signup: role type → details → JD → team invite. ~23% activation at 7 days. |
| Proposed state | 2-step signup: paste JD → confirm extracted role. AI pre-fills everything else. Optional team invite moves to post-activation. |
| Screen 1 | Landing — "Paste a job description" large textarea, one primary CTA |
| Screen 2 | Extracted role confirmation — editable tags, scoring preview |
| Screen 3 | Dashboard first-visit — empty state with 3 candidate slots |

---

## The three things that will always go wrong on the first generation

1. **Sample data is too generic.** "Software Engineer" "Marketing Manager" "Sales Rep" — replace with actual role titles from your customer base (e.g. "Senior Product Designer — Series B fintech, Berlin").

2. **The comment banner is too prominent.** First-generation puts a huge callout at the top. Use Edit to resize it down to a 32px-height pill in the corner.

3. **Step indicator shows "4 of 4" on the success screen.** First-generation keeps incrementing. Use Comments (this is a structural fix) to say "On screen 4, show a checkmark instead of the step indicator — the flow is complete, not mid-step."

---

## Why stakeholders respond better to this format

The Figma link requires an account, a download, zooming around a canvas, and interpreting arrows. This requires 1 click and mimics using the actual product. VP Design specifically will take you more seriously if you send this instead of a Figma frame — it signals you thought about the review experience, not just the design.
