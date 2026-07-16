# Rabbi story — Hebrew RTL landing page — handoff

A single-page, static Hebrew RTL landing page that preserves the user's original
text verbatim and presents it in a warm, spiritual/editorial visual treatment.

## Files

```
/home/user/workspace/rabbi_story_landing/
├── index.html            # The page. Contains the user's exact text.
├── styles.css            # All styles (palette, type, layout, responsive).
├── preview_desktop.png   # Full-page screenshot at 1280px width (for QA).
├── preview_mobile.png    # Full-page screenshot at 390px width (for QA).
└── HANDOFF.md            # This file.
```

Open `index.html` directly in any browser, or serve the folder with any static
host. No build step, no dependencies beyond two Google Fonts pulled in via
`<link>`.

## Text fidelity

The page text inside the `<article>` is reproduced exactly from the user's
message: punctuation, em-dashes, semicolons, the triple `???` after
"איך חיים ככה", the `**` before the WhatsApp line, the double-space before
"השנייה", the double-space in "שמרגיש  בליבו", and all four URLs (Telegram,
WhatsApp, Bit/Paybox phone, Nedarim Plus).

No headline, kicker, subtitle, meta description, or any other prose was added
inside the page. The browser tab `<title>` is "איך חיים ככה?" (taken from the
body's own question) — this is not visible inside the page itself.

`<br/>` tags reproduce the user's hard line-breaks within paragraphs; blank
lines become new paragraphs. Links are wrapped in `<a>` for clickability but
the visible text of each URL is unchanged. The `**` is wrapped in
`<span class="asterisks">` purely to color it — the characters themselves are
preserved.

## Design decisions

**Aesthetic.** Warm, parchment-like editorial. Aims for a feeling of dignity
and quiet rather than a marketing landing page.

**Palette** (defined as CSS variables at the top of `styles.css`):

| Role            | Hex       | Use                                           |
| --------------- | --------- | --------------------------------------------- |
| `--bg`          | `#f4ecdc` | Outer background (cream)                      |
| `--paper`       | `#fbf5e6` | Card surface                                  |
| `--ink`         | `#2a2418` | Primary body text — warm near-black           |
| `--ink-soft`    | `#4a402d` | Secondary text                                |
| `--teal`        | `#1f5b5e` | Links + pull-quote + WhatsApp card accent     |
| `--teal-deep`   | `#143e41` | Hover state, emphasized block text            |
| `--gold`        | `#b8852a` | Ornaments, asterisks, lede border, underlines |
| `--gold-soft`   | `#d9b46a` | Softer gold accents                           |

The background is a layered gradient — a warm radial wash at the top, a
slightly darker wash at the bottom corner, on a cream gradient base — plus two
fixed blurred "glow" elements to give the page atmosphere without imagery.

**Typography** (loaded from Google Fonts):

- **Frank Ruhl Libre** (serif, weights 400/500/700/900) — used for the lede
  paragraph, the emphasized block ("כל זה לא נעלם..."), and the pull-quoted
  "איך חיים ככה???". Frank Ruhl is a modern Hebrew serif that reads as
  literary/spiritual rather than corporate.
- **Heebo** (sans, weights 300/400/500/700) — used for body paragraphs and the
  links section. Heebo is a clean, friendly Hebrew sans designed for screens.

Body text uses `clamp()` between roughly 16px and 18px so it scales smoothly
between mobile and desktop. The lede and pull-quote scale up to 24px and 38px
respectively at desktop widths.

**Layout.**

- Mobile-first single column, max-width 760px on desktop, centered.
- One card with rounded corners, soft shadow, parchment gradient fill, and a
  1px warm border.
- Gold ornamental dots/lines at the top and bottom of the card act as visual
  bookends in place of a headline.
- The lede paragraph has a `border-inline-start` in soft gold (RTL-aware — it
  appears on the right side in Hebrew).
- The "כל זה לא נעלם..." paragraph is rendered as a centered emphasis card in
  muted teal — the page's only "hero moment".
- "איך חיים ככה???" is a pull-quote: large display weight, teal color, gold
  underline beneath it.
- The four link blocks are rounded cards with a subtle hover lift. The
  WhatsApp card is tinted in muted teal to distinguish the personal channel
  from the broader Telegram channel and the donation links.

**Responsive breakpoints.**

- Below 720px: card padding 40px / 28px; story type at 16–17px.
- 720px+: card padding 56px; story type at 18px.
- 980px+: card padding 64px / 72px.

**Accessibility.**

- `lang="he"` and `dir="rtl"` on `<html>`.
- All text passes WCAG AA contrast (deep ink on cream, deep teal on cream).
- `:focus-visible` outline in gold on all anchors.
- `prefers-reduced-motion` disables hover transitions.
- Print stylesheet strips background and shadows.

## Editing content later

To change the text: edit `index.html`. The content lives between
`<section class="story" id="page-title">` and the `</section>` that closes
`.links`. Paragraphs use `<p>...</p>`. Hard line-breaks inside a paragraph
use `<br/>`.

To restyle without touching content: edit `styles.css`. The palette and font
choices are defined in the `:root { ... }` block at the top — changing those
variables propagates everywhere.

Special classes you can apply to a paragraph:

- `class="lede"` — large serif treatment with the gold side rule.
- `class="emph"` — centered teal emphasis card.
- `class="invite"` — adds a dashed top divider and a little extra space.
- `<span class="pull-quote">...</span>` inside a paragraph — large teal serif
  with the gold underline.

Link blocks are wrapped in `<div class="link-block">`. The accented variant
(currently used for WhatsApp) adds `link-block--accent`.

## How to preview

```
cd /home/user/workspace/rabbi_story_landing
python3 -m http.server 8765
# then open http://localhost:8765/
```

Or just open `index.html` directly in a browser — there is no server-side code.
