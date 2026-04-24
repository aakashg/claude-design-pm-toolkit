# Claude Design PM Prompt Toolkit
## Prompt 13: The Internal Tool / Admin Dashboard

**Use case:** Admin UIs, operator consoles, internal ops tools, API explorer surfaces, trust & safety dashboards, support console. The stuff nobody gets to "design properly" because it is not customer-facing — so it ends up as Retool or a barebones table forever.

**What you get:** Dense, keyboard-navigable, data-first interface. Dark or light theme. Built to look like Vercel, Linear, or Retool done right, not a SaaS marketing site.

Most prompts in this toolkit target landing pages or onboarding. Internal tools have the opposite constraints: information density > whitespace, shortcut-first > discoverability, production-realistic data > aspirational mockups.

---

## The Prompt

```
Build an internal admin tool for [PRODUCT NAME]: the [TOOL NAME] dashboard.

CONTEXT: This is an internal tool used by [USER ROLE — e.g. "ops engineers", "support agents", "trust & safety reviewers"]. It is NOT customer-facing. Design goals are the opposite of a marketing page:
- Information density wins over whitespace
- Keyboard-first: every action has a shortcut
- Production-realistic data: real-looking IDs, timestamps, statuses
- Zero marketing copy, no "designed by humans" taglines, no confetti
- Users open this tool 20 times a day; optimize for speed of repeat use

USER'S PRIMARY JOB: [WHAT DO THEY DO ON THIS SCREEN ALL DAY — 1 sentence. Example: "Review flagged content, classify each as approved/rejected/escalate, move to the next item."]

AESTHETIC: Dark technical (default) or light clean (your pick):

Option A (Dark Technical — recommended for developer / ops tools):
- Background: #0a0a0b
- Surface: #131316
- Surface-elevated: #1c1c20
- Border: rgba(255,255,255,0.08)
- Text: #f5f5f5 primary, rgba(255,255,255,0.6) secondary
- Accent: your brand color
- Font: JetBrains Mono or Geist Mono for IDs and data. Inter for UI.
- Feels like Vercel's dashboard or Linear.

Option B (Light Clean — for less technical internal users):
- Background: #fafbfc
- Surface: #ffffff
- Border: #e5e7eb
- Text: #0f172a primary, #64748b secondary
- Font: Inter everywhere
- Feels like Retool done right, or Stripe Dashboard.

LAYOUT:
- Left sidebar: 240px, collapsible. Logo top, nav items below (Home, [TOOL NAME], [OTHER TOOL], Settings), user menu bottom.
- Top bar: 48px. Left: breadcrumb / current page title. Center: global command palette trigger (cmd+K). Right: environment switcher (prod/staging/dev), notifications, user avatar.
- Main content: fills the remaining space.

MAIN CONTENT — the actual tool:

1. HEADER BAR: Title of current view, count of records, "last refreshed: [timestamp]", a refresh button.

2. FILTER / SEARCH BAR: Full-width row below the header.
   - Search input (monospace, placeholder "Search by ID, email, or key: prefix for filters")
   - Filter pills: Status (multi-select), Date (range picker), Assigned (person picker), Tags
   - A "Saved views" dropdown with 3-4 preset views
   - Filters persist in URL query params so views are shareable

3. DATA TABLE: Core of the tool.
   - Dense rows (48px height max). Zebra-striping subtle.
   - Columns: ID (monospace, truncated with copy-on-click), Timestamp (relative: "4m ago" + absolute on hover), Status (colored pill), Subject (truncated, full on hover), Actions (inline icon buttons).
   - Sortable column headers. Click to sort, click again to reverse, third click to clear.
   - Sticky header on scroll.
   - Right-click on row = context menu (Copy ID, Open in new tab, Archive, etc.)
   - Keyboard: J/K to navigate rows, Enter to open, Esc to close detail pane.
   - Select with shift-click or checkbox for bulk actions.

4. DETAIL PANE: Slides in from the right when a row is clicked.
   - 60% width of viewport, or full width on screens below 1280px.
   - Header: record ID + status pill + quick actions (Approve, Reject, Escalate — keyboard-accessible with 1/2/3).
   - Tabs: Overview, Activity, Raw JSON, Audit log.
   - Overview tab shows structured data in a definition-list format (key-value pairs).
   - Raw JSON tab uses a syntax-highlighted code block (monokai-style colors).
   - Activity tab shows a timeline of events.
   - Bottom: free-text notes field, "Notes persist with the record" hint.

5. BULK ACTION BAR: When 2+ rows are selected, a floating bar appears at the bottom.
   - "[N] selected" count on left
   - Action buttons: Approve all, Reject all, Assign to, Export CSV, Clear selection
   - Keyboard: Cmd+A selects all visible, Esc clears.

6. COMMAND PALETTE: Cmd+K anywhere.
   - Search across actions, records, and navigation
   - Recent items section at top
   - Keyboard-only navigation, no mouse needed

SAMPLE DATA REQUIREMENTS:
- 25+ rows in the table, NOT placeholder "Row 1, Row 2"
- Realistic IDs (e.g. "evt_1Nabc2xyz" for Stripe-style, or "usr_01H8ABC..." for ULID-style)
- Real timestamps ranging from "2m ago" to "3d ago"
- Mix of statuses (not all "Active") — include edge cases: "Failed", "Pending review", "Retrying"
- Realistic subjects / names that vary in length so the truncation behavior is visible

NOT NEEDED:
- No hero section
- No testimonials
- No pricing
- No "Get started" CTA
- No marketing copy anywhere
- No heavy animation (subtle 0.15s transitions on hover only)
- No illustrations
- No "Made with ❤️" footer

ACCESSIBILITY:
- Every action keyboard-accessible. Tab order follows visual order.
- Focus states: clear 2px ring in the accent color.
- Screen reader labels on icon-only buttons.
- Color contrast: WCAG AA minimum on all text, especially low-opacity muted text.

OUTPUT: Single HTML file with all CSS inline. Keyboard shortcuts work. Table is populated with 25+ realistic rows. Sidebar, detail pane, and command palette are all functional.
```

---

## What to put in each slot

| Slot | Example |
|---|---|
| Product name | Arcline |
| Tool name | Review Queue |
| User role | Trust & safety analysts |
| User's primary job | Review flagged content, classify each as approved/rejected/escalate, move to the next item |

---

## Refinement prompts (use after first generation)

**Add realistic workflows:**
```
Add 3 realistic bulk workflows that operators actually run:
1. "Approve all matching filter" — one-click approve everything currently filtered, with an undo toast.
2. "Assign to me" — shortcut Cmd+Shift+A, assigns selected records to current user.
3. "Snooze until tomorrow 9am" — shift selected records out of the queue for a day, they return in-queue.
Each workflow shows a subtle confirmation toast with an Undo link (10-second window).
```

**Add keyboard shortcut reference:**
```
Add a keyboard shortcut cheat sheet. Trigger: press "?" anywhere. Shows a modal with all shortcuts grouped by category: Navigation (J/K/G-H/Cmd-K), Actions (1/2/3/A/R), Bulk (Cmd-A/Shift-click), View (F/D/V). Each row: key combination on the left in a monospace pill, description on the right. Dismiss with Esc or ? again.
```

**Add production-safety visual cues:**
```
Add environment indication so operators never confuse prod and staging:
- Top bar has a persistent environment pill: "PROD" in red, "STAGING" in amber, "DEV" in gray.
- Bulk-destructive actions (Delete, Revoke) have a secondary confirmation in PROD only.
- Prod actions that affect customer records get a subtle red underline in the action menu.
```

---

## Why this prompt exists

Claude Design's defaults are marketing-site aesthetics: generous whitespace, large hero, beautiful illustrations. That is wrong for internal tools. Operators open these 30 times a day and need density, keyboard shortcuts, and realistic data. This prompt inverts the defaults explicitly so you do not have to fight them in 10 rounds of Comments.

The most-skipped use case in the article. The one with the highest day-to-day ROI.
