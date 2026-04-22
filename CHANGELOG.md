# Changelog

All notable changes to the travel-hub-widgets embed URLs are documented here.
Version is embedded as `<meta name="widget-version">` in each HTML file so you
can curl any widget and verify which release is live.

## [Unreleased]

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
