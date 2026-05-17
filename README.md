# RNA-Seq-Analysis-Pipeline-Using-Galaxy
This project presents a complete RNA-seq analysis pipeline implemented using the Galaxy platform. The workflow includes raw data acquisition, quality control, alignment, post-alignment processing, and gene quantification.  The pipeline is designed to ensure data quality, accurate read mapping, and reliable downstream analysis.

---

# RNA-Seq Analysis Pipeline Using Galaxy

## Overview

This project presents a comprehensive RNA-seq analysis pipeline implemented using the Galaxy platform. The workflow covers the full analysis process, including data acquisition, quality control, alignment, post-alignment processing, and gene quantification.

The pipeline is designed to ensure high data quality, accurate read mapping, and reliable downstream analysis.

---

## Input Data

* Raw sequencing reads retrieved from SRA (FASTQ format)
* Reference genome (Drosophila melanogaster)
* Gene annotation files (GTF/GFF)
* Experimental design file (factors table)

---

## Workflow Steps

### 1. Data Acquisition

* Reads were downloaded from SRA using **Fasterq-dump**
* Output: paired-end FASTQ files

### 2. Quality Control

* Quality assessment performed using **MultiQC**
* Aggregated reports used to evaluate sequencing quality across samples

### 3. Alignment

* Reads aligned to the reference genome using **HISAT2**
* Output: BAM alignment files

### 4. Post-alignment Processing

* Alignment statistics generated using **Samtools**
* BAM files filtered to retain high-quality reads
* PCR duplicates removed using **Picard MarkDuplicates**
* Alignment summaries generated using **Samtools idxstats**

### 5. Annotation Processing

* Gene annotation files converted to **BED** and **BED12** formats
* Prepared for downstream analysis and visualization

### 6. RNA-seq Quality Assessment

* Read distribution across genomic regions analyzed
* Gene body coverage assessed for uniformity
* Library strandedness inferred using **Infer Experiment**

### 7. Gene Quantification

* Gene-level read counts generated using **featureCounts**
* Output used for downstream expression analysis

### 8. Visualization

* Alignment data visualized using **JBrowse**
* Enabled inspection of read coverage across genomic regions

### 9. Reporting

* **MultiQC** used to aggregate results from multiple steps
* Generated comprehensive reports for quality and alignment metrics

---

## Workflow File

The complete Galaxy workflow is available in:

`workflow/rna_seq_pipeline.ga`

This file can be imported directly into Galaxy to reproduce the analysis.

---

## Results

The pipeline generates:

* Quality control reports (MultiQC)
* Alignment statistics
* Gene count matrix (featureCounts)
* Visualization outputs (JBrowse)

Example outputs are provided in the `results/` directory.

---

## Notes

This project was developed as part of bioinformatics training and demonstrates practical implementation of RNA-seq analysis using Galaxy. The workflow emphasizes reproducibility and structured data processing.

---

---

