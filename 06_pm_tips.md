# Claude Design PM Prompt Toolkit
## Six Things I Learned From Testing This

These are the mistakes I made in the first three sessions and what changed after I stopped making them.

---

## 1. Screenshot the layout. Do not describe it.

Find something on Dribbble, Higgsfield, or motionsites.ai that has the layout you want. Take a screenshot. Use Nano Banana 2 to strip the existing text and imagery — if you leave the original content in the image, Claude tries to match it and the output gets confused. Upload the clean image. Prompt: "use this exact layout with our established colors and typography."

Claude builds to the visual reference every time. Describing a complex layout in words takes longer and produces worse output. The layout has a lot of implicit decisions — column ratios, spacing, component hierarchy — that are faster to show than to specify.

---

## 2. Use motionsites.ai for interaction prompts.

motionsites.ai has free pre-built prompts for specific interactions: spotlight reveal effects, liquid glass CSS, custom JavaScript typography animations, fade systems. You do not have to write any of this from scratch. Copy the interaction prompt from motionsites.ai, paste it into Claude Design, replace the asset URLs with yours. The prompts in this toolkit use the liquid glass CSS from this source, refined for PM use cases.

Higgsfield is useful for cinematic video backgrounds — especially looping product visuals, abstract textures, and environment shots that work as hero backgrounds. Dribbble and Pinterest for layout and composition inspiration.

---

## 3. Edit first. Comments second. Chat third.

This is the modality hierarchy that saves the most tokens.

**Edit** is for anything you can click on directly: a text element, a color, a font weight. Free, instant, no token burn.

**Comments** are for structural changes you want to batch. Select an element, leave a note ("sidebar has too much empty space", "this button should be the primary CTA, not secondary"), select the comments you want to act on, hit Send to Claude. Use this when you have 3 or more changes to make at once. Do not use it for a single minor fix. One thing worth knowing: comments can be buggy. Undeletable comments and unexpected whitespace are real issues in the current research preview. If a comment is not working, paste it into Chat instead.

**Chat** is for direction-level changes: "make the whole thing darker and more minimal", "switch the layout from 3-column to alternating rows", "add a second CTA section before the footer". Use Chat for decisions, Edit and Comments for execution.

---

## 4. Give Claude total creative freedom on the first generation.

The output quality drops significantly when you force strict design system adherence from the start. The constraint evaluation burns tokens and the result tends to be stiff. Let Claude design freely on the first pass. You will get better visual quality. Then use a second prompt to pull it on-brand: "apply our design system — use [hex color] for primary actions, [font name] for headings, [border-radius] for cards, remove any gradients that are not in our palette."

Build free-form first. Apply brand constraints second. This is the correct order.

---

## 5. Nail the hero section, then expand.

Once you have established the background, typography, color treatment, and core CSS effects in the hero, prompt Claude to build the rest of the page from that foundation. The prompt: "build the rest of the page in the same visual style as the hero — same colors, same typography, same liquid glass effects, same animation pattern. Generate 6-8 sections."

Getting the hero right is roughly 90% of the visual work. Everything else inherits from it. This is also where the time investment makes sense. Spend the tokens on the hero until it is right before expanding.

---

## 6. Plan your token budget before you start.

Daily PM use will hit your Pro plan limits. One heavy session building a complex showcase can burn 95% of a weekly quota. Enable extra usage on Team or Enterprise before your first serious build session, or upgrade to Max tier. Think of each hi-fi artifact as having a per-page cost. A fully built 8-section launch page costs roughly $10–20 in tokens when you include the refinement prompts. The comparison is not "is this cheaper than free" — it is "is this cheaper than a designer's time" and the answer is yes by a significant margin.

The one trap is using Comments to correct design system errors repeatedly. If Claude keeps getting your brand fonts wrong, it is cheaper to export the design and fix the typography in Figma manually for 10 minutes than to spend 15 token-heavy comment cycles correcting it.

---

## The video workflow (quick reference)

**Generate:** Kling 3.0 or Sedance 2.0. Universal prompt: `looping animation no camera movement no extra elements to be added no zoom in or zoom out looping animation`. Keep under 8 seconds. Two image variants (e.g. plain surface + textured surface) creates a transition effect between the two.

**Fix loops:** If the video has a hard cut when it restarts, ask Claude to add a JavaScript fade-out/in on loop. Prompt: `add a timeupdate event listener that fades the video to opacity 0 over 0.3s when 0.4 seconds remain in the loop, then fades back to opacity 1 as it restarts.`

**Host:** Mux.com free tier or Cloudflare Stream. Get the live URL. Claude Design cannot use local files.

**Add motion:** Framer Motion smooths everything out after the initial generation. Prompt: `convert the hero section animations and feature card hover states to use Framer Motion (motion/react). Use spring physics for hover states: stiffness 280, damping 22.`

**Mobile check:** After generating, test at 375px width. If anything breaks: `make the entire page responsive. On screens below 768px: all multi-column grids should stack to 1 column, headline font sizes should cap at 48px, navbar should show only the logo and primary CTA button.`
