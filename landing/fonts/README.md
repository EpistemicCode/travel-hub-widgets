# Self-hosted fonts — Quiet Atlas landing page

Replace the Google Fonts `<link>` in `landing/index.html` with these self-hosted woff2 files.
All families are OFL (SIL Open Font License) — free to self-host.

## Families to download

| Family         | Weights | Source                                              |
|----------------|---------|-----------------------------------------------------|
| Fraunces       | 400     | https://fonts.google.com/specimen/Fraunces          |
| Inter          | 400, 500| https://fonts.google.com/specimen/Inter             |
| JetBrains Mono | 400, 500| https://fonts.google.com/specimen/JetBrains+Mono   |

## Download steps

1. Visit each Google Fonts URL above.
2. Select the weights listed, click **Download family**.
3. From the zip, extract only the `.ttf` files for the weights you need.
4. Convert to `woff2` with https://cloudconvert.com/ttf-to-woff2 or `fonttools`:
   ```
   pip install fonttools brotli
   fonttools convert Fraunces-Regular.ttf
   ```
5. Place files here as:
   ```
   fonts/
   ├── Fraunces-Regular.woff2
   ├── Inter-Regular.woff2
   ├── Inter-Medium.woff2
   ├── JetBrainsMono-Regular.woff2
   └── JetBrainsMono-Medium.woff2
   ```

## CSS @font-face block (paste into tokens.landing.css, replace Google Fonts link)

```css
@font-face {
  font-family: 'Fraunces';
  src: url('../fonts/Fraunces-Regular.woff2') format('woff2');
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'Inter';
  src: url('../fonts/Inter-Regular.woff2') format('woff2');
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'Inter';
  src: url('../fonts/Inter-Medium.woff2') format('woff2');
  font-weight: 500;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'JetBrains Mono';
  src: url('../fonts/JetBrainsMono-Regular.woff2') format('woff2');
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'JetBrains Mono';
  src: url('../fonts/JetBrainsMono-Medium.woff2') format('woff2');
  font-weight: 500;
  font-style: normal;
  font-display: swap;
}
```

## Preload tags (add to `<head>` above the CSS links)

```html
<link rel="preload" href="fonts/Fraunces-Regular.woff2" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="fonts/Inter-Regular.woff2"    as="font" type="font/woff2" crossorigin>
<link rel="preload" href="fonts/Inter-Medium.woff2"     as="font" type="font/woff2" crossorigin>
```

(JetBrains Mono is below-fold / mono labels only — no preload needed.)

## Perf target

All 5 files combined should be ≤ 120 KB. Subsetting to Latin + Extended-Latin saves ~40%.
Use `pyftsubset` from fonttools if needed:
```
pyftsubset Fraunces-Regular.ttf --unicodes="U+0020-007F,U+00A0-00FF,U+0100-017F" --flavor=woff2 --output-file=Fraunces-Regular.woff2
```
