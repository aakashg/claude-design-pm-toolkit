# Claude Design PM Prompt Toolkit
## Prompt 14: The Commerce Page — PDP / Cart / Checkout

**Use case:** E-commerce product detail pages, cart, checkout, order confirmation. The most-skipped surface in default Claude Design output, because the toolkit defaults are marketing-page biased. This prompt is the explicit retail flow.

**What you get:** A 3-screen commerce flow — PDP with variants and add-to-cart, mini-cart slide-out, checkout with shipping + payment + confirmation. Real product copy, real money formatting, plausible inventory states.

---

## The Prompt

```
Build a 3-screen e-commerce flow for [PRODUCT NAME], a [PRODUCT CATEGORY — e.g. "premium ceramic dinnerware brand", "AI-powered indoor garden", "boutique skincare line"].

USER: Returning customer who has bought from us before. Knows the brand. Browsing on a Tuesday evening on their phone. Cart abandoned 4 days ago, came back via a re-engagement email.

DEVICE: Mobile-first, 375px primary viewport. Desktop responsive at 1024px+ but the design optimization is for mobile.

VISUAL DIRECTION: [PICK ONE]

Option A (Modern minimal — Aesop, Apple, Glossier):
- Background: warm off-white #fafaf7
- Text: #1a1a1a primary, #6b6b6b muted
- Accent: single brand color used sparingly
- Typography: serif display + sans-serif body. Generous whitespace.
- Photography: large product imagery with soft shadows, never on white

Option B (Bold consumer — Allbirds, Casper, Warby Parker):
- Background: white with strategic colored sections
- Text: #0a0a0a primary
- Accent: bold brand color used liberally
- Typography: bold sans-serif display + clean sans-serif body
- Photography: lifestyle imagery + product shots interlaced

Option C (Premium editorial — Hermès, Aesop online, Net-a-Porter):
- Background: cream or pale warm tone
- Text: dark espresso brown, not pure black
- Accent: muted single color
- Typography: high-contrast serif (Didone-style) display + thin sans body
- Photography: editorial-style, often cropped, often abstract

SCREENS TO BUILD (3 screens, fully clickable):

SCREEN 1 — PDP (Product Detail Page)
A single product page. Layout (mobile-first):
- Top: full-bleed product image carousel. Swipeable. Pagination dots bottom-center. 4-5 images.
- Below image: product name (display font, 28px), price (in correct currency formatting — "$84" not "$84.00", "€84,00" with locale-correct comma if EUR), short tagline (1 line, muted)
- Variant selectors: color swatches (round 32px chips, selected gets a 2px ring) + size selector (text buttons in a row, selected gets dark fill). NEVER use a generic dropdown for variants — always tactile selectors.
- Quantity stepper: minus / number / plus, 40x40px tap targets each.
- Inventory state:
  - "In stock" → no message
  - Low stock (≤5) → small "Only [N] left" in a soft alert color
  - Out of stock for selected variant → CTA changes to "Notify when back" with email field
- Primary CTA: "Add to bag" — full width, 52px tall, solid brand color. Sticky at the bottom on scroll.
- Below CTA: shipping promise ("Free shipping over $50, returns within 30 days") in 12px muted.
- Below the fold:
  - Description (3-4 sentence rich product copy — never marketing fluff, focus on materials, dimensions, what makes it specific)
  - Specs accordion (Materials, Dimensions, Care, Sustainability)
  - Reviews summary: average rating + count, link to all reviews
  - 3 review excerpts (real-sounding 2-3 sentence reviews with reviewer name + verified badge)
  - "You might also like" — 4-product carousel

SCREEN 2 — MINI-CART
Triggered when "Add to bag" is clicked. Slides in from the right (desktop) or up (mobile), 90% opacity backdrop behind.
- Header: "Bag (3)" + close X
- Cart items: 3 line items with image thumbnail (64x64), product name, variant (color + size), price, quantity stepper, remove (X) button
- Subtotal, estimated shipping, estimated tax, total — itemized.
- Promo code input: collapsible, "Have a code?" link expands to input + apply button
- Free shipping progress bar: "Add $12 more for free shipping" — actual progress bar fills as the cart total approaches the threshold
- Primary CTA: "Checkout — $XX.XX" full width
- Secondary: "Continue shopping" text link
- Trust signals row: payment method icons (Visa, Mastercard, Amex, Apple Pay, PayPal, Klarna)

SCREEN 3 — CHECKOUT
Single-page checkout (NOT multi-step — those convert worse). Sections stacked:
1. Express checkout — Apple Pay / Google Pay / Shop Pay buttons row, 48px tall. "or" divider below.
2. Contact: email input + "I want order updates and offers" checkbox (default unchecked — opt-in not opt-out)
3. Shipping address: name, address line 1, address line 2 (optional), city, state, ZIP, country (defaults to user's geo). Auto-complete on address line 1 from a placeholder Google Places integration.
4. Shipping method: radio group, 3 options (Standard 5-7 days FREE, Express 2-3 days $9, Overnight $24)
5. Payment: card number (with auto-formatting), expiry, CVC, name on card. Card type icon appears as the user types (Visa logo when first 4 digits match Visa pattern, etc.)
6. Order summary on the right side at desktop, expandable accordion at top on mobile.
7. Place order CTA: full width, 56px tall, brand color. Says "Place order — $XX.XX".
8. Below CTA: trust note "Your card is not charged until your order ships. Free returns within 30 days."

ORDER CONFIRMATION (post-submission state of screen 3):
- Top: large checkmark animation (CSS-only, scales in from 0 to 1 with a slight overshoot, 0.4s)
- "Order #1042 confirmed"
- "We sent a confirmation to [email]"
- Order summary recap
- "Track your order" CTA + "Continue shopping" secondary

REAL DATA REQUIREMENTS:
- Product names: real brand voice (e.g. "Linen-blend Crew, Morning Mist" — not "Product 1")
- Prices: ending in plausible numbers ($84, $128, $42 — not $99.99 or $100.00)
- Reviewer names: mix of cultures and lengths
- Cart contents: 3 real-looking items at varied price points
- Inventory state: at least one variant should show "Low stock" so the alert UI is visible
- Currency: assume USD by default, but if I specify a country in the persona, format correctly

NOT INCLUDED (do not add):
- No newsletter signup popup
- No live chat widget
- No "exit intent" modal
- No countdown timer ("Sale ends in 4:23!")
- No "27 people are viewing this" social proof
These are dark patterns. Modern brands skip them.

OUTPUT: 3 fully clickable screens. Mobile-first responsive. Real product imagery placeholders described well enough that I can swap in real product photos in 5 minutes. RTL-ready (use logical CSS properties for any internationalization).
```

---

## Localization — RTL languages (Arabic, Hebrew)

If your store ships to MENA, add this refinement prompt:

```
Add RTL layout support. Wrap the entire output with dir="auto" on the
<html> tag. Replace all left/right CSS properties with logical
equivalents:
- padding-left → padding-inline-start
- margin-right → margin-inline-end
- text-align: left → text-align: start
- left: 0 → inset-inline-start: 0

Directional icons (chevrons, arrows) get class="rtl:rotate-180" so
they mirror in RTL languages. Currency symbols flip side: in
Arabic-locale, the symbol comes after the number ("84 د.إ" not
"د.إ 84").

Test by adding dir="rtl" to the <html> tag and reloading. The whole
layout should mirror — image carousels swipe the other direction,
checkout fields align right, the cart slides in from the left.
```

---

## What to put in each slot

| Slot | Example |
|---|---|
| Product name | Mira & Bloom (a ceramic dinnerware brand) |
| Product category | Premium ceramic dinnerware made in Portugal |
| Visual direction | Option A — Modern minimal |
| Real-product imagery placeholders | "Hand-thrown stoneware bowl, photographed against a pale clay backdrop" |

---

## Refinement prompts (use after first generation)

**Add Apple Pay / Shop Pay express flow:**
```
Wire the express checkout buttons. Apple Pay button uses the official
Apple Pay JS API with a payment request for the cart total. Shop Pay
button uses Shopify's Shop Pay component if available, otherwise
falls back to a same-page email-only express form. Show only the
buttons that work on the user's device — Apple Pay only on Safari,
Google Pay only where available.
```

**Add a one-click subscribe variant:**
```
Add a "Subscribe and save 15%" toggle on the PDP under the variant
selectors. When enabled: shows the discounted price, a frequency
dropdown (every 30 / 60 / 90 days), and the Add to bag CTA changes
to "Subscribe — $XX.XX every 30 days". This replaces the standard
add-to-bag, not adds to it.
```

**Add post-purchase upsell:**
```
On the order confirmation screen, add a "Frequently bought together"
3-item row below the order summary. Each item shows: thumbnail, name,
price, "Add to order" button. Items added here ship with the existing
order at no additional shipping cost. Add a small banner: "Add within
the next 60 minutes to ship with your order."
```

---

## Why this prompt exists

E-commerce was the single most-requested missing use case from PM readers. The default Claude Design prompt, given "build a product page", produces a marketing landing page with a "Buy now" CTA — not a real PDP with variants, inventory state, mini-cart, and checkout. This prompt fills the gap explicitly with all the surfaces a commerce PM actually ships.
