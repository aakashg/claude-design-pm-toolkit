# Claude Design PM Prompt Toolkit
## Prompt 15: The Research / Unmoderated Usability Test Prototype

**Use case:** Unmoderated usability tests (Maze, UserTesting, Lyssna, in-house). Solo research where you give a participant a task list, watch them complete it (or not), and read the recording afterward. The prototype needs task framing, completion tracking, and an exit survey baked in.

**Why it is different from Prompt 8 (stakeholder review):**
- Prompt 8 = stakeholders giving you a yes/no decision on a flow.
- Prompt 15 = real users completing tasks while you watch from a distance.

This means: clear task framing on entry, no "click to advance" cheats, success-state tracking, an exit survey, and zero PM hand-holding inside the prototype itself.

---

## The Prompt

```
Build an unmoderated usability test prototype for [FEATURE NAME] in [PRODUCT NAME].

CONTEXT FOR THIS RESEARCH:
- Research question: [WHAT YOU WANT TO LEARN — e.g. "Can a first-time user create their first role within 3 minutes without help?"]
- Test platform: [WHERE — e.g. Maze, UserTesting, Lyssna, or self-hosted with screen recording]
- Participants: [WHO — e.g. "5 hiring managers, 3-7 years of recruiting experience, never used our product"]
- Tasks they will attempt: [3-5 SPECIFIC TASKS — see structure below]

TASK STRUCTURE: Each task is a one-sentence instruction the participant reads before they start. Tasks should be outcome-framed ("Create a role for a Senior Engineer in Marketing") not click-framed ("Click the Create Role button"). The prototype must support each task end-to-end without the participant needing to ask for help.

EXAMPLE TASKS for the [FEATURE NAME] flow:
1. [TASK 1 — outcome-framed sentence]
2. [TASK 2 — outcome-framed sentence]
3. [TASK 3 — outcome-framed sentence]

PROTOTYPE STRUCTURE:

SCREEN 0 — Welcome / Task Briefing
Single screen, before the prototype starts.
- Heading: "Welcome — thanks for participating."
- Below: a 3-line context paragraph explaining what the product is and what you will be doing today (no marketing fluff — it is research, not a pitch).
- Then: "You will complete [N] tasks. Take your time. Think out loud if your platform supports recording."
- Then: a numbered list of all tasks (1-5), each on its own line with a small circle bullet that fills in as the participant completes that task. The list stays visible throughout the test as a sidebar — see below.
- CTA: "Start the test" — primary, large.

THE PROTOTYPE ITSELF (whatever screens are needed for the actual tasks):
- The product flow as it would appear in production.
- NO additional reviewer hints, NO instructions, NO arrows pointing at things. The point is to see if a real user can find what they need without help.
- Every interactive element works. Nothing is "smoke and mirrors" beyond what is essential to the flow.
- Realistic-but-fake sample data populated throughout.

PERSISTENT TASK SIDEBAR:
- Right side of screen on desktop, collapsible. On mobile: collapses to a small "Tasks (1/3)" pill in the top-right that expands to a sheet on tap.
- Shows the current task highlighted, completed tasks with a checkmark, upcoming tasks dim.
- Includes a small "I am stuck — skip this task" link below the current task. Important: real research lets people give up. Without a skip option, you get false-positive completions.

COMPLETION DETECTION:
- Each task has an implicit completion state in the prototype (e.g. "task 1 complete when the user reaches Screen 4 with a non-empty role title"). Add JavaScript that detects this state and auto-advances the task counter.
- When a task auto-completes, show a small toast in the bottom-right: "Task 1 complete. Moving to task 2." — does NOT advance the screen, just updates the sidebar.

SCREEN N+1 — Exit Survey
After all tasks (or when the participant uses Skip on the last task):
- "Thanks for completing the test."
- Then 4 short questions, each on its own scrolling section:
  1. "How easy was this to use?" — 1-5 scale, single-tap radio
  2. "What was the most confusing moment?" — open text, 200 char limit
  3. "Would you recommend this to a coworker?" — 0-10 NPS-style scale
  4. "Anything else you want us to know?" — open text, 500 char limit
- Submit CTA: "Send feedback"
- After submit: "Thanks. You can close this window."

DESIGN DIRECTION:
Match the production product as closely as possible. Use our Design System (attached). Research participants need to feel like they are using the real product, not a research artifact. The exit survey is the only place where it should look "research" (slightly more form-y, slightly less branded).

NOT INCLUDED (do not add):
- No reviewer hints inside the flow itself (the whole point is to see if they figure it out)
- No "Are you sure?" confirmations beyond what production would have
- No analytics that track every click in the prototype itself — your test platform handles recording
- No login or signup gates — participants land on the welcome screen and start

OUTPUT: 1 welcome screen + N task screens + 1 exit survey screen, all clickable. Persistent task sidebar. Completion detection wired up. Mobile-responsive. Single shareable URL.
```

---

## Companion deliverable: the test plan you send with the link

When you send the prototype to a research recruiter or platform, paste this alongside:

```
Test name: [FEATURE NAME] usability — [DATE]
Estimated time: 8-15 minutes
Participants needed: [N]
Screening criteria: [3-5 BULLET POINTS — e.g. "Has hired for an engineering role in the last 12 months", "Uses an ATS at work (Greenhouse, Lever, Ashby, Workday)"]

Prototype URL: [CLAUDE DESIGN SHARE LINK]

Tasks (do not show participants this list — the prototype shows them):
1. [TASK 1]
2. [TASK 2]
3. [TASK 3]

What I am specifically watching for:
- [SPECIFIC BEHAVIOR 1 — e.g. "Do they hesitate before clicking Parse with AI?"]
- [SPECIFIC BEHAVIOR 2]
- [SPECIFIC BEHAVIOR 3]

Recording requirements: think-aloud + screen recording + face cam if possible.
```

---

## What changes vs. a stakeholder prototype

| Element | Stakeholder Prototype (08) | Research Prototype (15) |
|---|---|---|
| Reviewer hints | Yes — small "i" icons explain what to look for | No — defeats the purpose |
| Sample data | Real-looking, reviewer-relevant (e.g. their domain) | Real-looking, generic-but-plausible |
| Step indicator | Yes — they need to know where they are | No — production product would not have one mid-flow |
| Skip option | No — they review the whole thing | Yes — real users give up; capture that |
| Exit | "Thanks for reviewing" message | 4-question exit survey |
| Companion message | Slack DM with the ask | Test plan with screening criteria |

---

## Why this prompt exists

Most PMs run usability tests by hand-rolling a Figma prototype and then sending it to Maze. The Figma → Maze flow has friction (export, re-link interactions, set up the test). A Claude Design prototype with task tracking baked in means the URL itself is the test artifact — paste into UserTesting, Maze, or Lyssna and start recruiting in 5 minutes.

The exit survey at the end gives you the qualitative + scale data without needing a separate Typeform. One artifact. One URL. One recording per participant.
