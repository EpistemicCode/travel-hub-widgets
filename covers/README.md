# Quiet Atlas — Cover Generator

Parametric vector cover generator for the **Travel Planning OS** Notion template.
Brand: **Quiet Atlas** · Owner: EpistemicCode · License: proprietary / All Rights Reserved.

---

## Files

| File | Purpose |
|---|---|
| `cover.html` | Renders ONE cover at exact pixel size, selected by `?preset=NAME` |
| `covers.css` | Frame styles + Quiet Atlas design tokens |
| `index.html` | Contact sheet: all 11 presets scaled down in a labeled grid (for approval) |
| `README.md` | This file |

---

## Presets

| Preset | Eyebrow | Title | Size | Glyph |
|---|---|---|---|---|
| `hub` | QUIET ATLAS | Travel Planning OS | 1500×600 | compass |
| `trips` | MODULE · TRIPS | Every trip, one place. | 1500×400 | suitcase |
| `itinerary` | MODULE · ITINERARY | Day by day. | 1500×400 | map-pin |
| `stays` | MODULE · STAYS | Rest easy. | 1500×400 | bed |
| `eats` | MODULE · EATS | Taste the place. | 1500×400 | cup-and-saucer |
| `transit` | MODULE · TRANSIT | Get there. | 1500×400 | paper-plane |
| `packing` | MODULE · PACKING | Pack light. | 1500×400 | checklist |
| `expenses` | MODULE · EXPENSES | Every dollar. | 1500×400 | wallet |
| `documents` | MODULE · DOCUMENTS | Papers, sorted. | 1500×400 | document |
| `contacts` | MODULE · CONTACTS | Help, on hand. | 1500×400 | phone |
| `banner` | QUIET ATLAS | where to next | 1500×300 | none |

---

## How to use

### Preview all covers
Open `index.html` in a browser. Every preset renders at ~480px wide for side-by-side approval.

### Preview one cover
Open `cover.html?preset=NAME` — e.g. `cover.html?preset=trips`.
Defaults to `hub` if `?preset=` is absent.

### Export PNGs
Open `cover.html?preset=NAME` in a headless browser set to the preset's exact viewport, then screenshot:

| Preset group | Viewport (px) | Command example (Puppeteer / Playwright) |
|---|---|---|
| `hub` | 1500 × 600 | `page.setViewportSize({width:1500,height:600})` |
| all modules | 1500 × 400 | `page.setViewportSize({width:1500,height:400})` |
| `banner` | 1500 × 300 | `page.setViewportSize({width:1500,height:300})` |

The cover element is absolutely positioned at `top:0; left:0` with `body { margin:0 }`, so a full-viewport screenshot captures it 1:1 with no whitespace padding.

### Photo upgrade (later)
Each cover's right half is wrapped in `<div class="scene">`. To swap the placeholder vector scene for a real photograph, replace the inner `<svg class="horizon">` with:

```html
<img class="scene-photo" src="your-photo.jpg" alt="">
```

The `.scene-photo` rule (`position:absolute; inset:0; object-fit:cover`) handles cropping automatically.

---

## Design tokens

| Token | Value | Used for |
|---|---|---|
| cream | `#F4EFE6` | Panel background, banner caption |
| ink | `#1B2A3A` | Title, body text |
| terracotta | `#C46A4A` | Rule dot, glyphs, accent |
| sage | `#7A8C7A` | Eyebrow, subtitle |
| brass | `#B8894A` | Section labels (contact sheet) |
| paper-shadow | `#E5DFD2` | Divider hairline, preview borders |
| rule | `#cbb89a` | Hairline rule in panel |

Fonts (Google Fonts CDN — TODO: self-host for production):
- **Fraunces** 400 + italic 400 — display / title / subtitle
- **Inter** 400 / 500 — UI / contact sheet
- **JetBrains Mono** 400 — eyebrow labels

---

## What this is NOT

- Not a widget — these covers are for Notion page headers / Gumroad listing images, not `<iframe>` embeds.
- Not connected to `assets/tokens.css` — cover tokens are self-contained in `covers.css` (different palette from the dark widget theme).
