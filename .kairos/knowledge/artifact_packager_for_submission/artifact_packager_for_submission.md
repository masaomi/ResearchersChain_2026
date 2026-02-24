---
name: artifact_packager_for_submission
description: Package all research artifacts for journal submission and archival
tags: [reproducibility, P1, packaging, submission, archival]
domain: general
source: {type: systematic, evidence_level: systematic}
---
# Artifact Packager for Submission

## Purpose
Create a complete, self-contained research package for submission and long-term archival.

## Package Contents

### Required
| Item | Format | Destination |
|------|--------|-------------|
| Manuscript | PDF/DOCX | Journal submission system |
| Figures (high-res) | TIFF/PDF/EPS (300+ dpi) | Journal submission system |
| Supplementary materials | PDF | Journal submission system |
| Raw data | FASTQ/CSV/etc. | Public repository (GEO, SRA, Zenodo, Dryad) |
| Analysis code | Scripts/notebooks | GitHub + Zenodo (DOI) |
| Environment specification | Dockerfile / renv.lock / environment.yml | With code |

### Recommended
| Item | Format | Destination |
|------|--------|-------------|
| Processed data | CSV/RDS/H5AD | Public repository |
| Pipeline configuration | Nextflow/Snakemake config | With code |
| Pre-registration | PDF/URL | OSF or journal |
| Reviewer response template | DOCX | Prepared in advance |

## Archival Checklist
- [ ] Data deposited with accession number
- [ ] Code archived with DOI (Zenodo release from GitHub)
- [ ] All accession numbers / DOIs referenced in manuscript
- [ ] License specified (code: MIT/Apache; data: CC-BY)
- [ ] ORCID linked for all authors
- [ ] Embargo period set if needed (pre-publication)

## Data Availability Statement Template
"Raw sequencing data have been deposited in [repository] under accession [ID]. Analysis code is available at [GitHub URL] and archived at [Zenodo DOI]."
