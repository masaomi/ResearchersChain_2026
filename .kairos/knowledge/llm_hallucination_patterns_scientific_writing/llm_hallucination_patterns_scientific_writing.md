---
title: "LLM Hallucination Patterns in Scientific Writing"
description: "Taxonomy of common LLM hallucination types in scientific documents, with detection heuristics and prevention strategies"
tags:
  - quality-assurance
  - scientific-writing
  - hallucination-detection
  - review
version: "1.0"
created: "2026-02-25"
evidence_source: "Observed during 3-agent parallel review of preprint/poster/presentation (2026-02-24)"
---

# LLM Hallucination Patterns in Scientific Writing

LLM-generated or LLM-assisted scientific documents are susceptible to specific categories of hallucination. This knowledge provides a taxonomy for systematic detection.

## Category 1: Biological/Domain Entity Fabrication

**Pattern**: Species names, gene names, cell types, or other domain-specific entities are substituted with plausible but incorrect alternatives.

**Examples**:
- Correct species replaced by a related but wrong organism
- Tissue types or sampling conditions invented
- Gene/protein names that sound plausible but don't exist in the organism

**Detection heuristic**:
- Cross-reference every species/organism name against the primary data source
- Verify tissue, sampling, and experimental condition descriptions against the cited paper's abstract
- Check taxonomic consistency (genus + species + common name)

## Category 2: Quantitative Value Fabrication

**Pattern**: Numerical results (metrics, p-values, correlation coefficients, effect sizes) are generated without grounding in actual computed data.

**Examples**:
- Performance metrics (accuracy, AUC, F1, RMSE) that don't match any CSV/output file
- Correlation values stated without corresponding computation
- Comparative improvements ("5-10% better") without supporting evidence
- Confidence intervals or p-values invented to support a narrative

**Detection heuristic**:
- Every numerical claim in text must trace to a specific output file (CSV, log, figure)
- Search for round numbers or suspiciously clean ranges (e.g., "0.72-0.82") — real data is rarely this neat
- Verify that comparative claims (e.g., "method A outperforms B by X%") are computed from actual paired results

## Category 3: Citation Fabrication and Misattribution

**Pattern**: Bibliographic details (journal name, volume, pages, year) are altered, or citations are attributed to wrong authors or journals.

**Examples**:
- Correct author + wrong journal (e.g., *Nature Plants* → *Plant Cell*)
- Correct paper + wrong volume/page numbers
- Citing a paper that exists but for a claim it does not support
- Citing non-existent papers with plausible-sounding titles

**Detection heuristic**:
- Verify every citation's journal, volume, pages, and year against the `.bib` file or DOI
- For key claims, confirm the cited paper actually supports that specific claim
- Be especially suspicious of citations not present in the `.bib` file

## Category 4: Methodology-Data Mismatch

**Pattern**: Methods described in text do not match the actual implemented code, or scenarios/configurations described differ from what was programmed.

**Examples**:
- Describing simulation scenarios that don't exist in the code (e.g., "Lorenz-coupled" when code has "threshold_coupled")
- Claiming a model hierarchy that differs from the actual decomposition
- Describing hyperparameters or architectures that don't match `config.py`
- Using labels/terminology inconsistent with the codebase

**Detection heuristic**:
- Diff every methodological claim against the corresponding source code
- Verify scenario names, model names, and parameter values against config files
- Check that variable naming conventions (e.g., NI_L1 vs NI_quad) are consistent between code and text

## Category 5: Narrative Overclaiming

**Pattern**: Results are described with stronger conclusions than the data supports, or caveats present in the data are omitted.

**Examples**:
- Presenting a simple benchmark result as if it generalizes to complex scenarios
- Omitting failure cases or negative results
- Claiming "robust" or "significant" without statistical tests
- Describing a proof-of-concept as a competitive method

**Detection heuristic**:
- For every superlative or strong claim, ask: "What is the weakest interpretation of this result?"
- Check if limitations sections adequately cover known failure modes
- Verify that "significant" is backed by a statistical test with reported p-value

## Prevention Workflow

When generating or reviewing LLM-assisted scientific documents:

1. **Entity audit**: List all species, genes, tissues, conditions mentioned → verify each against primary sources
2. **Numerical audit**: List all quantitative claims → trace each to a specific output file
3. **Citation audit**: Verify journal, year, volume, pages for every reference
4. **Code-text consistency check**: Diff methodology descriptions against source code
5. **Claim strength audit**: Flag all superlatives and comparative claims → verify with data

## Priority Order for Review

Highest risk of undetected hallucination:
1. **Poster/Presentation** (compressed format, less scrutiny, higher hallucination rate)
2. **Results section** (quantitative claims most vulnerable)
3. **Methods section** (terminology and parameter mismatches)
4. **Introduction** (citation misattribution)
5. **Discussion** (overclaiming)
