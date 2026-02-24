---
name: consent_scope_checker
description: Verify that informed consent covers the intended analysis scope
tags: [ethics, P0, consent, compliance]
promoted_from: L2/afd_foundation_001/draft_consent_scope_checker
evolution_criterion: Upholds research ethics — ensures analyses stay within consented boundaries
---
# Consent Scope Checker

## Purpose
Ensure all planned analyses fall within the boundaries of informed consent.

## Workflow
1. Identify consented purpose (primary research question)
2. List all planned analyses (primary + secondary + exploratory)
3. Check each analysis against consent scope
4. Flag analyses that may exceed consent boundaries
5. Recommend action per finding
6. Output: consent coverage matrix with recommendations

## Coverage Matrix Template
| Analysis | Consented? | Action Needed |
|----------|-----------|---------------|
| Primary DE analysis | Yes | Proceed |
| Secondary pathway analysis | Yes | Proceed |
| Exploratory pharmacogenomics | Unclear | Consult ethics board |
| Data sharing to public repo | No | Seek additional consent |

## Actions
- **Proceed**: Analysis within consent scope
- **Consult**: Seek ethics board clarification
- **Expand**: Obtain additional consent from participants
- **Exclude**: Remove analysis from scope
