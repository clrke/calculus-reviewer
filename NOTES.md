# Calculus Reviewer — Project Notes

This repo is the single source of truth (live at
https://clrke.github.io/calculus-reviewer/). It used to be a subfolder inside
the private `saint-expeditus` monorepo; consolidated here on 2026-09-12 so
there's one copy to edit instead of two that can drift.

## Deliverables (current)
- `Calculus-Midterm-Reviewer-Corrected.pdf` — cheat sheet + errata + 17-problem
  worked practice exam, combined into one printable PDF. Supersedes the
  original slide deck (3 verified errors fixed — see the PDF's Errata section).
- `index.html` — standalone, randomized-every-attempt practice quiz (4 levels:
  mix & match → single-rule blanks → 2-layer combined → 3-layer combined).
  Math verified against 7,500+ numeric derivative cross-checks; UI
  functionally tested end-to-end in real Chrome, both locally (`file://`) and
  against the live Pages deployment.

## Dropped (2026-09-12)
`CHEAT-SHEET.md`, `ERRATA.md`, `PRACTICE-EXAM.md` — removed before deploy.
Their content was fully absorbed into the combined PDF above; keeping both
was redundant and the PDF is the one actually meant for studying/printing.

## Deferred decision — quiz score persistence
**Status: on hold, resume on request.**

Question: should `index.html` persist best scores across browser sessions
(e.g. via `localStorage`), instead of the current in-memory-only,
per-page-load scoring?

Investigated 2026-09-12:
- Confirmed via headless Chrome test that `localStorage` works fine under the
  `file://` protocol for this exact file (write/read/remove all succeeded).
- Now that the quiz is deployed to GitHub Pages (real `https://` origin), the
  `file://`-specific shared-origin caveat is moot — a Pages-hosted origin is
  a normal, standard, per-site origin. This removes the main technical
  complication and makes revisiting this a lower-risk, mostly-cosmetic
  addition than it would have been for the offline-only version.
- Still untested in Safari/Firefox specifically, and incognito/private
  windows won't persist it regardless (inherent to `localStorage`, not
  specific to this app).

Net: no hard blocker, small implementation (namespaced key +
`JSON.stringify`/`parse` around the existing `bestScores` object in the UI
script). Parked at user's request rather than a technical concern.
