---
name: model_selection_advisor
description: Guide selection of appropriate ML models based on problem characteristics
tags: [machine_learning, P1, model-selection, decision]
domain: ml
source: {type: systematic, evidence_level: systematic}
---
# Model Selection Advisor

## Purpose
Choose the right ML model based on problem type, data characteristics, and requirements.

## Decision Matrix

| Problem | Data Size | Interpretability Need | Recommended Models |
|---------|-----------|----------------------|-------------------|
| Classification (tabular) | Small-Medium | High | Logistic regression, Decision tree |
| Classification (tabular) | Medium-Large | Medium | Random Forest, XGBoost |
| Classification (tabular) | Large | Low | Deep learning, ensemble |
| Regression (tabular) | Any | High | Linear regression, GAM |
| Regression (tabular) | Medium-Large | Medium | Random Forest, Gradient boosting |
| Classification (image) | Large | Low | CNN (ResNet, EfficientNet) |
| Sequence (text/DNA) | Large | Low | Transformer, RNN/LSTM |
| Clustering | Any | Medium | k-means, DBSCAN, hierarchical |
| Dimensionality reduction | Any | Medium | PCA, UMAP, t-SNE |

## Key Considerations
- **Start simple**: Always establish a baseline with a simple model first
- **Data size**: Deep learning needs large datasets; tree-based methods work well on smaller data
- **Feature types**: Mixed types favor tree-based; homogeneous numerical favor linear/neural
- **Inference vs prediction**: If understanding "why" matters, prefer interpretable models
- **Deployment constraints**: Model size, inference speed, hardware requirements

## Model Comparison Protocol
1. Define evaluation metric aligned with the problem
2. Use consistent cross-validation strategy
3. Compare models on held-out test set (never used during development)
4. Report confidence intervals for performance estimates
5. Consider practical significance, not just statistical
