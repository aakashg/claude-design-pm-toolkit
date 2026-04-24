# Claude Design PM Prompt Toolkit

**The prompts, references, and fix-it guides for every PM use case in [The PM's Complete Guide to Claude Design](https://www.news.aakashg.com).**

Built to take you from "I heard about Claude Design" to "I just shipped a prototype my VP asked for" in about 12 minutes. Every file in this repo is copy-paste ready. Customize 2–4 lines. Done.

---

## Who this is for

- **Product managers** shipping prototypes, launch pages, board decks, and stakeholder reviews without a dedicated design team.
- **Solo founders and PMMs** who need something that looks like a design team built it, today.
- **Heads of product** evaluating how far AI-native design actually goes before you commit your team.

**Who this is NOT for:** designers doing precision work in Figma. Claude Design is a first-draft tool. This toolkit is for the draft.

---

## Start here

1. **If you are brand new to Claude Design:** read the article first → [The PM's Complete Guide to Claude Design](https://www.news.aakashg.com).
2. **If you want every prototype to look like your product:** do [`09_design_system_setup.md`](./09_design_system_setup.md) once. Costs an hour. Pays back on every future generation.
3. **If you need to ship something today:** jump to the quickstart table below.

---

## Quickstart by use case

| Your task today | File | Time |
|---|---|---|
| Board update / pitch deck | [`07_pitch_deck.md`](./07_pitch_deck.md) | ~8 min |
| Feature flow for engineering handoff | [`03_feature_flow.md`](./03_feature_flow.md) | ~12 min |
| Investor demo / Series A website | [`01_investor_demo.md`](./01_investor_demo.md) | ~8 min |
| Product launch / waitlist page | [`02_product_launch.md`](./02_product_launch.md) | ~6 min |
| Product Hunt / cinematic showcase | [`04_animated_showcase.md`](./04_animated_showcase.md) | ~45 min |
| Stakeholder review prototype | [`08_stakeholder_prototype.md`](./08_stakeholder_prototype.md) | ~10 min |
| Admin tool / ops dashboard | [`13_internal_tool.md`](./13_internal_tool.md) | ~15 min |

---

## What is in this toolkit

### The prompts (copy-paste, customize 2–4 lines)

| File | What it is |
|---|---|
| [`01_investor_demo.md`](./01_investor_demo.md) | Dark premium investor demo page. Liquid glass, animated metrics, before/after. |
| [`02_product_launch.md`](./02_product_launch.md) | Clean SaaS launch page. Email capture, feature grid, social proof. |
| [`03_feature_flow.md`](./03_feature_flow.md) | 4-screen interactive prototype. Clickable flow, Claude Code handoff ready. |
| [`04_animated_showcase.md`](./04_animated_showcase.md) | Cinematic video background showcase. Liquid glass, word-by-word blur. |
| [`07_pitch_deck.md`](./07_pitch_deck.md) | Board update / quarterly deck. 14 slides with speaker notes, exports to PPTX. |
| [`08_stakeholder_prototype.md`](./08_stakeholder_prototype.md) | Review-ready clickable prototype. Real sample data, step indicator, comment-ready. |
| [`13_internal_tool.md`](./13_internal_tool.md) | Admin / ops / operator dashboard. Dense, keyboard-first, zero marketing copy. |

### The references (read once, reuse forever)

| File | What it is |
|---|---|
| [`05_design_system.md`](./05_design_system.md) | Liquid glass CSS, typography system, all @keyframes, color tokens. |
| [`06_pm_tips.md`](./06_pm_tips.md) | Six things learned from testing: screenshot technique, token budget, hero-first. |
| [`09_design_system_setup.md`](./09_design_system_setup.md) | Set up your Design System in Claude Design + SKILL.md template. |
| [`10_clarifying_questions.md`](./10_clarifying_questions.md) | What to answer for every clarifying question Claude asks. The highest-leverage 90 seconds of any session. |
| [`11_claude_code_handoff.md`](./11_claude_code_handoff.md) | README template for Claude Code handoff. Cuts engineering implementation time in half. |
| [`12_error_recovery.md`](./12_error_recovery.md) | 12 common failures + copy-paste fix prompts. |
| [`CHEATSHEET.md`](./CHEATSHEET.md) | Printable 1-pager. Tape above your monitor. |

---

## How to use

1. Open Claude Design at [claude.ai/design](https://claude.ai/design)
2. Pick the right tab (Prototype for flows, Slide deck for decks, etc.)
3. Select your Design System from the dropdown (if you have one — see `09_design_system_setup.md`)
4. Copy the prompt from the file matching your use case
5. Fill in the bracketed slots
6. Paste into Claude Design, hit Send
7. **Answer the clarifying questions deliberately** — see `10_clarifying_questions.md`

The output after thoughtful clarifying answers is significantly better than a cold prompt.

---

## The article → toolkit map

If you are reading the article, here is where each section lives in this repo:

| Article section | Toolkit file |
|---|---|
| §2.1 Feature Flow Wireframe | `03_feature_flow.md` |
| §2.2 Pitch Deck / Board Update | `07_pitch_deck.md` |
| §2.3 Product Launch / Feature Announcement | `02_product_launch.md` + `04_animated_showcase.md` |
| §2.4 Stakeholder Review Prototype | `08_stakeholder_prototype.md` |
| §3 The Workflow: How the Loop Works | `CHEATSHEET.md` |
| §4 Five Skills That Separate the PMs Who Get Value | `06_pm_tips.md` |
| §5 Where Claude Design Fits vs. Figma, v0, Stitch | `CHEATSHEET.md` |
| §7 How to Set Up Your Design System | `09_design_system_setup.md` |
| §8 The PM Prompt Toolkit | every prompt file in this repo |

---

## The video workflow (for `04_animated_showcase.md`)

Before using Prompt 4, you need a hero video URL:

1. Generate a looping video with [Kling 3.0](https://klingai.com) or Sedance 2.0. Prompt: `looping animation no camera movement no extra elements to be added no zoom in or zoom out looping animation`. Keep under 8 seconds.
2. Upload to [Mux.com](https://mux.com) (free tier) or Cloudflare Stream.
3. Get the live URL.
4. Paste it where the prompt says `[YOUR HERO VIDEO URL]`.

Full details in `06_pm_tips.md`.

---

## Honest costs

A fully built hi-fi page with refinements runs ~$2–7 in Claude tokens. A 10–14 slide deck runs ~$2–5. Heavy sessions with multiple refinement rounds can burn 95% of a weekly Pro quota. **Enable Team / Enterprise overage or upgrade to Max before your first serious build.** See `06_pm_tips.md` point 6 for the full breakdown.

The comparison is not "is this cheaper than free." It is "is this cheaper than a designer's time." The answer is yes by a significant margin.

---

## Contributing and sharing

If you build something great with these prompts, share it. Tag [@aakashg0](https://x.com/aakashg0) on X.

If you want to improve a prompt — open a PR. The most useful additions right now:

- A retail / e-commerce landing variant
- A consumer / mobile-first prototype variant
- A voice-first / conversational prototype variant
- Localized brand personality examples for non-US PMs

---

## License

MIT. See [`LICENSE`](./LICENSE). Use these prompts in client work, internal tools, or your own newsletter — no attribution required but always appreciated.

---

## From the Product Growth newsletter

This toolkit accompanies the Claude Design deep dive in [Product Growth by Aakash Gupta](https://www.news.aakashg.com). Subscribe for weekly PM deep dives.
