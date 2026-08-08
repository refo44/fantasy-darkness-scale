# The Fantasy Darkness Scale

A 1–10 index scoring 100 fantasy books, anime, games, and films from cozy hope to grimdark
despair, weighted across seven criteria (structural despair, limited heroism, moral cynicism,
structural corruption, redemption difficulty, narrative acceptance of injustice, and explicit
darkness).

**Live site:** https://fantasydarknessscale.site/ (defaults to English, with an ES/EN switcher
in the top-right corner)

- `/` — English
- `/es/` — Spanish (La Escala de Oscuridad en Obras de Fantasía)

## Contents

- `index.html`, `es/index.html` — the static pages (no build step)
- `CNAME` — custom domain for GitHub Pages (fantasydarknessscale.site)
- `Fantasy_Grimdark_Scale_v2_WIP.xlsx` — the scored source data backing the live site above
  (Methodology, Evaluations, and Summary sheets), under the v2 methodology: interval-based
  tiering and a 0-4 integer scale per criterion for reproducibility — see its Methodology sheet
  for the formula and criteria anchors, and `ADDITIONS_LOG.md` for the rationale. All 100 catalog
  works are scored (filename kept as "WIP" since new works are still added over time)
- `og-en.jpg`, `og-es.jpg` — Open Graph/Twitter Card preview images, referenced from each
  page's `<head>`
- `ADDITIONS_LOG.md` — tracks new works being scored and added to the scale over time
- `CRITERIA_THEORY.md` — theoretical grounding for the 7 scoring criteria: what each one is a
  construct of, and the low/high polarity each represents
- `SCORING_RECORD.md` — full per-work v2 scoring analysis (all 7 criteria with reasoning,
  weighted/final score, tier) for every rescored title
- `TIER_GUIDE.md` — descriptive guide to what each of the scale's 10 tiers actually contains,
  with representative examples from the current catalog

## License

This project is dual-licensed, because the code and the content serve different purposes:

- **Source code** (HTML, CSS, JavaScript) — [MIT](LICENSE). Reuse it however you like,
  including commercially.
- **Content** (the scale, criteria, scores, evaluations, and written text in both
  languages, plus the scored spreadsheet) — [CC BY-NC-SA 4.0](LICENSE-CONTENT.md).
  Share and remix it non-commercially with attribution; commercial use requires
  permission.

Full terms and scope: [LICENSE](LICENSE) and [LICENSE-CONTENT.md](LICENSE-CONTENT.md).
