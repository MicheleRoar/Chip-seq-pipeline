# Chip-seq Pipeline

This repository contains a pipeline for the analysis of the Transcription Factor and Histone Mark ChIP-seq data.

## Motivation

The aim of this project is to create a standard pipeline that includes, metadata extraction, quality controls, data analysis and peak calling. 
This pipeline, receiving as input a list of GEO GSM ids and their corresponding factor (both Histone Marks and Transcription Factors), is able to automatically recognise the phred quality score, the sample's organism and discriminate single-end samples from paired end.

## Pipeline summary
1. Fastq file download ([parallel-fastq-dump](https://github.com/rvalieris/parallel-fastq-dump))
2. Metadata Extraction ([Entrez-Direct](https://www.ncbi.nlm.nih.gov/books/NBK179288/))
3. Raw read QC ([FastQC](https://github.com/s-andrews/FastQC))
4. Alignment ([bowtie2](https://github.com/BenLangmead/bowtie2))
5. Mark duplicates ([SAMtools](https://github.com/samtools/samtools))
6. Filtering to remove:
    - reads mapping to blacklisted regions ([SAMtools](https://github.com/samtools/samtools), [bedtools](https://github.com/arq5x/bedtools2))
    - reads that are marked as duplicates ([SAMtool](https://github.com/samtools/samtools))
    - reads that are unmapped ([SAMtool](https://github.com/samtools/samtools))
7. Evaluate sequencing alignment data ([qualimap](https://github.com/EagleGenomics-cookbooks/QualiMap))
8. Calculate PCR bottleneck coefficient (PBC) & Non-Redundant Fraction (NRF) ([pysam](https://github.com/pysam-developers/pysam))
9. Call broad/narrow peaks ([MACS2](https://github.com/macs3-project/MACS))
10. Present QC for raw read, alignment, peak-calling and differential binding results (MultiQC)
