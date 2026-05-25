# RNA-Seq Analysis Pipeline Using Galaxy

![Platform](https://img.shields.io/badge/Platform-Galaxy-blue) ![Organism](https://img.shields.io/badge/Organism-Drosophila%20melanogaster-brightgreen) ![Status](https://img.shields.io/badge/Status-Complete-success) ![License](https://img.shields.io/badge/License-MIT-lightgrey)

A complete, reproducible RNA-seq analysis pipeline implemented on the Galaxy platform, covering the full workflow from raw read acquisition through differential expression analysis. This project follows best practices in sequencing data analysis, emphasizing data quality, accurate read mapping, and structured reproducible processing.

> Developed under the supervision of **Prof. Rehab Abdallah**, Faculty of Biotechnology, Misr University for Science and Technology (MUST), Egypt.

---

## Table of Contents

- [Overview](#overview)
- [Input Data](#input-data)
- [Workflow Steps](#workflow-steps)
- [Workflow File](#workflow-file)
- [Results](#results)
- [Tools Used](#tools-used)
- [Author](#author)

---

## Overview

This pipeline processes raw RNA sequencing data from *Drosophila melanogaster* — a widely used model organism in genomics research — through a structured multi-step workflow. The goal is to produce reliable gene-level count matrices and differential expression results, while maintaining full quality control and reproducibility throughout.

The entire workflow is implemented in Galaxy and can be reproduced by any user by importing the provided `.ga` workflow file.

---

## Input Data

| Input | Description |
|---|---|
| Raw sequencing reads | Retrieved from NCBI SRA (paired-end FASTQ format) |
| Reference genome | *D. melanogaster* genome — UCSC (FASTA) |
| Gene annotation (GTF) | `genomic.gtf` and `dm6.ncbiRefSeq.gtf` |
| Gene annotation (GFF) | `genomic.gff` and `genomic_fixed.gtf` |
| Experimental design | `factors_clean.tsv` — sample grouping for DE analysis |

---

## Workflow Steps

### 1. Data Acquisition
- Reads downloaded from NCBI SRA using **Fasterq-dump v3.1.1**
- Output: paired-end FASTQ files

### 2. Quality Control
- Initial quality assessment using **FastQC**
- Aggregated multi-sample reports generated using **MultiQC v1.33**
- Sequencing quality, adapter content, and read length distribution evaluated across all samples

### 3. Alignment
- Reads aligned to the *D. melanogaster* reference genome using **HISAT2**
- HISAT2 selected for its splice-aware alignment, essential for accurate RNA-seq mapping
- Output: BAM alignment files

### 4. Post-alignment Processing
- Alignment statistics computed using **Samtools**
- BAM files filtered to retain only high-quality mapped reads
- PCR duplicates identified and removed using **Picard MarkDuplicates**
- Per-chromosome alignment summaries generated using **Samtools idxstats**

### 5. Annotation Processing
- Gene annotation files converted to BED and BED12 formats
- Prepared for compatibility with downstream QC and visualization tools

### 6. RNA-seq Quality Assessment
- Read distribution across genomic features (exons, introns, intergenic regions) analyzed using **RSeQC**
- Gene body coverage assessed for 5′→3′ uniformity using **RSeQC**
- Library strandedness inferred using **RSeQC Infer Experiment**
- All three RSeQC outputs aggregated separately into **MultiQC v1.33** reports

### 7. Gene Quantification
- Gene-level read counts generated using **featureCounts**
- Count matrices from multiple samples merged using **Collection Column Join v0.0.3**
- Output: unified count matrix used for differential expression analysis

### 8. Differential Expression Analysis
- Differential expression analysis performed using **limma-voom v3.58.1**
- Contrast tested: `control vs. histidine`
- Normalization method: TMM
- p-value threshold: 0.05 | Log fold-change threshold: 0
- p-value adjustment: Benjamini-Hochberg (BH)
- Output: DE result tables and diagnostic plots (MD plot, heatmap)

### 9. Visualization
- Alignment tracks visualized using **JBrowse**
- Multi-sample read coverage and SNPs/Coverage tracks inspected across genomic regions

### 10. Reporting
- **MultiQC v1.33** used to aggregate QC and alignment metrics across all pipeline steps
- Comprehensive HTML reports generated for easy interpretation

---

## Workflow File

The complete Galaxy workflow is available at:

```
workflow/Galaxy-Workflow-rna_seq_pipeline.ga
```

To reproduce this analysis:
1. Open your Galaxy instance
2. Go to **Workflow → Import**
3. Upload `Galaxy-Workflow-rna_seq_pipeline.ga`
4. Connect your input datasets and run

---

## Results

The pipeline produces the following outputs:

| Output | Tool | Description |
|---|---|---|
| QC reports | MultiQC v1.33 | Aggregated quality metrics across all samples |
| Alignment files | HISAT2 + Samtools | Filtered, sorted BAM files |
| Duplicate metrics | Picard | PCR duplicate removal statistics |
| RSeQC reports | MultiQC v1.33 | Read distribution, gene body coverage, strandedness |
| Gene count matrix | featureCounts + Column Join | Merged read counts per gene per sample |
| DE results | limma-voom v3.58.1 | Differentially expressed genes with statistics |
| Coverage tracks | JBrowse | Visual inspection of read alignment and SNPs |

### Example Outputs

**JBrowse — Multi-sample Alignment & SNPs/Coverage Tracks**
![JBrowse Coverage](results/jbrowse.png)

---

## Tools Used

| Tool | Version | Purpose |
|---|---|---|
| Fasterq-dump | 3.1.1 | SRA data download |
| FastQC | — | Per-sample quality control |
| MultiQC | 1.33 | Aggregated QC reporting |
| HISAT2 | — | Splice-aware read alignment |
| Samtools | — | BAM processing and statistics |
| Picard MarkDuplicates | — | PCR duplicate removal |
| RSeQC | — | RNA-seq specific QC metrics |
| featureCounts | — | Gene-level quantification |
| Collection Column Join | 0.0.3 | Merging per-sample count matrices |
| limma-voom | 3.58.1 | Differential expression analysis |
| JBrowse | — | Alignment visualization |

---

## Author

**Anan Mohamed Elrayes**
3rd Year Biotechnology Student — MUST, Egypt
📧 ananelrayes2110@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/anan-elrayes) | [GitHub](https://github.com/ananelrayes2110-glitch)

---

*This pipeline demonstrates a reproducible, production-style RNA-seq workflow following best practices in sequencing data analysis, from raw reads through differential expression.*
