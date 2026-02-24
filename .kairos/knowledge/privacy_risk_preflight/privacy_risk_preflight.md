---
name: privacy_risk_preflight
description: Pre-flight check for genomic data privacy risks before analysis
tags: [ethics, P0, privacy, GDPR, HIPAA]
promoted_from: L2/afd_foundation_001/draft_privacy_risk_preflight
evolution_criterion: Upholds research ethics — prevents accidental privacy violations
---
# Privacy Risk Preflight

## Purpose
Systematic privacy risk assessment before any genomic data analysis begins.

## Checklist
1. **Consent scope**: Is informed consent sufficient for this analysis?
2. **De-identification**: Is data de-identified or anonymized?
3. **Re-identification risk**: Rare variants, small populations, family data?
4. **Regulatory compliance**: GDPR (EU), HIPAA (US), institutional policy?
5. **Data transfer**: Cross-institutional data transfer agreements in place?
6. **Storage security**: Encrypted at rest, access-controlled?
7. **Output risk**: Could results reveal individual identity?

## Risk Levels
| Level | Action |
|-------|--------|
| Low | Proceed with standard precautions |
| Medium | Add safeguards, document mitigations |
| High | Consult ethics board before proceeding |
| Critical | STOP — do not proceed without explicit approval |

## Genomics-Specific Risks
- Whole genome data is inherently identifiable
- Rare variant carriers in small cohorts
- Family studies can reveal non-consented relatives
- Population-specific variants in underrepresented groups
