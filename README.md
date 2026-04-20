# travel-hub-widgets

Hand-crafted widgets for the **Travel Planning OS** Notion template — live hotel/flight search, local time + weather, trip countdown. Designed to be **embedded directly into any Notion page via `/embed`**.

> ⚠️ These widgets are free to **embed** in your own Notion pages. They are **not** free to copy, fork, redistribute, or rehost. See [LICENSE](./LICENSE).

## How to use

Paste the widget URL into Notion using the `/embed` command. That's it — no download, no signup, no account.

```
Type /embed in Notion → paste the URL → resize to the size shown below
```

| Widget | Embed URL | Size |
|---|---|---|
| **Stays search** (hotels) | `https://epistemiccode.github.io/travel-hub-widgets/stays.html` | 480 × 360 |
| **Flights search** | `https://epistemiccode.github.io/travel-hub-widgets/flights.html` | 480 × 380 |
| **Now in …** (time + weather) | `https://epistemiccode.github.io/travel-hub-widgets/nowin.html` | 380 × 260 |
| **Trip countdown** | `https://epistemiccode.github.io/travel-hub-widgets/countdown.html` | 340 × 260 |

## Pre-configure with query params

Each widget accepts URL query parameters so you can pre-fill defaults for your trip:

```
# Stays in Bali, 1-week window, 2 adults
stays.html?city=Bali&checkin=2026-05-01&checkout=2026-05-08&adults=2

# Flight from Shanghai to Bali, round-trip
flights.html?from=SHA&to=DPS&depart=2026-05-01&return=2026-05-08&adults=2&type=RT

# Now-in Ubud, Bali (local time + live weather)
nowin.html?lat=-8.5069&lon=115.2625&tz=Asia/Makassar&place=Ubud

# Countdown to a specific trip
countdown.html?to=2026-05-02T21:40&dest=Ubud,+Bali&flight=GA+881
```

If you omit `lat`/`lon` on `nowin.html`, it auto-detects the viewer's location. If you omit the target date on `countdown.html`, it defaults to 30 days out.

## Affiliate disclosure

`stays.html` and `flights.html` link out to Trip.com. When someone clicks through and books, the widget author may earn a referral commission at no extra cost to the traveler. The outbound URLs are direct `trip.com` links — no intermediate redirect, no tracking scripts.

## Data sources

All external APIs used are **free, public, and key-less**:

- **Weather** — [Open-Meteo](https://open-meteo.com) (no signup)
- **Visitor location fallback** — [ipapi.co](https://ipapi.co) (no signup)
- **Time zones** — browser `Intl.DateTimeFormat` (no network)

No analytics, no user tracking, no cookies.

## Terms of use

- ✅ **Embed** these URLs in your Notion pages, blog, documentation, or personal website
- ✅ **Link** to this repository or the widgets
- ❌ **Do not** fork, copy, mirror, rehost, or republish the widget source code
- ❌ **Do not** modify the affiliate identifiers and rehost under your own brand
- ❌ **Do not** bundle these widgets into a commercial product without written permission

See [LICENSE](./LICENSE) for the full terms.

## Contact

Suggestions, partnership inquiries, or commercial licensing: open an issue on this repository.
