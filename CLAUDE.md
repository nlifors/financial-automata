# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

`financial-automata` — a marketing landing page for a (fictional) firm building autonomous
trading systems. The entire site is a single self-contained file: **`index.html`** with
inline CSS and vanilla JS. No build step, no framework, no runtime dependencies.

Deployed to GitHub Pages from `main` (root): https://nlifors.github.io/financial-automata/

## Develop & preview

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

There is no test/lint/build pipeline — editing `index.html` and reloading is the loop.

## Architecture notes

Everything lives in `index.html`, organized top-to-bottom as: `:root` CSS variables →
component styles → responsive `@media` blocks → markup sections (nav, hero, ticker, stats,
platform, process, performance, strategies, CTA, footer) → one IIFE `<script>`.

Conventions worth preserving when editing:
- **Design tokens** are CSS custom properties on `:root` (`--signal` is the lime accent,
  `--up`/`--down` are the long/short semantic colors). Change the theme there, not inline.
- **Three fonts, by role:** `--font-display` (Bricolage Grotesque) for headings,
  `--font-body` (Archivo) for prose, `--font-mono` (JetBrains Mono) for all data/labels.
- **JS is feature-detected and motion-aware.** Every animation checks
  `prefers-reduced-motion` and bails to a static end-state. Scroll reveals and stat
  count-ups use `IntersectionObserver`.
- **The hero canvas** renders an elementary cellular automaton (Rule 110) — it's decorative
  and brand-thematic (the firm is "Automata"). Keep it `aria-hidden` and low-opacity so it
  never competes with the copy.
- **The equity curve** is generated deterministically in JS (no `Math.random`) so it renders
  identically every load, then animated via `stroke-dashoffset`.

## Tooling (git-ignored, not part of the site)

`record.js` + `playwright-core` (in `node_modules/`) drive headless Chromium to capture
screenshots and a screen recording; output media (`*.png`, `*.mp4`, `*.gif`, `video/`) is
ignored. None of this is needed to run or deploy the site.
