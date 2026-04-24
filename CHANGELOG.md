# Changelog

All notable changes to this toolkit. Format inspired by [Keep a Changelog](https://keepachangelog.com/).

This toolkit is tested against the Claude Design Research Preview as of **April 2026**. As Claude Design ships new features, prompts may need updating — entries below note when each prompt was last verified.

---

## [1.0.0] — 2026-04-24

Initial public release. Companion to [The PM's Complete Guide to Claude Design](https://www.news.aakashg.com/p/claude-design) in Product Growth.

### What is in this release

**Nine copy-paste prompts** — covering every PM use case from internal tools to investor demos:

- `01_investor_demo.md` — Dark premium investor demo page with liquid glass, animated metrics, before/after.
- `02_product_launch.md` — Clean SaaS launch page with email capture, feature grid, social proof, plus analytics + ESP integration variants.
- `03_feature_flow.md` — 4-screen interactive prototype with refinement prompt and i18n/RTL support.
- `04_animated_showcase.md` — Cinematic video background showcase with Framer Motion refinement, no-video CSS-only fallback, prefers-reduced-motion handling.
- `07_pitch_deck.md` — 14-slide board update / quarterly deck with speaker notes, exports to PPTX.
- `08_stakeholder_prototype.md` — Clickable review prototype with real sample data, step indicator, comment-ready, plus Slack-message template.
- `13_internal_tool.md` — Admin / ops dashboard. Density over whitespace, keyboard-first, command palette, production-realistic data.
- `14_commerce_page.md` — E-commerce PDP / cart / checkout with variant selectors, inventory states, RTL support for MENA.
- `15_research_prototype.md` — Unmoderated usability test prototype with task sidebar, completion detection, exit survey.

**Six references** — the patterns and templates you reuse on every project:

- `05_design_system.md` — Liquid glass CSS, four typography sets (dark cinematic, clean SaaS, warm consumer, retro terminal, playful), all @keyframes, color tokens with WCAG contrast ratios.
- `06_pm_tips.md` — Six lessons from testing plus token budget and data-privacy guidance.
- `09_design_system_setup.md` — One-hour Design System setup + full SKILL.md template (matches article §4a).
- `10_clarifying_questions.md` — Cheat sheet for the 9 questions Claude asks before generating, with the 30-second answer template + anti-copy ban list.
- `11_claude_code_handoff.md` — README template for the Claude Code handoff bundle. Security baseline, i18n requirements, bundle size budget, definition-of-done checklist.
- `12_error_recovery.md` — 14 common failures with copy-paste fix prompts. Covers liquid glass, mobile breaks, video loading, animations, fonts, hover reveals, Safari diffs, color drift, placeholder data, rigid output, WCAG failures, prefers-reduced-motion, context drift.

**Plus:**
- `CHEATSHEET.md` — Printable 1-pager. Tape above your monitor.
- `LICENSE` — MIT.

---

## Risk note

Claude Design is a research preview as of this release. Anthropic may ship breaking changes to the surface during the preview period. If a prompt stops working as expected:

1. Check this changelog for an updated version of the prompt.
2. Open an issue on GitHub describing what changed.
3. As a fallback, the underlying CSS / animation patterns in `05_design_system.md` are stack-agnostic — they work in any HTML/CSS environment if Claude Design itself becomes unavailable.

The toolkit will continue to track Claude Design changes. If Anthropic ever deprecates Claude Design (unlikely given the trajectory), every prompt here is portable to v0, Bolt, Lovable, or any future AI design tool with minor tweaks — the ideas (clarifying-question discipline, free-form-then-constrain, Tweaks-Edit-Comments order) transfer regardless of vendor.
