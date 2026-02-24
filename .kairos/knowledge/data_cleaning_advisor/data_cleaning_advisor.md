---
name: data_cleaning_advisor
description: Guide systematic data cleaning strategies before analysis
tags: [data_engineering, P1, cleaning, preprocessing, quality]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Data Cleaning Advisor

## Purpose
Provide systematic strategies for cleaning data while preserving scientific integrity.

## Cleaning Workflow

1. **Profile**: Understand data structure, types, distributions, missingness
2. **Validate**: Check against expected ranges, types, and constraints
3. **Clean**: Apply documented, reproducible transformations
4. **Verify**: Confirm cleaning improved quality without introducing bias
5. **Document**: Record every decision and transformation

## Common Issues and Strategies

| Issue | Detection | Strategy |
|-------|----------|----------|
| Missing values | `df.isnull().sum()`, missingness pattern | See missing_data_strategy_advisor |
| Duplicates | Exact or fuzzy duplicate detection | Remove after verifying they are true duplicates |
| Outliers | IQR, z-score, domain-specific thresholds | Investigate cause before removing; document rationale |
| Inconsistent formats | Value counts, regex patterns | Standardize (dates, units, categories) |
| Data type errors | Type checking, failed conversions | Cast with error handling, investigate failures |
| Encoding issues | Non-ASCII characters, mojibake | Detect and fix encoding (UTF-8 standard) |
| Unit mismatches | Distribution anomalies, domain knowledge | Convert to consistent units, document |

## Critical Rules
- **Never modify raw data** — create a cleaned copy, keep originals
- **Script everything** — no manual Excel edits
- **Document all decisions** — why was this row removed? Why this threshold?
- **Assess impact** — compare results with and without cleaning decisions
- **Preserve provenance** — log transformations in the cleaning script

## Outlier Decision Framework
```
Is it a data entry error? → Fix or remove
Is it a measurement error? → Remove with documentation
Is it a genuine extreme value? → Keep; consider robust methods
Are you unsure? → Run analysis with and without; report both
```
