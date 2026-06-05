# Incoming Raider FAQ

A searchable, single-page FAQ for incoming students at Regis Jesuit High School —
tech, schedules, classes, clubs, wellbeing, and "who do I ask?" — in the RJEdTech
"Raider shell" house style. No build step or server is needed to host it.

**Live site:** `https://rjedtech.github.io/<repo-name>/`

## What's in this repo

| File / folder        | What it is                                                        | Needed to host? |
|----------------------|-------------------------------------------------------------------|-----------------|
| `index.html`         | The whole site — content, search, styling, logo + watermark baked in | **Yes** |
| `favicon.ico`        | Browser tab icon (fallback)                                       | Optional (icon only) |
| `favicon.svg`        | Browser tab icon (modern)                                         | Optional (icon only) |
| `favicon-32.png`     | Browser tab icon (32px)                                           | Optional (icon only) |
| `apple-touch-icon.png` | Home-screen icon on iOS                                         | Optional (icon only) |
| `docs/*.md`          | The seven content pages — **the source of truth** for every answer | No (source only) |
| `build_site.py`      | Regenerates `index.html` from the markdown                        | No (tooling) |
| `chrome_assets.py`   | The official RJ logo + shield watermark (data-URIs) used by the builder | No (tooling) |
| `README.md`          | This file                                                         | No |

Only `index.html` is required for the live site. The four favicon files just give
the browser-tab icon; everything else (logo, watermark, fonts loaded from Google
Fonts) is already embedded or loaded over the web. The `docs/`, `build_site.py`, and
`chrome_assets.py` files are kept here so the FAQ stays editable — they aren't served.

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

## Notes

- **Freshness:** the page shows a "compiled on <date>" banner, and any answer drawn from a
  prior-year source is tagged in amber. Re-confirm time-sensitive details (dates, staff,
  schedules) against My RJ each year and rebuild.
- **Feedback:** the footer links a Microsoft Form for reporting a problem or suggesting a question.
- Built and maintained by the Office of Educational Technology.
