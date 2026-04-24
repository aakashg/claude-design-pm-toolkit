# Claude Design — PM Cheat Sheet

**Print this. Tape it above your monitor.**

---

## The 4 Surfaces

| Tab | Use for |
|---|---|
| **Prototype** | Feature flows, onboarding screens, stakeholder review, landing pages |
| **Slide deck** | Board updates, investor decks, product reviews, quarterly roadmaps |
| **From template** | Animation (timeline-based motion). Save any project as a template here |
| **Other** | One-pagers, marketing assets, anything that does not fit the first two |

**Default: Prototype. Mode: High Fidelity.** Skip Wireframe — it rarely saves time.

---

## Before You Type a Prompt

Attach context. You get 4 options. Use **at least 2 every session**:

1. **Design System** — from your Figma or GitHub repo. Keeps outputs on-brand.
2. **Screenshot** — a Dribbble / Higgsfield / Pinterest layout reference.
3. **Codebase** — GitHub URL for your frontend subfolder.
4. **Figma file** — your existing design assets.

---

## The Workflow Loop

```
Idea → prompt → prototype → refine (Tweaks / Edit / Comments) → Claude Code handoff → production
```

**Old model:** Idea → PRD → design queue → Figma review → engineering sprint. 2 weeks.
**New model:** Idea → prototype in 12 minutes.

---

## Tool Use in the Right Order

| Tool | What it costs | Use for |
|---|---|---|
| **Tweaks** | Free | Global color, illustration style, background tone. Resets everything at once. |
| **Edit** | Free | Anything you can click on directly. Text, colors, specific elements. |
| **Comments** | Costs tokens | Structural changes only: layouts, missing steps, section rebuilds. |

**Rule: Tweaks first. Edit second. Comments last.**

Using Comments when Edit would work = burning tokens unnecessarily. One of the top ways PMs hit their weekly quota mid-session.

---

## The 5 Skills That Separate PMs Who Compound

1. **Use screenshots, not descriptions.** Strip text with Nano Banana 2, upload clean image.
2. **Know your prompt resources.** motionsites.ai for interactions, Dribbble / Pinterest for layouts.
3. **Right modality, right order.** Tweaks → Edit → Comments. Every session.
4. **Know your 80% ceiling.** Self-serve: wireframes, pitches, feature flows, first drafts. Hand off: brand-defining surfaces, custom illustration, complex motion.
5. **Taste at speed.** Generate 5 directions in 20 minutes. Kill 4. Build judgment through reps.

---

## Where It Fits vs. Other Tools

| Tool | Fits best for |
|---|---|
| **Figma** | Precision work. Component systems. Final review. Where things finish. |
| **v0** | Ship React to production today. When you know what component you want. |
| **Google Stitch** | One-shot generation. Not back-and-forth refinement. |
| **Claude Design** | First draft, back-and-forth refinement, handoff with design intent intact. **Where things start.** |

---

## Export Paths

| Export | Use when |
|---|---|
| **Share → Copy link** | Stakeholder async review. No account needed on their end. |
| **Share → Export as PDF** | Read-only archive, shareable via email. |
| **Share → Export as PPTX** | Slide deck that will be edited in PowerPoint. |
| **Share → Send to Canva** | Deck that will be finalized by your team. |
| **Share → Export as standalone HTML** | Live shareable URL for a prototype. |
| **Share → Handoff to Claude Code** | Engineering is ready to build — pass through Claude Code with the handoff README. |

---

## Token Budget — Plan Before You Start

- **Hi-fi page:** ~$2–7 in tokens
- **10-slide deck:** ~$2–5 in tokens
- **Full prototype with 3 refinement rounds:** ~$10–20 in tokens
- **One heavy session:** can burn 95% of a weekly Pro quota

**Upgrade to Max or enable Team/Enterprise overage before your first serious session.** Find this out up front, not mid-build.

---

## The 3 Honest Things About Claude Design

1. **Tokens hit faster than you expect.** Plan the budget.
2. **This is the first iteration.** What looks magical today will look primitive in 18 months. Get in early.
3. **Claude Design is a first-draft tool. Figma is still the finish line.** Use Claude for ideation and drafts, finish in Figma when precision matters.

---

## Quickstart by Use Case

| Your task | Start with |
|---|---|
| "I need a pitch for the board on Monday" | `07_pitch_deck.md` |
| "I have an idea and want to see if it works as a flow" | `03_feature_flow.md` |
| "Engineering wants a spec to build from" | `03_feature_flow.md` + `11_claude_code_handoff.md` |
| "I need a launch page for Tuesday" | `02_product_launch.md` |
| "I need to show an investor what this will look like" | `01_investor_demo.md` |
| "Product Hunt launch with a cinematic hero" | `04_animated_showcase.md` |
| "Stakeholders need to click through and give feedback" | `08_stakeholder_prototype.md` |
| "I have an admin tool / ops console to design" | `13_internal_tool.md` |
| "I want every prototype to look like my actual product" | `09_design_system_setup.md` (start here, once) |

---

## When Something Goes Wrong

See `12_error_recovery.md` for 12 common failures and their fix prompts.

**The meta-rule:** if you have made 3+ Comments that did not stick, duplicate the project (`Share → Duplicate project`) and re-prompt from scratch. Fighting a stuck session is the #1 way to burn your weekly quota. Duplicate early.

---

*Toolkit: [github.com/aakashg/claude-design-pm-toolkit](https://github.com/aakashg/claude-design-pm-toolkit) · Newsletter: [news.aakashg.com](https://www.news.aakashg.com)*
