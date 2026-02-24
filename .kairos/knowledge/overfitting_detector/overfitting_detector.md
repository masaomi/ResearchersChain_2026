---
name: overfitting_detector
description: Detect and mitigate overfitting in ML models
tags: [machine_learning, P1, overfitting, regularization, generalization]
domain: ml
source: {type: systematic, evidence_level: systematic}
---
# Overfitting Detector

## Purpose
Identify when models are fitting noise rather than signal, and apply appropriate remedies.

## Detection Signals

| Signal | Indicator | Severity |
|--------|----------|----------|
| Train >> Test performance | Large gap between train and test metrics | High |
| Perfect training accuracy | 100% on train, much lower on test | High |
| Performance drops on new data | Model degrades in production/validation | High |
| Complex model barely beats simple | Marginal gain for much more complexity | Medium |
| Unstable predictions | Small data changes cause large output changes | Medium |

## Learning Curve Diagnosis
```
Performance
  │  ╭──── Training (should decrease slightly)
  │ ╱
  │╱   ╭── Validation (should increase and converge)
  │   ╱
  └──────── Data size
     
  Gap = Overfitting    Converged low = Underfitting
```

## Remedies

| Remedy | When to Use |
|--------|------------|
| More training data | Always the best option if available |
| Regularization (L1/L2) | Linear models, neural networks |
| Dropout | Neural networks |
| Early stopping | Iterative models (boosting, neural nets) |
| Reduce model complexity | Fewer features, shallower trees, smaller network |
| Cross-validation | Better evaluation, not a fix per se |
| Feature selection | Remove noisy/irrelevant features |
| Ensemble methods | Bagging reduces variance |
| Data augmentation | When more real data unavailable |

## Key Principle
A model that memorizes the training data is useless. The goal is generalization, not memorization. Always evaluate on data the model has never seen.
