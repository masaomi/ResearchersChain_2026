---
name: visualization_best_practices
description: Principles for effective and honest data visualization
tags: [visualization, P1, figures, communication, best-practices]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Visualization Best Practices

## Purpose
Create figures that are informative, honest, and publication-ready.

## Core Principles
1. **Show the data** — individual data points over bar charts when feasible
2. **Facilitate comparison** — align scales, use consistent colors
3. **Minimize chartjunk** — remove unnecessary gridlines, 3D effects, decoration
4. **Tell the truth** — axis starts at zero for bar charts; don't truncate misleadingly
5. **Accessibility** — colorblind-safe palettes, sufficient contrast, readable text

## Chart Selection Guide

| Data Relationship | Recommended | Avoid |
|------------------|-------------|-------|
| Distribution | Histogram, density, violin, box plot | Pie chart for continuous data |
| Comparison | Grouped bar, dot plot, forest plot | Stacked bar (hard to compare) |
| Relationship | Scatter plot, hexbin (large n) | 3D scatter (hard to read) |
| Composition | Stacked area, treemap | Pie chart (>5 categories) |
| Trend | Line chart, smoothed line | Bar chart for time series |
| Genomics | Volcano plot, MA plot, heatmap, genome browser | — |

## Publication Checklist
- [ ] Resolution >= 300 DPI for print
- [ ] Font size readable at published size (>= 8pt)
- [ ] Axis labels with units
- [ ] Legend clear and complete
- [ ] Color palette colorblind-safe (viridis, cividis, or tested with simulator)
- [ ] Figure panels labeled (A, B, C)
- [ ] Scale bars where appropriate
- [ ] Statistical annotations (p-values, significance brackets) if needed
- [ ] Vector format preferred (PDF, SVG) over raster (PNG)

## Avoid
- Dual y-axes (misleading correlations)
- Rainbow color scales (not perceptually uniform)
- 3D charts (distort perception)
- Dynamite plots (bar + error bar) — use box/violin + points instead
