# CompuDataAnalysis

[![R version](https://img.shields.io/badge/R-%3E=4.0-blue.svg)](https://www.r-project.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/miacarboni-creator/CompuDataAnalysis)](https://github.com/miacarboni-creator/CompuDataAnalysis/releases)

**CompuDataAnalysis** is an R package for high-throughput data manipulation, aggregation, 
and performance benchmarking across bioinformatics and clinical datasets.

It leverages the efficient **`data.table`** framework to provide a unified workflow for transforming, joining, 
and analyzing large-scale tabular data efficiently.

---

## Functions Overview

The package includes utilities for:

- **CSV / Data Loading**  
- **Bulk RNA-seq Analysis**  
- **Laboratory Data Analysis**  
- **Genomic Peaks & SNP Analysis**  
- **Cell Type Integration**  

> Functions are grouped by their main purpose for clarity. For advanced users, see function documentation in R.

---

### 1️ CSV / Data Loading

| Function | Description |
|----------|-------------|
| `load_csv(file_name_pattern)` | Searches for and loads the first CSV file matching a pattern. Supports recursive searches. |

---

### 2️ Bulk RNA-seq Analysis

| Function | Description |
|----------|-------------|
| `summarize_bulk_counts(bc, meta, condition_filter, gene_pattern)` | Summarizes bulk RNA-seq counts by condition and gene pattern; calculates mean counts per gene. |
| `add_log_and_high_flag(bc_dt)` | Adds log2-transformed counts and a flag if a gene's count exceeds the median. |
| `analyze_join_index(bc, meta)` | Joins data and metadata using **data.table**; benchmarks indexing performance. |
| `analyze_bulk_counts_df(bc_df, meta_df)` | Analyzes bulk RNA counts in **data.frame/tibble**; totals per patient and identifies top 10 genes per condition. |
| `get_upregulated_genes(cnt_dt, meta_dt)` | Selects genes upregulated ≥2× in treated vs. control groups. |

---

### 3️ Laboratory Data Analysis

| Function | Description |
|----------|-------------|
| `classify_abnormal_labs(labs_dt, refs_dt, meta_dt = NULL)` | Classifies lab results as normal or out-of-range; provides per-patient and per-test statistics. |
| `match_labs_vitals(labs_dt, vitals_dt)` | Matches CRP measurements with nearest-in-time vital signs; computes per-patient correlations. |

---

### 4️ Genomic Peaks & SNP Analysis

| Function | Description |
|----------|-------------|
| `get_top_peaks(dt, chromosome, start_min, start_max, top_n = 50)` | Extracts top genomic peaks in a specified interval, sorted by score. |
| `process_peaks(peaks_wide, meta_dt)` | Converts wide-format peak/count data to long format; computes gene × condition statistics (mean, median, quartiles). |
| `compute_peak_gene_overlap(peaks_dt, genes_dt, top_n = 20)` | Computes base-pair overlaps between peaks and genes; summarizes per gene and returns top N. |
| `map_snps_to_genes(variants_dt, genes_dt)` | Maps SNPs to genes; filters HIGH-impact variants; counts variants per gene/sample. |
| `compute_top_genes_dt(cohortA_dt, cohortB_dt, counts_dt, top_n = 100, preview_n = 10)` | Identifies most variable genes between cohorts; previews results; calculates mean counts per condition/cohort. |

---

### 5️ Cell Type Integration

| Function | Description |
|----------|-------------|
| `process_celltype_integration_dt(annot_dt, ct_dt)` | Integrates cell annotations with clustering results using **data.table**; computes counts/percentages per cluster; generates plots. |
| `process_celltype_integration_df(annot_df, ct_df)` | **data.frame/dplyr** equivalent for cell type integration and cluster summary. |
| `compare_performance_integration(annot_dt, ct_dt)` | Benchmarks execution times between **data.table** and **data.frame/dplyr** workflows. |


## Installation

Install directly from GitHub:

```r
install.packages(
  "https://github.com/miacarboni-creator/CompuDataAnalysis/raw/main/CompuDataAnalysis_0.0.0.9000_.tar",
  repos = NULL,
  type = "source"
)

