---
name: figure_accessibility_checker
description: Check figures for accessibility including color vision deficiency support
tags: [visualization, P1, accessibility, colorblind, inclusive-design]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Figure Accessibility Checker

## Purpose
Ensure all figures are accessible to readers with diverse visual abilities.

## Color Vision Deficiency (CVD)

~8% of males and ~0.5% of females have some form of CVD. Figures must be readable by all.

### Safe Color Palettes
| Palette | Source | Use |
|---------|--------|-----|
| viridis | matplotlib/R | Sequential data (default recommendation) |
| cividis | matplotlib | Sequential, optimized for CVD |
| Okabe-Ito | Color Universal Design | Categorical (up to 8 colors) |
| ColorBrewer | colorbrewer2.org | Tested for various types of CVD |

### Unsafe Combinations (Avoid)
- Red vs Green (most common confusion)
- Blue vs Purple (tritanopia)
- Rainbow/jet colormap (not perceptually uniform + CVD-unfriendly)

## Beyond Color: Redundant Encoding
Always use at least two visual channels:
- Color + Shape (scatter plots)
- Color + Pattern/Texture (bar charts)
- Color + Labels (direct annotation)
- Color + Line style (solid, dashed, dotted)

## Accessibility Checklist
- [ ] Colorblind-safe palette used (test with CVD simulator)
- [ ] Information not conveyed by color alone (redundant encoding)
- [ ] Sufficient contrast between elements (WCAG AA: 4.5:1 ratio)
- [ ] Text readable at published size (>= 8pt)
- [ ] Alt text provided for digital figures
- [ ] Patterns or shapes distinguish groups in addition to color
- [ ] White/light backgrounds preferred over dark

## Testing Tools
- **Coblis** (coblis.com): CVD simulator for images
- **Viz Palette** (projects.susielu.com/viz-palette): Test palette accessibility
- **R**: `colorBlindness::cvdPlot()` on ggplot objects
- **Python**: `colorspacious` package for CVD simulation
