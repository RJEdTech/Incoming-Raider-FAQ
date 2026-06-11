# Incoming Raider FAQ

A searchable, single-page FAQ for incoming students at Regis Jesuit High School —
tech, schedules, classes, clubs, wellbeing, and "who do I ask?" — in the RJEdTech
"Raider shell" house style. The page is **trilingual (English, Spanish, and Tigrinya)**
with an in-page language switcher, and includes a quiet, collapsible **support & crisis**
panel near the top. No build step or server is needed to host it.

**Live site:** `https://rjedtech.github.io/<repo-name>/`

## What's in this repo

| File / folder        | What it is                                                        | Needed to host? |
|----------------------|-------------------------------------------------------------------|-----------------|
| `index.html`         | The whole site — content, search, all three languages, the support panel, styling, logo + watermark baked in | **Yes** |
| `favicon.ico`        | Browser tab icon (fallback)                                       | Optional (icon only) |
| `favicon.svg`        | Browser tab icon (modern)                                         | Optional (icon only) |
| `favicon-32.png`     | Browser tab icon (32px)                                           | Optional (icon only) |
| `apple-touch-icon.png` | Home-screen icon on iOS                                         | Optional (icon only) |
| `docs/*.md`          | The seven content pages — **the source of truth** for every answer | No (source only) |
| `build_site.py`      | Regenerates `index.html` from the markdown                        | No (tooling) |
| `chrome_assets.py`   | The official RJ logo + shield watermark (data-URIs) used by the builder | No (tooling) |
| `README.md`          | This file                                                         | No |

Only `index.html` is required for the live site. The four favicon files just give
the browser-tab icon; everything else (logo, watermark, all three languages, the
support panel, fonts loaded from Google Fonts) is already embedded or loaded over the
web. The `docs/`, `build_site.py`, and `chrome_assets.py` files are kept here so the
FAQ stays editable — they aren't served.

## Deploy (one time)

1. Put `index.html` (and the four favicon files) in the **root** of this repo.
2. **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)` → Save.**
3. Wait ~1 minute. The site is live at `https://rjedtech.github.io/<repo-name>/`.

No GitHub Actions or build workflow is needed — `index.html` is already built.

## Update the content

1. Edit the relevant file in `docs/` (e.g. `docs/academics.md`). Each entry looks like:

   ```
   ### Q: Your question here?

   The answer, in plain language. **Bold** for emphasis, [links](https://example.com) as needed.

   **Where to go:** [Tile or page name](https://link-to-the-resource)

   <!-- source: where this came from; tags: search, keywords, here -->
   ```

   Phone numbers and email addresses become tap-to-call / tap-to-email automatically.

2. Rebuild the page:

   ```
   python3 build_site.py
   ```

   This reads the seven `docs/*.md` files and rewrites `index.html`.

3. Commit `index.html` (and your edited markdown). The live site updates within a minute.

> **Before you rebuild — direct edits vs. the builder.** Some things (the language
> blocks and the support/crisis panel) live as constants in `index.html`. If you
> hand-edit one of those — for example a translated label or the panel styling — make
> the same change wherever `build_site.py` defines it, or the next
> `python3 build_site.py` will overwrite your edit. Confirm where the language blocks
> and the support panel are defined in the builder before rebuilding.

## Languages

- The page ships in **English, Spanish, and Tigrinya**, switchable from the header.
- When Tigrinya is selected, a **translation note** appears automatically, since those
  strings are machine-drafted and pending review.
- Interface strings (buttons, labels, notices) live in the `I18N.en` / `I18N.es` /
  `I18N.ti` blocks in `index.html`. They're plain Unicode between quotes — no HTML
  entities needed; just escape any literal `"` as `\"`.
- **Review chain for translated copy:** Tigrinya — **Nathan Haile (Admissions)**;
  Spanish — **Naileth Talbot and the Spanish teachers**. Route new or changed labels
  through them before publishing.

## Support & crisis panel

- A collapsible box near the top of the page links **988**, **Crisis Text Line**
  (text HOME to 741741), **Safe2Tell**, a trusted adult at school, and **Care Solace**.
- It's intentionally low-key — neutral card, no animation, calm "support" wording
  rather than alarm — so a logistics FAQ doesn't read as an emergency page. Keep that
  tone if you edit it.
- The short header label is the `crisis_btn` string in each language block; the
  expanded contents are in the `CRISIS_I18N` block.

## Notes

- **Freshness:** the page shows a "compiled on <date>" banner, and any answer drawn from a
  prior-year source is tagged in amber. Re-confirm time-sensitive details (dates, staff,
  schedules) against My RJ each year and rebuild.
- **Feedback:** the footer links a Microsoft Form for reporting a problem or suggesting a question.
- Built and maintained by the Office of Educational Technology.
