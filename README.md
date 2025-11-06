# CompuDataAnalysis

**CompuDataAnalysis** is an R package for high-throughput data manipulation, aggregation, 
and performance benchmarking across diverse datasets in bioinformatics and clinical research.

Built around the efficient `data.table` framework, it offers a unified set of tools 
for transforming, joining, and analyzing large-scale tabular data efficiently.

---

## Installation

To install the package directly from GitHub:

```r
RUN R -e "install.packages('https://github.com/miacarboni-creator/CompuDataAnalysis/raw/main/CompuDataAnalysis_0.0.0.9000_.tar', repos = NULL, type = 'source')"

# Package Functions

This package provides utilities for RNA-seq data analysis, laboratory results processing, genomic peak/SNP analysis, and cell type integration. Functions are grouped by their main purpose for clarity.

---

## 1. CSV / Data Loading

| Function | Description |
|----------|-------------|
| `load_csv(file_name_pattern)` | Searches for and loads the first CSV file whose name matches a specified pattern. Supports recursive searches in subdirectories. |

---

## 2. Bulk RNA-seq Analysis

| Function | Description |
|----------|-------------|
| `summarize_bulk_counts(bc, meta, condition_filter, gene_pattern)` | Summarizes bulk RNA-seq gene expression data by experimental condition and gene pattern, calculating mean counts per gene. |
| `add_log_and_high_flag(bc_dt)` | Adds log2-transformed counts and a flag indicating if a gene's count is above the median. |
| `analyze_join_index(bc, meta)` | Performs a join between data and metadata using **data.table**, benchmarking the effect of indexing on performance. |
| `analyze_bulk_counts_df(bc_df, meta_df)` | Analyzes bulk RNA count data in **data.frame/tibble**, totals counts per patient, and identifies top 10 genes per condition. |
| `get_upregulated_genes(cnt_dt, meta_dt)` | Selects genes upregulated in the treated group compared to control (≥2× mean). |

---

## 3. Laboratory Data Analysis

| Function | Description |
|----------|-------------|
| `classify_abnormal_labs(labs_dt, refs_dt, meta_dt = NULL)` | Classifies lab results as normal or out-of-range using reference intervals, providing per-patient and per-test statistics. |
| `match_labs_vitals(labs_dt, vitals_dt)` | Matches CRP measurements with nearest-in-time vital signs and computes correlations per patient. |

---

## 4. Genomic Peaks & SNP Analysis

| Function | Description |
|----------|-------------|
| `get_top_peaks(dt, chromosome, start_min, start_max, top_n = 50)` | Extracts the most significant genomic peaks in a specified interval, sorted by score. |
| `process_peaks(peaks_wide, meta_dt)` | Converts peak or count data from wide to long format and computes gene × condition statistics (mean, median, quartiles). |
| `compute_peak_gene_overlap(peaks_dt, genes_dt, top_n = 20)` | Calculates base-pair overlaps between peaks and genes, summarizes per gene, returns top N. |
| `map_snps_to_genes(variants_dt, genes_dt)` | Maps SNPs to genes, filters for HIGH-impact variants, and counts them per gene/sample. |
| `compute_top_genes_dt(cohortA_dt, cohortB_dt, counts_dt, top_n = 100, preview_n = 10)` | Identifies the most variable genes between two cohorts, previews results, and calculates mean counts per condition/cohort. |

---

## 5. Cell Type Integration

| Function | Description |
|----------|-------------|
| `process_celltype_integration_dt(annot_dt, ct_dt)` | Integrates cell annotations with clustering results using **data.table**, computes counts/percentages per cluster, generates plots. |
| `process_celltype_integration_df(annot_df, ct_df)` | Equivalent **data.frame/dplyr** version of cell type integration and cluster summary. |
| `compare_performance_integration(annot_dt, ct_dt)` | Compares execution times between **data.table** and **data.frame/dplyr** versions of the integration workflow. |

---
