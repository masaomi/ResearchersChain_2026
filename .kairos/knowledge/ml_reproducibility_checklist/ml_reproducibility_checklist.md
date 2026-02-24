---
name: ml_reproducibility_checklist
description: Comprehensive checklist for reproducible ML experiments
tags: [machine_learning, P1, reproducibility, checklist]
domain: ml
source: {type: systematic, evidence_level: systematic}
---
# ML Reproducibility Checklist

## Purpose
Ensure ML experiments are fully reproducible by another researcher.

## Checklist

### Data
- [ ] Dataset source documented (URL, version, download date)
- [ ] Train/validation/test split documented (method, seed, proportions)
- [ ] Preprocessing steps documented and scripted (no manual steps)
- [ ] Data leakage verified absent (no test information in training)
- [ ] Class distribution reported for all splits

### Model
- [ ] Model architecture fully specified
- [ ] All hyperparameters documented (including defaults)
- [ ] Hyperparameter search method and range documented
- [ ] Random seeds set for all stochastic components
- [ ] Number of training epochs/iterations documented
- [ ] Early stopping criteria documented (if used)

### Evaluation
- [ ] Evaluation metrics justified and defined
- [ ] Cross-validation strategy documented
- [ ] Confidence intervals or standard deviations reported
- [ ] Comparison with meaningful baselines (not just random)
- [ ] Statistical significance of improvements tested
- [ ] Results reported on held-out test set (used only once)

### Environment
- [ ] Hardware documented (GPU type, RAM, CPU)
- [ ] Software versions pinned (framework, libraries)
- [ ] Docker/conda environment file provided
- [ ] Training time reported
- [ ] Code available with README and entry point

### Reporting (ML-specific)
- [ ] Training curves provided (loss, metric vs epoch)
- [ ] Confusion matrix or per-class metrics for classification
- [ ] Feature importance analysis included
- [ ] Failure cases analyzed and discussed
- [ ] Model limitations explicitly stated

## Reference Standards
- NeurIPS Reproducibility Checklist
- ML Reproducibility Challenge guidelines
- FAIR principles for ML (data + model + code)
