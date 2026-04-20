# travel-hub-widgets

Self-contained HTML widgets for the **Travel Planning OS** Notion template. Embeds in any Notion page via `/embed`, hosts free on GitHub Pages.

- Utility widgets: countdown, map, currency, now-in weather, rotating quote
- Affiliate widgets: stays search (Travelpayouts) — more coming

Zero backend, zero build step, zero external JS. Just HTML + a shared CSS token file.

## Quick start (fork & use)

1. Fork this repo to your own GitHub.
2. Enable **GitHub Pages** on `main` branch (Settings → Pages → Deploy from branch → main → `/root`).
3. Open each affiliate HTML file, edit the `CONFIG` block at the top of the `<script>` tag and replace `{{MARKER}}` / `{{TRS}}` / `{{CID}}` with **your** affiliate IDs. (Without this, clicks still work but earn the repo owner's commission — not yours.)
4. Commit + push. Your widgets live at `https://<your-user>.github.io/travel-hub-widgets/<name>.html`.
5. In Notion, type `/embed` on your hub/module page and paste the widget URL. Resize the embed to match the widget's native dimensions (listed in each file's comment header).

## Widget reference

| File | Size | Type | Query params |
|---|---|---|---|
| `countdown.html` | 340×260 | utility | `?to=2026-05-02T21:40&dest=Ubud,+Bali&flight=GA+881` |
| `map.html` | 480×320 | utility | `?stops=Canggu,Ubud&active=Ubud` |
| `currency.html` | 480×320 | utility | `?home=USD&trip=IDR&amount=100` |
| `nowin.html` | 380×260 | utility | `?lat=-8.5&lon=115.2&tz=Asia/Makassar&place=Ubud` |
| `quote.html` | 560×200 | utility | `?accent=%23ff8a5c` |
| `stays.html` | 480×320 | **affiliate** (Travelpayouts) | `?city=Bali&checkin=2026-05-01&checkout=2026-05-08&adults=2` |

## Affiliate disclosure

Affiliate widgets include outbound links to booking partners. The repo owner may earn a commission when you click those links and complete a booking. Forking the repo and swapping the markers makes *you* the earner. No tracking beyond the affiliate partner's own redirect.

## Local preview

```bash
cd travel-hub-widgets
python -m http.server 8000
# open http://localhost:8000/stays.html?city=Bali
```

## License

MIT. Fork freely.
