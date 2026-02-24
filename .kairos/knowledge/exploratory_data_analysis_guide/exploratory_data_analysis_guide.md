---
name: exploratory_data_analysis_guide
description: Systematic guide for exploratory data analysis (EDA)
tags: [data_engineering, P1, eda, exploration, visualization]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Exploratory Data Analysis Guide

## Purpose
Conduct systematic EDA to understand data before formal analysis.

## EDA Workflow

### 1. Data Overview
- Dimensions (rows, columns)
- Data types (numeric, categorical, temporal)
- Head/tail/sample inspection
- Memory usage

### 2. Univariate Analysis
| Data Type | Summaries | Visualizations |
|-----------|----------|----------------|
| Numeric | Mean, median, SD, min, max, quartiles | Histogram, box plot, density plot |
| Categorical | Frequency counts, mode, cardinality | Bar chart, pie chart (sparingly) |
| Temporal | Range, frequency, gaps | Time series plot |

### 3. Bivariate/Multivariate Analysis
| Combination | Methods |
|-------------|---------|
| Numeric vs Numeric | Scatter plot, correlation matrix, pair plot |
| Numeric vs Categorical | Box plot by group, violin plot |
| Categorical vs Categorical | Contingency table, mosaic plot |
| High-dimensional | PCA, t-SNE, UMAP, correlation heatmap |

### 4. Data Quality Assessment
- Missingness pattern (MCAR/MAR/MNAR?)
- Outlier identification
- Distribution shapes (normal? skewed? multimodal?)
- Class balance (for classification tasks)

### 5. Relationship Discovery
- Correlations (linear and non-linear)
- Grouping patterns (clusters?)
- Temporal trends or seasonality
- Potential confounders

## EDA Principles
- **Look at the data before modeling** — always
- **EDA is hypothesis-generating**, not hypothesis-testing
- **Document surprising findings** — they may be the most important
- **Resist premature conclusions** — explore, don't confirm
- **Visualize, don't just summarize** — Anscombe's quartet proves why
