# Portfolio site — PriceScan Cyprus case study

A static portfolio site for MP's senior-PM job search, built around the Price Comparison
Tool project as the flagship case study.

## Structure

```
portfolio-site/
├── index.html        Personal home: positioning, project teaser, experience, contact
├── case-study.html   Flagship case study: problem → discovery → execution → decisions → data → trust
├── backlog.html      Interactive, filterable view of all 37 backlog items
├── styles.css        Shared stylesheet (no build step, plain CSS)
├── data/
│   └── backlog.js    Backlog dataset (plain JS array; loaded via <script>, works from disk)
├── DEPLOYMENT.md     Step-by-step guide: GitHub → Vercel → custom domain
└── PLACEHOLDERS.md   Checklist of personal details to fill in before publishing
```

## Design decisions

- **No framework, no build step.** Plain HTML/CSS/JS. Anyone can edit it, Vercel serves it
  as-is, and nothing can break in a dependency update. Deliberate for a portfolio that must
  outlive the job search.
- **Data as a plain JS file, not fetched JSON.** `data/backlog.js` loads via a `<script>` tag
  so the site works when opened directly from disk (double-click `index.html`) — no local
  server needed for previewing.
- **Content traceability.** Every number and claim on the site traces to the app repo:
  `docs/README.md` (ticket index), git history (65 commits from 2026-06-12), and
  `scripts/` (importer outputs). If the project moves on, update `data/backlog.js`
  and the metric bands in `index.html` / `case-study.html`.

## Content sources

| Claim on site | Source |
|---|---|
| 47 ticketed items | `price-comparison-app/docs/README.md` + PCT-001–004 (pre-docs-folder) |
| 65+ production releases | git history (65 commits to main, each auto-deploying via Vercel) |
| 1,666 / 9,005 / 455 import counts | `scripts/alphamega*` commit, `supermarketcy-done.json`, `wolt-metro-done.json` |
| $3.06 → $1.45 cost/user/month | `docs/PCT-033-drop-catalog-from-scan-prompt.md` |
| Identity model / decisions | PCT-016, 029, 036/037, 038, 039, 044, 045, 046 write-ups |

## Editing

- Backlog items: edit `data/backlog.js` (one object per item; themes drive the filter buttons).
- Metrics: the `.metrics` blocks near the top of `index.html` and `case-study.html`.
- Colors/typography: CSS variables at the top of `styles.css`.

## Deliberately excluded

**Timeline/duration framing** — at MP's request the site makes no duration claims
("28 days", "4 weeks", week-based timeline, visible ticket dates). Delivery is framed
as four *phases*; backlog dates exist in `data/backlog.js` but are not rendered.
Don't reintroduce dates or speed claims. Also excluded:

Scraping mechanics (bot-protection workarounds) are not described on the site — importers
are presented as "automated catalog importers" only. Keep it that way on a public site.
