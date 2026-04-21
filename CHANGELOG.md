# Changelog

All notable changes to the travel-hub-widgets embed URLs are documented here.
Version is embedded as `<meta name="widget-version">` in each HTML file so you
can curl any widget and verify which release is live.

## [Unreleased]
- GA4 events across revenue widgets (stays/flights/countdown): widget_view, search_intent, affiliate_click, trip_set
- trip_sub2 encoding on outbound Trip.com URLs — enables per-destination revenue breakdown in Trip.com dashboard
- countdown: "Copy for Notion" banner in iframe contexts (honest fix for Notion's sandbox-storage limitation)
- error boundary: no longer triggers on resource/extension noise (only real JS exceptions)

## [1.2.0] — 2026-04-21
### Added
- nowin: city selection now persists across refresh via URL param + localStorage
- nowin: "↺ auto" button to clear saved city and re-detect
- nowin: snap-to-nearest-city from 80-entry CITIES list for accurate weather
- GA4 (G-1WH2JWQLZB) on index.html directory page only (widgets stay cookieless)
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
