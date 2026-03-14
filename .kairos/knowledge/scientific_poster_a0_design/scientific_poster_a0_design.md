---
title: "Scientific Poster A0 Design Guide"
tags: [poster, A0, design, visualization, scientific-communication, PDF]
created: "2026-03-03"
source: "L2 poster_redesign_v2 (session_20260303_071600_64ed9950)"
version: "1.0"
---

# Scientific Poster A0 Design Guide

Lessons learned from iterative poster design for academic conferences. A0 portrait (841mm × 1189mm).

## Layout Principles

### Structure: 2-Column + Full-Width Panels
```
┌─────────────────────────────────┐
│  HEADER (title, authors, logos) │
├────────────────┬────────────────┤
│  LEFT COLUMN   │  RIGHT COLUMN  │
│  (Methods &    │  (Key findings │
│   main results)│   & validation)│
├────────────────┴────────────────┤
│  FULL-WIDTH: Key Findings + Ref │
└─────────────────────────────────┘
```

- A0 portrait comfortably fits **6-7 figures** with moderate text
- Full-width bottom section must be **short** (findings only) — tall bottom panels steal column space
- Footer is expendable — header already carries author/affiliation info
- Use `flex: 1` on last section in each column to absorb remaining space

### Space Management
- **`overflow: hidden` on a fixed-size container is dangerous** — content silently disappears with no visual warning
- All section panels should use `flex-shrink: 0` except the last one per column
- Constrain figure heights with `max-height` when vertical space is tight (e.g., 150mm for secondary figures)
- When content overflows: reduce figure `max-height` first, then trim text — never remove figures

## Text Density

### Sweet Spot per Section
- **3-5 sentences** of explanatory text
- **1 figure** (primary visual)
- **1 key-box or compact table** (supporting evidence)

### Common Mistakes
| Mistake | Symptom | Fix |
|---------|---------|-----|
| Too much text | "Report on a wall" | Cut to 3-5 sentences, let figures speak |
| Too little text | Empty space, figures feel disconnected | Restore context sentences — empty space is worse than moderate text |
| Over-cutting in iteration | Pendulum swings: full → sparse → restore | Make small incremental cuts, check PDF after each |

### Iterative Balance Process
1. Start with full text from the report/paper
2. Cut to ~50% — keep only what a 1-minute reader needs
3. Check PDF output for overflow or empty space
4. Adjust: restore or trim ±1-2 sentences per section
5. Repeat until balanced

## Font Sizes for A0 (reading distance ~1m)

| Element | Recommended Size | Notes |
|---------|-----------------|-------|
| Title (h1) | 48px | Bold, white on dark header |
| Author names | 32px | |
| Affiliation | 26px | Lighter weight/opacity |
| Section headings (h2) | 32px | White on dark blue banner |
| Sub-headings (h3) | 26px | Colored, with bottom border |
| Body text (p, li) | **24px minimum** | Critical — smaller is unreadable at 1m |
| Equations | 30px | Serif font, bold, centered box |
| Equation notes | 21px | Muted color |
| Tables (body) | 21-22px | |
| Table headers | 20-21px | |
| Key/warning boxes | 22px | |
| Figure captions | 20px | Italic, muted color |
| References | 19px | Compact inline format |
| Hero statistics | 36-38px | Extra bold, color-coded |

## Visual Elements

### Hero Numbers
Large, bold, color-coded statistics that draw attention:
- **Positive results**: green (`#2e7d32`)
- **Negative/warning results**: red/orange (`#bf360c`)
- **Neutral/informational**: dark blue (`#1a3a6b`)

Use for: p-values, AUROC scores, percentages, odds ratios.

### Summary Strips
Horizontal row of color-coded badges summarizing a key classification:
```
[6 Nonlinear] [4 Linear] [7 Inconclusive]
```
Place immediately after the main results figure.

### Key Boxes (green) / Warning Boxes (orange)
- Key boxes: 2-3 bullet findings with bold highlights
- Warning boxes: caveats and limitations (shows intellectual honesty)
- Keep titles short: "Reframing", "Insight", "Implication"

### Compact Tables
- Use for side-by-side method comparisons (3-5 rows max)
- Highlight best values with bold green (`.highlight` class)
- Smaller font than body text (20-21px)

## Naming Conventions

| Context | Better Term | Worse Term | Why |
|---------|-------------|------------|-----|
| Poster bottom | "Key Findings" | "Key Contributions" | Audience wants discoveries, not self-assessment |
| Limitations | "Critical Finding" | "Limitation" | Frame honestly but positively |
| Summary | "Key Findings" | "Conclusions" | Posters are findings-driven, not argument-driven |

## PDF Generation

### Chrome Headless — Does NOT Work for Large Paper
Chrome headless `--print-to-pdf` with `--paper-width`/`--paper-height` **silently ignores** custom sizes beyond standard formats. Output defaults to Letter/A4.

### Puppeteer — Reliable Solution
```javascript
// convert_to_pdf.mjs
import puppeteer from 'puppeteer';
const browser = await puppeteer.launch({ headless: true });
const page = await browser.newPage();
await page.goto(`file://${htmlPath}`, { waitUntil: 'networkidle0' });
await page.pdf({
  path: pdfPath,
  width: '841mm',    // A0 width
  height: '1189mm',  // A0 height
  printBackground: true,
  margin: { top: 0, right: 0, bottom: 0, left: 0 },
  preferCSSPageSize: false,  // Use explicit size, not @page CSS
});
await browser.close();
```

**Key**: `preferCSSPageSize: false` + explicit `width`/`height` is the reliable combination.

### Verification
```bash
# Check PDF page dimensions (Node.js)
node -e "
const fs = require('fs');
const buf = fs.readFileSync('poster.pdf');
const str = buf.toString('latin1');
const m = str.match(/\/MediaBox\s*\[([\d.\s]+)\]/);
if (m) { const v = m[1].trim().split(/\s+/); 
  console.log((v[2]/72*25.4).toFixed(0)+'mm ×', (v[3]/72*25.4).toFixed(0)+'mm'); }
"
# Expected: 841mm × 1189mm
```

## Standard Paper Sizes Reference

| Size | mm | inches | points |
|------|-----|--------|--------|
| A0 | 841 × 1189 | 33.11 × 46.81 | 2384 × 3370 |
| A1 | 594 × 841 | 23.39 × 33.11 | 1684 × 2384 |
| A2 | 420 × 594 | 16.54 × 23.39 | 1191 × 1684 |

## Checklist Before Printing

1. Open HTML in browser — visual check for overflow, gaps, alignment
2. Generate PDF with Puppeteer (not Chrome CLI)
3. Verify PDF is 1 page, correct dimensions (841 × 1189 mm)
4. Check all figure paths resolve (relative `../figures/`)
5. Print-preview: `@media print` rendering correct
6. No section hidden behind another (check last section in each column)
7. Text readable at arm's length on screen ≈ 1m on A0
