# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

`financial-automata` — the marketing landing page for **Financial Automata**, the real
personal-finance app that lives at `~/dev/financial_planner` (FastAPI + React + PostgreSQL).
The app ingests bank/broker statement exports (CSV/Excel) and organizes them into net worth,
cash flow, spending, holdings, and budget projections. This site is a single self-contained
file: **`index.html`** with inline CSS and vanilla JS. No build step, no framework, no runtime
dependencies.

Deployed to GitHub Pages from `main` (root): https://nlifors.github.io/financial-automata/

## Develop & preview

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

There is no test/lint/build pipeline — editing `index.html` and reloading is the loop.

## Architecture notes

Everything lives in `index.html`, organized top-to-bottom as: `:root` CSS variables →
component styles → responsive `@media` blocks → markup sections (nav, hero, spec band,
how-it-works, features, privacy, get-started, CTA, footer) → one IIFE `<script>`.

The voice is **concrete and confident**: the page demonstrates the product (a mock dashboard,
an import toast, a keyword-rule chip) instead of making vague claims. Claims discipline —
only state things the app actually does (auto-detection of 3 statement types, content-hash
dedup, 19 editable keyword categories, net-worth snapshots, 3–12-month projections,
per-user isolation, self-hosting). No invented integrations, pricing, or testimonials.
The demo numbers in the hero card are illustrative and labeled as such in the footer.

Conventions worth preserving when editing:
- **Design tokens mirror the app** (`financial_planner/frontend/src/styles.css`): navy
  `--bg #0b1020`, `--surface #16203a`, brand blue `--brand #4f8cff`, violet `--violet
  #7c5cff`. **Cyan `--cyan #22d3ee` is "the goal color"** — reserved for the wordmark
  accent, the goal node, eyebrows, and confirmations. Keep it scarce. Change the theme
  in `:root`, not inline.
- **Chart colors are validated.** The donut/categorical steps (`--cat-1..4`: `#4f8cff`,
  `#7c5cff`, `#0891b2`, `#059669`) pass CVD/contrast checks against the dark surface —
  don't swap them for the lighter semantic tints without re-validating.
- **The logo is the app's logo** — directed-graph badge (blue→violet, cyan goal node),
  copied from `financial_planner/frontend/src/components/Logo.tsx` / `public/favicon.svg`.
  Keep them in sync. The wordmark is lowercase `financial` + cyan `automata`.
- **Three fonts, by role:** `--font-display` (Familjen Grotesk) for headings and the
  wordmark, `--font-body` (Schibsted Grotesk) for prose/buttons, `--font-mono`
  (Spline Sans Mono) for data, labels, and terminal copy. Tabular figures via `.num`.
- **JS is feature-detected and motion-aware.** Every animation checks
  `prefers-reduced-motion` and bails to a static end-state. Scroll reveals use
  `IntersectionObserver`.
- **The hero canvas** renders the automaton at work: a directed graph where particles
  (transactions) flow from statement nodes through parse/categorize nodes into a single
  cyan goal node — echoing the logo. Seeded by a deterministic PRNG (no `Math.random`
  for layout), kept `aria-hidden` and masked so it never competes with the copy.

## Tooling (git-ignored, not part of the site)

`record.js` + `playwright-core` (in `node_modules/`) drive headless Chromium to capture
screenshots and a screen recording; output media (`*.png`, `*.mp4`, `*.gif`, `video/`) is
ignored. None of this is needed to run or deploy the site.
