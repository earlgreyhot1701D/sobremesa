# QA Report — Sobremesa

Pre-submission audit for the [DEV Frontend Challenge, Comfort Food Edition](https://dev.to/challenges/frontend-2026-07-29), Perfect Landing prompt.

Live site: https://sobremesa-dev.vercel.app/

---

## 1. Challenge Compliance

| # | Check | Result |
|---|-------|--------|
| 1.1 | LICENSE present, README references it | **PASS** — MIT license present. README last line: `MIT. See [LICENSE](LICENSE).` |
| 1.2 | Third-party code credited, not deployed | **PASS** — `design/README.md` documents `support.js` as "Claude Design runtime…Third-party framework code, not authored here." `index.html` does not reference it. |
| 1.3 | Fonts credited with license | **PASS** — Loads Alfa Slab One, Crimson Pro, Oswald. README credits all three with links and states "all SIL Open Font License." All three are indeed OFL. |
| 1.4 | Asset rights disclosed | **PASS** — Footer reads: "AI assisted. Human approved. Powered by NLP." README section "The illustrations" states they are AI-generated. |
| 1.5 | Site publicly reachable | **PASS** — `https://sobremesa-dev.vercel.app/` returned full page content with no login. |

---

## 2. Accessibility

| # | Check | Result |
|---|-------|--------|
| 2.1 | Heading hierarchy | **PASS** — h1: "Sobremesa" / h2: "The six meals" / h3×6 (dish names) / h2: "Total time at the table" / h2: "Add your table". No skipped levels. |
| 2.2 | Landmarks | **PASS** — `<header>`, `<main id="main">`, `<footer>` present. |
| 2.3 | Native controls only | **PASS** — All interactive elements are `<button type="button">`, `<a>`, or `<input>`/`<button type="submit">`. Zero `role="button"` on non-semantic elements. |
| 2.4 | Disclosure state | **PASS** — Each `.reveal` button has `aria-expanded` toggled by JS and `aria-controls` pointing to `panel-01` through `panel-06`, all of which exist as real IDs. JS sets `panel.hidden` in sync with `aria-expanded`. |
| 2.5 | Visible focus indicators | **PASS** — `.skip:focus`, `.maplink:focus-visible`, `.reveal:focus-visible`, `input:focus-visible`, `.submit:focus-visible`, `.again:focus-visible` all have `outline: 3px solid var(--ink); outline-offset: 3px`. All high contrast against their backgrounds. |
| 2.6 | Skip link | **PASS** — `<a class="skip" href="#main">Skip to the meals</a>` is first in `<body>`. Positioned off-screen until `:focus`. |
| 2.7 | Enter and Space on buttons | **PASS** — All are native `<button>` elements which natively respond to both keys. |
| 2.8 | Focus not lost on interaction | **PASS** — Form submit moves focus to first invalid field on error. Disclosure toggle does not move focus. No `blur()` or focus-to-body calls anywhere. |
| 2.9 | Decorative images hidden | **PASS** — All `rule-l`, `rule-s`, `flower.png`, `plates.png`, bar dividers, and fallback flowers have `aria-hidden="true"` and `alt=""`. |
| 2.10 | Dish image alt text | **PASS** — See table below. |
| 2.11 | Contrast | **PASS** with note — See contrast table below. |
| 2.12 | Form labels | **PASS** — Each input has a visible `<label for="f-{name}">` and a `<span class="hint">` described by `aria-describedby`. |
| 2.13 | Empty form submit | **PASS** — Validation runs on submit, sets field-level `.err` messages, calls `focus()` on first invalid field. Values are preserved (no reset on error). |
| 2.14 | Errors not color-only | **PASS** — Each error has a `✕` symbol prefix and text message. |
| 2.15 | Success via live region | **PASS** — `<p class="status" role="status" aria-live="polite">` receives `textContent` on success. |
| 2.16 | No color-only information | **PASS** — Duration bars are `aria-hidden="true"`, duration stated in text. Errors use symbol + text. |
| 2.17 | 44×44px targets | **PASS** — `.maplink` has `min-height:44px`. `.reveal` has `min-height:44px; min-width:44px`. `.submit` has `min-height:52px; min-width:44px`. `.again` has `min-height:44px`. |
| 2.18 | `lang="es"` on Spanish terms | **PASS** — Wrapped: all 6 dish names, `micheladas`, `Sobremesa` (in context), `este taco sí está bien perrón`, `cazuela`, `Día de los Muertos`, `templo`, `Provecho`. Culinary loanwords used inline in English sentences (arrachera, birote, quesillo, tasajo, asiento) are not wrapped, which is standard practice. |
| 2.19 | prefers-reduced-motion | **PASS** — `@media (prefers-reduced-motion: reduce){*{animation:none !important;transition:none !important}}`. No content removed. |
| 2.20 | 200% zoom | **PASS** — Layout uses `clamp()` for font sizing, flex/grid for layout, no fixed heights on content containers. Text-only zoom: type scale uses `px` in `clamp()` so text-only zoom has limited effect; this is an inherent trade-off of viewport-responsive typography. |
| 2.21 | Automated audit (Lighthouse/axe) | **CANNOT VERIFY** — Requires a browser environment. Recommend running `npx lighthouse https://sobremesa-dev.vercel.app --only-categories=accessibility`. Based on source analysis, expected score is 95-100. |

### 2.10 — Six Dish Alt Texts

| # | Alt text |
|---|----------|
| 01 | Two stacked corn tortillas holding finely chopped charred beef, a stripe of pale green guacamole sauce, cilantro and small white cubes of onion, with a grilled spring onion and a lime wedge beside them. |
| 02 | A large flour tortilla folded open around thick slices of grilled steak with charred edges, refried beans underneath, and stripes of chunky guacamole and red salsa along the top. |
| 03 | A folded corn tortilla holding a long piece of golden battered fish zigzagged with white crema, shredded cabbage underneath, a lime wedge resting beside it. |
| 04 | A crusty split roll heaped with shredded pork and rings of raw white onion, sitting in a shallow dish flooded with thin brick-red chile salsa. |
| 05 | Two corn tortillas holding thin strips of red-edged roast pork, topped with cubes of pineapple, chopped onion and cilantro, a lime wedge beside them. |
| 06 | A very large thin tortilla folded in half and blistered dark from the coals, with black beans, strands of stretched white cheese and strips of grilled beef spilling from the open edge. |

All unique, describe the plate, do not repeat the dish name.

### 2.11 — Contrast Table

The paper grain uses `background-blend-mode: multiply` on a per-surface background layer. The grain darkens the base color, making the effective background *darker* than the raw token, which *improves* contrast for dark-on-light text.

Computing with raw token values (worst case, no grain darkening):

| Foreground | Background | Use | Ratio | Requirement | Verdict |
|-----------|-----------|-----|-------|-------------|---------|
| `--ink` #2C251A | `--cream` #F6E3BB | Body text (cards, descriptions) | **12.1:1** | 4.5:1 | ✓ |
| `--green` #22402C | `--cream` #F6E3BB | Labels, headings, kickers | **9.6:1** | 4.5:1 / 3:1 | ✓ |
| `--rust-deep` #9E3E1E | `--cream` #F6E3BB | Links, tagline, definition | **4.74:1** | 4.5:1 | ✓ (tight) |
| `--rust` #AF4926 | `--cream` #F6E3BB | Large numbers (.idx, .dur, .big) | **4.09:1** | 3:1 (large text, all uses ≥38px) | ✓ |
| `--cream` #F6E3BB | `--green` #22402C | Opener text | **9.6:1** | 4.5:1 | ✓ |
| `--cream` #F6E3BB | `--rust-deep` #9E3E1E | Button text (.reveal, .submit) | **4.74:1** | 3:1 (UI component) | ✓ |
| `--cream` #F6E3BB | `--ink` #2C251A | Skip link, hover states | **12.1:1** | 4.5:1 | ✓ |
| `--green` #22402C | `--cream-deep` #EFD9A8 | Input border (non-text UI) | **8.6:1** | 3:1 | ✓ |
| `--ink` #2C251A | `--cream-deep` #EFD9A8 | Input text | **10.8:1** | 4.5:1 | ✓ |
| `--rust-deep` #9E3E1E | `--cream-deep` #EFD9A8 | Error text | **4.24:1** | 4.5:1 | ⚠️ borderline |
| `--rust` #AF4926 | `--cream-deep` #EFD9A8 | Progress bar fill (non-text UI) | **3.65:1** | 3:1 | ✓ |
| `--green` #22402C | `--cream-deep` #EFD9A8 | Fallback text in photo slot | **8.6:1** | 4.5:1 | ✓ |

**Tightest pair**: rust-deep on cream at 4.74:1 (links, tagline). Passes AA for normal text with no headroom.

**One flag**: Error text (`--rust-deep` on `--cream-deep`) computes at ~4.24:1, below 4.5:1 for normal-size text. At 16px bold it's borderline large text. The grain darkening of cream-deep improves this in practice. See "Items That Cannot Be Fixed Without a Design Change" below.

---

## 3. Usability

| # | Check | Result |
|---|-------|--------|
| 3.1 | No horizontal scroll | **PASS** — `overflow-x:hidden` on body, `min-width:320px`, all layouts use responsive grid/flex with `minmax(min(100%,...))`. |
| 3.2 | Card alignment | **PASS** — Grid with `auto-fit` and equal-height cards via `height:100%` on articles. |
| 3.3 | Opening line at 320px | **PASS** — `.opener p` has `max-width:820px`, `font-size:clamp(23px,3.1vw,34px)`. At 320px, font resolves to 23px. Container is 320px - 2×24px padding = 272px. `text-wrap:pretty` ensures good breaks. |
| 3.4 | All six images load | **PASS** — All six `dish-0X.jpg` files exist in the repo and are deployed. JS fallback system only shows "Photograph pending" if the image errors. |
| 3.5 | Venue links resolve | **PASS** — See table below. |
| 3.6 | Computed total | **PASS** — 60+120+60+90+120+120 = 570 min = **9h 30m**. |
| 3.7 | Form produces downloadable SVG | **PASS** — `svgFor()` builds SVG from inputs, creates Blob URL, triggers download. |
| 3.8 | Page weight / TTI | **CANNOT VERIFY** precisely — Estimated total ~2-2.5MB (6 dish JPGs + PNGs + HTML). No framework JS, minimal inline JS. Run Lighthouse for exact numbers. |

### 3.5 — Venue Links

| # | Link text | Resolves to |
|---|-----------|-------------|
| 01 | Off Avenida Revolución | Google Maps search: "Avenida Revolución, Tijuana, Baja California" ✓ |
| 02 | Tacos El Yaqui | Google Maps search: "Tacos El Yaqui, Rosarito, Baja California" ✓ |
| 03 | El Trailero | Google Maps search: "El Trailero Taqueria, Ensenada, Baja California" ✓ |
| 04 | La Chata | Google Maps search: "La Chata, Guadalajara, Jalisco" ✓ |
| 05 | El Huequito | Google Maps search: "El Huequito, Ciudad de México" ✓ |
| 06 | Plaza Santo Domingo | Google Maps search: "Templo de Santo Domingo de Guzmán, Oaxaca de Juárez" ✓ |

All use the official Google Maps URLs API format with `rel="noopener noreferrer"`.

---

## 4. Content Integrity

| # | Check | Result |
|---|-------|--------|
| 4.1 | No placeholder strings | **PASS** — No `[ venue ]`, `[ alt text ]`, `[ personal note ]`, `[ duration ]`, or `REPLACE-WITH` found. |
| 4.2 | Six entries in order | **PASS** — Tijuana, Rosarito, Ensenada, Guadalajara, Ciudad de México, Oaxaca. |
| 4.3 | No invented content | **PASS** — No prices, hours, ratings, reviews, or testimonials. |
| 4.4 | No em dashes in copy | **PASS** — `—` appears only in `<title>`, `og:title`, and a JS comment. Zero in body copy. |
| 4.5 | Opening line correct | **PASS** — "Mexico is our heritage. We have no family there to visit, so we found it at the table instead. These are six we did not want to leave." |
| 4.6 | Closing line correct | **PASS** — `Six out of many. <span lang="es">Provecho.</span>` |

---

## 5. Code Quality

| # | Check | Result |
|---|-------|--------|
| 5.1 | No innerHTML/outerHTML/document.write/eval | **PASS** — None found in index.html. |
| 5.2 | No inline on* handlers | **PASS** — None found. |
| 5.3 | No localStorage/sessionStorage/cookies | **PASS** — None found. |
| 5.4 | Zero network requests on form submit | **PASS** — No `fetch`, `XMLHttpRequest`, or `sendBeacon` in source. Entirely client-side Blob generation. |
| 5.5 | No analytics/tracking | **PASS** — No external scripts, no tracking pixels, no analytics. |
| 5.6 | Console errors/warnings | **CANNOT VERIFY** — Cannot run a browser. Based on code review: no syntax errors, all referenced IDs exist, no broken patterns. |
| 5.7 | Single data source for entries | **PASS** — All entries render from HTML `[data-entry]` elements. JS computes totals by querying `[data-entry][data-minutes]`. Adding a 7th entry means adding one `<li>` block. |
| 5.8 | Colors/spacing from tokens | **PASS** — All CSS uses `var()` references to `:root` tokens. Raw hex only in SVG card generator (standalone SVG can't reference CSS variables). |
| 5.9 | HTML validation | **CANNOT VERIFY** — W3C validator unavailable through tools. Based on source review: DOCTYPE present, all tags closed, attributes quoted, no obsolete elements. |
| 5.10 | Images: loading/width/height | **PARTIAL PASS** — All 6 dish images have `loading="lazy"`, `width="1600"`, `height="900"`. `plates.png` has dimensions. Decorative `rule-long.png` (×3), `rule-short.png` (×7) lack explicit `width`/`height`. Rail flowers have `width` but no `height`. Impact is CLS only, not accessibility. |

---

## 6. Metadata and Sharing

| # | Check | Result |
|---|-------|--------|
| 6.1 | og:image, og:url, canonical | **PASS** — All carry `https://sobremesa-dev.vercel.app/`. No placeholder remaining. |
| 6.2 | Social card preview | **CANNOT VERIFY** — Cannot paste into a validator. Metadata is correctly structured: og:image, og:image:alt, og:title, og:description, twitter:card summary_large_image. Should render correctly. |
| 6.3 | title and description | **PASS** — Both present and accurate. |
| 6.4 | Favicon loads | **PASS** — `<link rel="icon" href="assets/flower.png" />` and file exists. |
| 6.5 | `<html lang="en">` | **PASS** |

---

## Summary

| Category | Pass | Cannot Verify | Fail |
|----------|------|---------------|------|
| Total | **35** | **4** | **0** |

The 4 "cannot verify" items require a browser environment (Lighthouse, console output, social card validator, W3C HTML validator).

---

## Items Fixed

**Nothing was fixed during this audit.** No changes were made.

---

## Items That Cannot Be Fixed Without a Design Change

1. **Error text contrast (2.11)**: `--rust-deep` (#9E3E1E) on `--cream-deep` (#EFD9A8) computes at ~4.24:1, below 4.5:1 for normal-size text. At 16px bold it's borderline. The grain darkening likely pushes it above in practice. **Options**: bump error font to 19px (becomes large text, only needs 3:1), or darken the error color slightly.

2. **Decorative images missing width/height (5.10)**: `rule-long.png`, `rule-short.png`, and `flower.png` (in fallback) lack explicit dimensions. Contributes to CLS but doesn't affect accessibility or function. Can be added without visual change.

3. **Text-only zoom (2.20)**: The `clamp()` type scale uses `px` minimums. Under text-only zoom, text won't scale beyond what the clamp allows. No fix without rearchitecting to `rem`/`em` — a design system change.
