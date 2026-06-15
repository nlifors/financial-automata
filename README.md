# Financial Automata

Landing page for a (fictional) tech firm building autonomous trading systems.

**Live:** https://nlifors.github.io/financial-automata/

A single, self-contained `index.html` — no build step, no dependencies. Open it in a
browser or serve the directory statically.

## Design

A refined "quant-terminal" aesthetic: deep ink background, an electric-lime *signal*
accent, monospace data readouts, and a fine engineered grid. The brand name drives the
concept:

- A live **elementary cellular automaton (Rule 110)** computes faintly behind the hero —
  a literal nod to *automata*, rendered on a `<canvas>`.
- A Conway's Game of Life **glider** is the logomark.
- A live **signal terminal** cycles LONG / SHORT / FLAT calls with a ticking P&L.
- A self-drawing **equity curve** (SVG `stroke-dashoffset`) with a deliberate drawdown dip.

Type: Bricolage Grotesque (display) · Archivo (body) · JetBrains Mono (data).
Motion respects `prefers-reduced-motion`. Fully responsive.

## Develop

```sh
# any static server works, e.g.
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy

Served from `main` (root) via GitHub Pages.

---

*Financial Automata is a fictional demonstration brand. Nothing here is investment advice;
performance figures are illustrative. See the risk disclosure in the page footer.*
