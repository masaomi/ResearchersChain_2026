---
name: result_regeneration_checker
description: Verify that published results can be regenerated from raw data and code
tags: [reproducibility, P1, regeneration, verification]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Result Regeneration Checker

## Purpose
Verify that every figure, table, and number in a manuscript can be regenerated from the provided data and code.

## Checklist

### Data
- [ ] Raw data accessible (public repository or upon request)
- [ ] Processed data files match what the code expects
- [ ] Data checksums match documented values
- [ ] No manual steps between raw and processed data (or all documented)

### Code
- [ ] All scripts/notebooks available (GitHub + archived DOI)
- [ ] README with execution instructions
- [ ] Dependencies listed with exact versions
- [ ] Entry point clear (which script generates which figure/table)

### Regeneration Test
- [ ] Clone repo on a clean machine (or container)
- [ ] Install dependencies from lockfile
- [ ] Run code end-to-end without modification
- [ ] Compare outputs to published figures/tables
- [ ] Numerical results match within stated precision

## Mapping Table
| Manuscript Element | Script | Input Data | Expected Output |
|-------------------|--------|------------|-----------------|
| Figure 1 | `fig1_pca.R` | `counts_normalized.csv` | `figures/fig1.pdf` |
| Table 2 | `table2_de.R` | `counts_raw.csv` | `tables/table2.csv` |
| p-value in text (p.5 L.3) | `main_analysis.R:L45` | `counts_raw.csv` | 0.003 |

## Common Failures
- Hardcoded absolute file paths
- Missing intermediate files not in repository
- Unrecorded manual data cleaning steps
- Different package versions producing different results
