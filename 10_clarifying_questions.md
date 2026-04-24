# Claude Design PM Prompt Toolkit
## Reference: Clarifying Questions Cheat Sheet

Claude Design does not build immediately. It asks 5–9 clarifying questions first. **This is where 70% of the output quality is set.** A bad answer here cannot be undone in Tweaks or Edit — it shapes the entire generation.

This file is the cheat sheet for what to answer. Every question Claude commonly asks is below, with the right answer and the wrong answer.

---

## Question 1 — Persona / Audience

**Claude asks:** *"Who is the primary user of this flow / page?"*

**Wrong answer:** "Product managers" / "Founders" / "Anyone who needs onboarding"

**Right answer:** Be specific about the *moment* they are in.
- "Hiring managers at Series B-D fintech, evaluating the product on a Tuesday afternoon between candidate calls. They have 4 minutes."
- "Solo founders who just shipped their MVP and have not done a product launch before. They are panicking 12 hours before Product Hunt."

The persona controls tone, density, what gets explained vs. assumed, what CTA copy reads like. A vague persona produces a generic output. A specific persona produces something a real human would actually use.

---

## Question 2 — Flow Length / Page Density

**Claude asks:** *"How long should this flow be?"* or *"How many sections should the page have?"*

**Wrong answer:** "Standard length"

**Right answer:** Bound it by the user's attention.
- For prototypes: "3–5 screens max. Anything longer and stakeholders bounce."
- For landing pages: "5 sections: hero, social proof, 3 features, before/after, email CTA. No founder section, no FAQ, no blog teaser."
- For decks: "12 slides. I will trim if any are weak."

If you do not bound it, Claude will give you 8 screens or 14 sections. The first generation always over-includes.

---

## Question 3 — Most Critical Moments

**Claude asks:** *"Which moments in the flow matter most?"*

**Wrong answer:** "All of them are important"

**Right answer:** Name 1–2 specific moments and explain why.
- "Screen 2 (paste job description) is the moment of truth — the user decides if our AI is real or not based on what comes back. The 'Parse with AI' button needs to feel substantial — loading state, real animation."
- "The hero CTA is the conversion moment. The headline carries 80% of the weight. Spend the visual budget there."

Claude allocates token spend based on what you say matters. If everything is important, nothing is.

---

## Question 4 — Visual Direction

**Claude asks:** *"What visual direction should I take?"*

**Wrong answer:** "By-the-book SaaS" (the default — produces a generic Vercel clone)

**Right answer:** Pick a *distinct* aesthetic. Reference real products, not categories.
- "Distinctive — feels like Linear's homepage merged with the editorial style of The Browser Company. Dark, premium, lots of negative space."
- "Distinctive — feels like Substack's reader, soft warm tones, generous serifs, conversational."
- "By-the-book SaaS only if you have a strong brand and want consistency over distinctiveness — which is not most prototypes."

> The PMs who pick "By-the-book SaaS" out of habit wonder why every prototype looks the same. The PMs who pick "Distinctive" and reference 2-3 real products get something that feels intentional.

---

## Question 5 — How Adventurous

**Claude asks:** *"How adventurous should I be with the design?"*

**Wrong answer:** "Safe / Conservative" (default for risk-averse PMs — produces forgettable output)

**Right answer:**
- For internal review prototypes: "Standard. Match our existing patterns."
- For investor demos and external launches: "Adventurous. Use unusual layouts, expressive typography, motion. We want this to be screenshotted and shared."
- For first drafts you will iterate on: **always pick adventurous.** You can always pull it back in Tweaks. You cannot push it forward without burning tokens.

---

## Question 6 — Brand Personality

**Claude asks:** *"Describe your brand personality in 3-5 words."*

**Wrong answer:** "Professional, modern, trustworthy" (every brand says this — Claude defaults to corporate)

**Right answer:** Adjectives that imply opposites.
- "Direct, technical, irreverent" (implies: NOT polite-corporate)
- "Warm, opinionated, hand-crafted" (implies: NOT slick-AI-generated)
- "Confident, plain-spoken, allergic to buzzwords" (implies: NOT aspirational)

The shape of the words you choose tells Claude what voice to use in copy. "Trustworthy" gives you generic SaaS copy. "Allergic to buzzwords" gives you copy that strips out filler.

---

## Question 7 — Copy Style / Tone

**Claude asks:** *"How should the copy read?"*

**Wrong answer:** "Clear and concise"

**Right answer:** Reference a writer or a publication.
- "Like Stripe's homepage — short sentences, declarative, never marketing fluff."
- "Like Patrick Collison's tweets — direct, slightly skeptical, technical when it needs to be."
- "Like Nilay Patel writing for The Verge — opinionated, specific, treats the reader like they are smart."

Claude knows these voices. Be specific.

---

## Question 8 — Inspirations / References

**Claude asks:** *"Any visual references or inspirations?"*

**Wrong answer:** "Notion / Linear / Stripe" (everyone says this — produces a blend that feels like nothing)

**Right answer:** 2-3 specific references with what you want from each.
- "Layout from Linear's homepage. Color treatment from Vercel's docs. Typography from Stripe Sessions 2024."
- "Hero from the Cron landing page (the bold serif). Card hover from Mercury. Spacing from Notion's pricing page."

The combination is what makes the output feel original.

---

## Question 9 — What to Avoid

**Claude asks:** *"Anything I should NOT do?"*

**Wrong answer:** Skipping this question (most PMs skip it)

**Right answer:** Be explicit about your aesthetic taboos.
- "No gradients. No drop shadows. No emoji in UI. No 'Get Started' as a CTA."
- "No stock photography of people. No 3D illustrations. No purple."
- "Do not use the word 'powerful' anywhere on the page."

This question prevents the most common revision cycles.

---

## The 30-second answer template

If Claude is waiting and you have 30 seconds, paste this and edit the brackets:

```
Persona: [SPECIFIC USER + SPECIFIC MOMENT — 1 sentence]
Length: [BOUND IT — "3 screens max" / "5 sections, no FAQ"]
Most critical: [1-2 SPECIFIC MOMENTS + WHY]
Visual direction: Distinctive
How adventurous: Adventurous
Brand personality: [3 ADJECTIVES, AT LEAST ONE IMPLIES OPPOSITES]
Copy style: Like [REFERENCE WRITER OR SITE]
Inspirations: Layout from [X], color from [Y], typography from [Z]
Do not: [3 EXPLICIT TABOOS]
```

This template alone moves your output quality from 60% to 85% on the first generation.

---

## What changes when you answer well

- **Less Tweaks needed** — your colors and typography land closer to your brand on first try.
- **Less Edits needed** — copy lands in your voice, not generic.
- **No structural Comments needed** — the layout matches your intent because you bounded it.
- **Token spend drops by ~40%** because you avoid the back-and-forth refinement cycle.

The clarifying questions are the highest-leverage 90 seconds of any Claude Design session. Spend them.
