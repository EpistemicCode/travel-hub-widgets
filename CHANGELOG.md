# Changelog

All notable changes to the travel-hub-widgets embed URLs are documented here.
Version is embedded as `<meta name="widget-version">` in each HTML file so you
can curl any widget and verify which release is live.

## [Unreleased]

## [1.5.1] — 2026-04-23
### Fixed
- **flights.html + stays.html:** Expedia deep-links were routed through `prf.hn/click/camref:.../destination:...` (generic Partnerize), which redirected to Expedia's homepage instead of the search page. Switched to Expedia Group Creator Network's native endpoint: `https://expedia.com/affiliate?siteid=1&landingPage=<encoded-target>&camref=1100l5Jqrn`. Verified from EG widget's own output format.
- **flights.html:** Expedia Flights-Search was concatenating adults + children counts (e.g. 6 adults + 1 child → 16 adults). Root cause: Expedia's `passengers` parser accepts `children:N` (count) OR `children:age,age` (ages list) ambiguously — when `,adults:6` followed `children:1`, the parser read `1,adults:6` as an ages list and folded values into adults. Fix: drop `children` from the Expedia URL entirely; send `adults:N,infantinlap:N` only. Trip.com URL still honors children cleanly. Children label in UI gets an asterisk tooltip explaining the limitation.
- **flights.html:** Restored `fromType:AIRPORT,toType:AIRPORT` in leg segments — required for Expedia to resolve bare IATA codes. An earlier iteration removed them on a false hypothesis.
- **flights.html:** Param order in Flights-Search URL matched to verified working reference: leg1, leg2, options, fromDate, toDate, d1, d2, passengers.

### Added
- **test-flight.html** — local-only side-by-side comparison page. Embeds EG's official search widget alongside the custom flights widget so URL output can be diffed against ground truth. Not linked from index.html, not for public use.
- Console log on Expedia button clicks (`[stays→expedia]`, `[flights→expedia]`) — kept in as a permanent diagnostic; no PII, helps future debugging without a rebuild.

### Notes
- Affiliate attribution now routes through creator.expediagroup.com (EG Creator Network), not Partnerize. `camref=1100l5Jqrn` is the correct credential for this account.
- `pubref` dropped — EG Creator's `/affiliate` endpoint uses `camref` alone. Per-destination reporting will need to come from `creativeref`/`adref` in a future iteration once those IDs are issued from the EG dashboard.

## [1.5.0] — 2026-04-22
### Added
- **stays.html + flights.html:** Expedia (Partnerize) added as the primary affiliate — user clicks the accent "Search on Expedia →" button, falls back to secondary "or try Trip.com →" button. Two revenue streams from one form.
- New GA param `provider` on `search_intent` and `affiliate_click` events (`'expedia'` or `'tripcom'`) — lets you A/B-compare which affiliate converts per destination in GA4 Explore.
- Expedia deep-links wrapped in Partnerize click tracking: `https://prf.hn/click/camref:1100l5Jqrn/pubref:<slug>/destination:<encoded-target>`
- Agoda partner verification meta tag in `index.html` (pending site verification from Agoda dashboard).

### Changed
- Custom dimension registration: add `provider` to GA4 Admin custom-dimensions list.

## [1.4.0] — 2026-04-22
### Added
- **map.html** — stylized route-map widget (480×320, fluid). Geocodes stops via Open-Meteo, renders dashed coral polyline + pulsing dot on active stop, tap opens Google Maps directions. Includes "Find stays in {active}" Trip.com affiliate link with `trip_sub2=map_<slug>` attribution.
- GA4 events on map: `widget_view`, `map_open`, `stays_from_map`. New custom dimension: `stop_count`.
- countdown: empty-state error line (`#set-err`) replaces `alert()` — Notion's iframe sandbox silently blocks modals.
- countdown: past-date validation with `min` attribute + inline red error.

### Changed
- countdown: setup form compacted (fits inside native 260px iframe without clipping the Set-trip button), `overflow-y:auto` safety net.
- countdown: immediate view transition on Set trip — previously the iframe banner blocked the transition inside Notion. Now a dismissable copy-URL toast overlays the countdown.
- countdown: ✎ Edit button moved to top-left to avoid Notion's comment button in the top-right corner.
- countdown: TIERS mood array hoisted above init to fix TDZ ReferenceError when loading from URL params.
- Error boundary scoped to `OWN_FILE` only — no longer triggers on gtag/extension/third-party noise.

## [1.3.0] — 2026-04-21
### Added
- GA4 events across revenue widgets (stays/flights/countdown): widget_view, search_intent, affiliate_click, trip_set
- trip_sub2 encoding on outbound Trip.com URLs — enables per-destination revenue breakdown in Trip.com dashboard
- countdown: "Copy for Notion" banner in iframe contexts (honest fix for Notion's sandbox-storage limitation)
- error boundary: no longer triggers on resource/extension noise (only real JS exceptions)

## [1.2.0] — 2026-04-21
### Added
- nowin: city selection now persists across refresh via URL param + localStorage
- nowin: "↺ auto" button to clear saved city and re-detect
- nowin: snap-to-nearest-city from 80-entry CITIES list for accurate weather
- GA4 (G-D8GYSB22FR) on index.html directory page only (widgets stay cookieless)
- affiliate_click events on stays + flights Search buttons (no-op unless host page has gtag)
- ipapi.co fetch now has a 3s timeout so blocked/slow connections fall through fast
- Global error boundary: widgets show a graceful offline card instead of breaking
- offline.html standalone error page

### Changed
- All 4 widgets rewritten to fill their iframe container (no more whitespace or scrollbars in Notion)

## [1.1.0] — 2026-04-20
### Added
- stays.html — Trip.com hotel search deep-link with full parameter set
- flights.html — Trip.com flight search with IATA airport datalist
- nowin.html — local time + Open-Meteo weather
- countdown.html — trip countdown widget
- index.html — directory page with live widget previews
- Proprietary license with embed-only grant

## [1.0.0] — 2026-04-19
### Added
- Initial repo scaffold, design tokens, /build-widget skill
