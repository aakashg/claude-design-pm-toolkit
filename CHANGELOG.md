# Changelog

All notable changes to this toolkit. Format inspired by [Keep a Changelog](https://keepachangelog.com/).

This toolkit is tested against the Claude Design Research Preview as of **April 2026**. As Claude Design ships new features, prompts may need updating — entries below note when each prompt was last verified.

---

## [1.1.0] — 2026-04-24

Round-2 expansion based on paid-subscriber feedback. Repo grew from 6 → 17 files.

### Added
- `07_pitch_deck.md` — Slide deck prompt for board updates and investor decks (article Use Case 2). 14-slide structure with speaker notes.
- `08_stakeholder_prototype.md` — Clickable review prototype (article Use Case 4). Real sample data, step indicator, comment-ready, with Slack-message template.
- `09_design_system_setup.md` — One-hour Design System setup + full SKILL.md template (article §7).
- `10_clarifying_questions.md` — Cheat sheet for the 9 questions Claude asks before generating. Includes the 30-second answer template + anti-copy ban list.
- `11_claude_code_handoff.md` — README template for the Claude Code handoff bundle. Includes security baseline, i18n requirements, bundle size budget, definition-of-done checklist.
- `12_error_recovery.md` — 14 common failures with copy-paste fix prompts. Covers liquid glass, mobile breaks, video loading, animations, fonts, hover reveals, Safari diffs, color drift, placeholder data, rigid output, WCAG failures, prefers-reduced-motion, context drift.
- `13_internal_tool.md` — Admin / ops dashboard prompt. Density over whitespace, keyboard-first, command palette, production-realistic data.
- `14_commerce_page.md` — E-commerce PDP / cart / checkout flow. Variant selectors, inventory states, mini-cart, single-page checkout, RTL refinement prompt.
- `15_research_prototype.md` — Unmoderated usability test prototype. Task sidebar, completion detection, exit survey, companion test plan.
- `CHEATSHEET.md` — Printable 1-pager.
- `LICENSE` — MIT.
- `CHANGELOG.md` — this file.

### Changed
- `README.md` — full rewrite. Added persona-driven "who is this for", quickstart table, article-section-to-file map, honest-cost breakdown, contributing section.
- `01_investor_demo.md` — added board-facing CTA copy variant + WCAG contrast accessibility checklist.
- `02_product_launch.md` — added 3 analytics-hook variants (PostHog, Segment, GA4) + 3 ESP integration variants (ConvertKit, HubSpot, Resend).
- `03_feature_flow.md` — added warning to scrub example blocks before sending; added i18n + RTL refinement prompt.
- `04_animated_showcase.md` — added no-video CSS-only fallback; added prefers-reduced-motion refinement.
- `05_design_system.md` — added 3 alternative typography sets (Warm Consumer, Retro Terminal, Playful Consumer); added WCAG contrast ratios on dark color tokens.
- `06_pm_tips.md` — token costs aligned with article ($2-7 per artifact); added data-privacy section (no PII, no secrets, no production data).
- All article URL references updated from `news.aakashg.com` (homepage) to the canonical post URL `news.aakashg.com/p/pm-guide-claude-design`.

---

## [1.0.0] — 2026-04-23

Initial release. The 6 files referenced from the original article.

### Added
- `01_investor_demo.md` — Dark premium investor demo page.
- `02_product_launch.md` — Clean SaaS launch page.
- `03_feature_flow.md` — 4-screen interactive prototype with refinement prompt.
- `04_animated_showcase.md` — Cinematic video background showcase with Framer Motion refinement.
- `05_design_system.md` — Liquid glass CSS, typography, animations, color tokens.
- `06_pm_tips.md` — Six lessons from testing.

---

## Risk note

Claude Design is a research preview as of this release. Anthropic has shipped breaking changes to the surface roughly monthly during the preview period. If a prompt stops working as expected:

1. Check this changelog for an updated version of the prompt.
2. Open an issue on GitHub describing what changed.
3. As a fallback, the underlying CSS / animation patterns in `05_design_system.md` are stack-agnostic — they work in any HTML/CSS environment if Claude Design itself becomes unavailable.

The toolkit will continue to track Claude Design changes through 2026 and beyond. If Anthropic deprecates Claude Design (unlikely given the trajectory), every prompt here is portable to v0, Bolt, Lovable, or any future AI design tool with minor tweaks — the ideas (clarifying-question discipline, free-form-then-constrain, Tweaks-Edit-Comments order) transfer regardless of vendor.
