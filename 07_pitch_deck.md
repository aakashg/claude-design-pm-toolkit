# Claude Design PM Prompt Toolkit
## Prompt 7: The Pitch Deck / Board Update

**Use case:** Board updates, quarterly reviews, Series A decks, all-hands roadmap reads. Claude Design's **Slide deck** tab generates a fully editable deck with speaker notes — exportable to PPTX and Canva.

**What you get:** 10–14 slide deck. On-brand covers, data charts, roadmap timelines, a What-Worked / What-Did-Not table, and speaker notes on every slide. Roughly 8 minutes from prompt to PPTX.

**Before you start — setup that saves an hour of cleanup:**

1. **Open the Slide deck tab** (not Prototype). `claude.ai/design` → Slide deck.
2. **Pick your Design System** from the dropdown. If you have not created one yet, see `09_design_system_setup.md` — spend the 20 minutes there first. A board deck that looks like your company vs. a Claude default is the difference between useful and forgettable.
3. **Toggle "Use speaker notes / Less text on slides" ON** if you will present live. OFF if the deck will be read async. Most PMs never see this toggle and wonder why their slides are either too dense or too sparse. Pick deliberately.
4. **Do not ask for speaker notes in the prompt** if the toggle is on — Claude generates them automatically. Asking twice creates duplicates.

**Customize 5 things:**
- `[COMPANY NAME]` and `[QUARTER]` — appear on the cover and divider slides
- `[NORTH STAR METRIC]` + the actual number + target
- Three **What Worked** launches with a one-line outcome each
- Two **What Did Not Work** items with a one-line root cause each
- Next-quarter bets (3 items, one line each)

---

## The Prompt

```
Build a [QUARTER] board update deck for [COMPANY NAME], a [ONE-LINE DESCRIPTION OF WHAT YOU DO].

AUDIENCE: Board of directors. They have read the memo. This deck is for the meeting — it reinforces the 3 takeaways and walks through the charts. Ruthless density. No filler slides.

TONE: Direct, confident, numeric. No hedging language. No "we believe" — use "we shipped", "we learned", "we will".

DECK STRUCTURE (14 slides max, feel free to collapse if any slide is weak):

1. COVER
   [COMPANY NAME] · [QUARTER] Board Update · Date. Minimal. Logo top-left. Name of presenter bottom.

2. THE THREE TAKEAWAYS
   Large Instrument Serif italic heading "Three things to know." Then a 3-row layout: each row has a number (01/02/03 in a muted color), a one-sentence claim, and a single supporting stat. This is the TL;DR slide — board members who check out after this should still know the punchline.

3. NORTH STAR
   Full-bleed chart. [NORTH STAR METRIC] over the last 4 quarters, target line overlaid. Current value large top-left, delta vs. last quarter ("+13pts", "-2%") in a colored pill. Single sentence caption bottom: what is driving the number.

4. NORTH STAR DRIVERS
   2x2 grid of small metric cards. Each card: metric name, current value, 4-week sparkline, delta. Pick the 4 metrics that explain movement in the North Star.

5. WHAT WORKED (shipped this quarter)
   "What worked" heading left. Right side: 3 shipped launches in a stacked list. Each: launch name (Instrument Serif italic), ship date, one-line outcome with a specific number (e.g. "+13pts D7 retention on mobile onboarding"). Use green accents sparingly.

6. SHIPPED THIS QUARTER — HONESTY SLIDE
   Two columns. Left column "Worked" — 3 items with specific outcomes. Right column "Did not work" — 2 items with one-line root cause and "Fix in [version/date]". Same visual weight. Do not hide the misses.

7. PRODUCT DEEP DIVE #1
   The biggest launch. 60/40 split: left is a screenshot of the product. Right is a 3-bullet "why it mattered / what it proved / what comes next". Chart inset bottom-right if there is a before/after.

8. PRODUCT DEEP DIVE #2
   Same structure as slide 7 for the second most important launch.

9. COMPETITIVE LANDSCAPE
   3-column table. Columns: us, competitor 1, competitor 2. Rows: 4 dimensions that matter to the board (customer segment, primary wedge, pricing, moat). One sentence per cell. No marketing language.

10. FINANCIALS SNAPSHOT
    ARR / revenue chart. Burn rate number. Runway in months. Hiring plan in one row of pills. Assume board reads the financial memo — this is a quick reinforcement, not a deep dive.

11. NEXT QUARTER BETS
    3 big bets in a horizontal row. Each: bet name (Instrument Serif italic), 2-line hypothesis, success metric. Color the "bet we are most confident in" with a subtle accent border — boards like seeing the PM make a call.

12. RISKS
    Title "What could go wrong." 3-row list. Each row: risk name, likelihood (low/med/high as a pill), mitigation in one sentence. The risk slide earns trust faster than any other — do not skip it.

13. ASKS
    "What we need from you." 2-3 specific asks. Each is an action the board can take: an intro, a decision, a hire approval. Do not put "support" on this slide. Put verbs.

14. APPENDIX COVER
    Blank cover "Appendix" — then any supporting detail slides the PM wants to have ready but not show by default (detailed cohort curves, churn breakdown, hiring funnel, anything the board might ask about).

VISUAL DIRECTION:
- Use our brand colors from the attached Design System. Do not introduce new colors for charts — stick to the palette.
- Typography: Instrument Serif italic for slide titles (36–52pt). Body in Readex Pro or Barlow 400, 14–16pt. Labels in 11pt uppercase tracked-wide.
- Charts: minimal, no 3D, no drop shadows. Use the brand accent for the current period, neutral gray for historical periods.
- Every stat on every slide has a caption explaining what it is measuring. No bare numbers.
- Include real-looking sample data — do not use "Lorem ipsum" placeholders or "$XX.X M". If I have not given you the number, use a plausible one and flag it in the speaker notes as "[confirm]".

SPEAKER NOTES (if the toggle is on):
- 3-5 sentences per slide
- Lead with the one-line claim
- Then the supporting context the board needs
- End with the transition to the next slide ("Which brings us to…")

OUTPUT: Editable deck, exportable to PPTX and Canva. Use the Design System dropdown selection for all styling.
```

---

## What to put in each slot

| Slot | Example |
|---|---|
| Company name | Arcline |
| Quarter | Q1 2026 |
| North star metric | Weekly active workspaces |
| What worked #1 | AI Search shipped March 12, +13pts D7 retention on mobile onboarding |
| What worked #2 | Bulk Export, March 20, 28% of Enterprise tenants adopted in 2 weeks |
| What did not work #1 | AI Search adoption 12% vs 35% target — root cause: discovery placement. Fix in v1.2, ships May 1 |
| Next quarter bet #1 | Activation rewrite — hypothesis: 7-day activation improves from 23% → 35% if we cut onboarding from 4 steps to 2 |

---

## After the first generation — the 3 fixes that always need to happen

1. **Kill the filler slides.** Claude often adds an "Agenda" slide and a "Thank you" slide. Delete both. Boards do not need an agenda slide for a 14-slide deck, and the ask slide is a better closer than thanks.

2. **Rewrite the takeaways.** The 3-takeaways slide is the most important slide in the deck. Claude's first draft will be generic. Rewrite each line yourself — this is the one slide where PM judgment beats LLM speed.

3. **Number-check every chart.** Claude fills in plausible numbers. Every chart with a hard number needs to be corrected against your actual data before the deck ships. Use Edit (not Comments) to swap the numbers — zero token cost, 30 seconds per chart.

---

## Export paths

- **Share → Export as PPTX** — download for PowerPoint or Keynote. Retains animations.
- **Share → Send to Canva** — fully editable by your team, good if someone other than you is finalizing.
- **Share → Copy link** — for async board review. Stakeholders can leave comments inline.

---

## Honest cost

A 14-slide deck with 2 refinement rounds runs ~$4–7 in Claude tokens. Compare to the cost of a deck designer (~$400–800 turnaround). This is the easiest ROI use case in the toolkit.
