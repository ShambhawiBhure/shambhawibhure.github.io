# Shambhawi Bhure · Portfolio

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![No Build Tools](https://img.shields.io/badge/build-none%20required-brightgreen?style=flat-square)
![WCAG AA](https://img.shields.io/badge/contrast-WCAG%20AA-success?style=flat-square)

> Personal portfolio for **Shambhawi Baswaraj Bhure**, M.S. Computer Science at Columbia University
> (Dec 2026), previously ML Engineering at Tesla and Software Engineer at Mastercard.

**→ [shambhawibhure.github.io](https://shambhawibhure.github.io/)**

---

## Stack

A single hand-written `index.html`: no framework, no build step, no dependencies. Fonts come from
Google Fonts; everything else is inline. Deployed straight from `main` via GitHub Pages.

The tradeoff is deliberate: nothing to rot, nothing to rebuild, and it loads instantly.

## Structure

```
index.html          Entire site: markup, design tokens, styles, and behaviour
robots.txt          Crawler directives
sitemap.xml         Single-page sitemap
assets/
  favicon.svg        Monogram favicon
  og.jpg             1200x630 social preview card
  shambhawi-560.jpg  Portrait, 1x
  shambhawi-920.jpg  Portrait, 2x (served via srcset)
  shambhawi.jpeg     Source photo, 800x800 (not referenced by the site)
Shambhawi_Baswaraj_Bhure_Resume.pdf
```

## Sections

`Hero` · `About` · `Experience` · `Selected Work` · `Skills` · `Education` ·
`Teaching & Leadership` · `Contact`

## Notes for future edits

**Theme.** Colors are CSS custom properties defined once in `:root` and redefined under
`[data-theme="dark"]`. Change a token, not a rule.

The palette is a neutral base with one slate-blue accent and a muted teal secondary:

| | Light | Dark |
| --- | --- | --- |
| Page / surface | `#fcfcfd` / `#ffffff` | `#0f1117` / `#1a1e28` |
| Ink | `#16181d` | `#f2f3f5` |
| Accent | `#3f5c9a` | `#8ba6e0` |
| Secondary | `#1a6b63` | `#5fc2b8` |

The accent exists as four tokens, and the distinction matters for accessibility:

| Token             | Use                                                         |
| ----------------- | ----------------------------------------------------------- |
| `--accent`        | Decorative fills, borders, and **large** text only (≥24px)   |
| `--accent-text`   | **Small** text; passes WCAG AA 4.5:1 on every background     |
| `--accent-solid`  | Button/badge fills that carry white text                     |
| `--accent-str`    | Hover state for solid fills                                  |

`--sec` / `--sec-lt` are the secondary teal, used for the featured-work badge, project bullets and
the education card rule.

Every text/background pair in both themes is verified at ≥4.5:1 (≥3:1 for large display text),
including colors composited over the `-lt` tints. If you change `--accent`, re-check the small-text
tokens before shipping.

**Theme flash.** A tiny blocking script in `<head>` sets `data-theme` before first paint. Keep it
there; moving it to the end of `<body>` reintroduces a flash of light theme for dark-mode visitors.

**Images.** The portrait is served through `srcset` at 560w/920w. If you swap the photo, regenerate
both sizes and keep the `width`/`height` attributes accurate, or the page will shift while loading.

The displayed box is 460 CSS px wide, so 920w is exactly 2x and needs no upscaling. Always cut from
the largest original available: the 3024x4032 camera file for the current portrait lives in git
history at commit `a4f9e17` (`git show a4f9e17:shambhawi.jpeg > source.jpeg`) rather than in the
working tree, so the repo stays light. Crop to 4:5 first, then resize. `--cropOffset` is `top left`,
and `-c` takes height before width:

```sh
sips -c 2419 1935 --cropOffset 847 847 source.jpeg --out /tmp/crop.jpg    # 4:5, head to waist
sips --resampleHeightWidth 1150 920 -s format jpeg -s formatOptions 50 /tmp/crop.jpg --out assets/shambhawi-920.jpg
sips --resampleHeightWidth  700 560 -s format jpeg -s formatOptions 60 /tmp/crop.jpg --out assets/shambhawi-560.jpg
```

Those quality numbers land both files near 180 KB and 112 KB. The autumn foliage is detailed and
compresses poorly, so check the size after any re-encode instead of assuming.

Keep `aspect-ratio: 4 / 5` in `.hero-photo` matching the files. Do not re-add a `max-height` next to
it; the two fought each other and `object-fit: cover` silently re-cropped the image.

**Social card.** `assets/og.jpg` is referenced by absolute URL in the Open Graph tags, as it has to be,
since scrapers don't resolve relative paths. If the domain changes, update those tags. The card is
generated from an SVG and rasterised with `sips -s format png card.svg --out card.png`; keep its
colors in sync with the tokens above.

**Icons.** All icons are inline 24×24 stroke SVGs that inherit `currentColor`: no icon font, no
emoji. Match `stroke-width` (1.6–1.8) when adding more.

**Accessibility.** Skip link, visible focus rings, `aria-expanded` / `aria-pressed` on the toggles,
`prefers-reduced-motion` honoured, and content stays visible without JavaScript. Worth preserving.

**Content.** The résumé PDF and the page content are maintained separately; when the résumé changes,
update `index.html` and the JSON-LD `Person` block to match.

---

<p align="center"><strong>Shambhawi Baswaraj Bhure</strong> · New York, NY</p>
