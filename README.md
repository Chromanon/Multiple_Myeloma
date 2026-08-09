🧬 ## Topological Data Analysis (TDA) Pipeline for Multiple Myeloma Phenotyping
# Project Overview
This repository contains a computational oncology pipeline that utilizes Topological Data Analysis (TDA) to identify and analyze distinct metabolic and oncogenic phenotypes within a Multiple Myeloma (MM) patient cohort.
By integrating genomic data (SNVs) and real-world clinical outcomes, this project aims to uncover novel disease subtypes that traditional linear models or strict clustering algorithms might miss. A specific focus of this pipeline is investigating the "Low Burden" or "Dark Matter" cohort—patients exhibiting clinical symptoms of Multiple Myeloma (CRAB criteria) but lacking canonical metabolic or cytogenetic drivers (e.g., TP53, KRAS, BRAF).
# Key Features
Automated Data Fetching: Dynamically downloads the Broad Institute Multiple Myeloma dataset (2014) from cBioPortal with MD5 checksum validation.
Biologically Informed Feature Engineering: Reduces genomic noise by restricting the feature space to 10 major oncogenic signaling pathways (based on Sanchez-Vega et al., 2018).
Continuous Shape Modeling (TDA): Applies the Mapper algorithm (TDAmapper) to create a continuous, overlapping network of patient phenotypes, avoiding the rigid boundaries of standard clustering.
Clinical Integration & Survival Analysis: Validates mathematical clusters against real-world clinical endpoints (Overall Survival) using Kaplan-Meier estimators.
Passenger Gene Filtering: Generates clean mutational landscapes (Oncoplots) by mathematically excluding giant structural passenger genes (e.g., TTN, MUC16) that commonly confuse machine learning models.
# Prerequisites & Installation
The pipeline is primarily built in R and optimized for execution in Google Colab to leverage cloud computing and persistent Google Drive storage.
Core R Dependencies:
tidyverse (Data manipulation and visualization)
maftools (Somatic variant analysis)
TDAmapper (Topological Data Analysis)
igraph (Network visualization)
survival & survminer (Clinical outcome analysis)
Note: The script automatically handles the installation of required system dependencies (like libmpfr-dev and libgmp3-dev for TDA) and Bioconductor packages when run in Colab.
# Pipeline Steps
Environment Setup: Mounts Google Drive and configures a persistent R library path.
Data Acquisition: Downloads and verifies the mm_broad clinical and mutational dataset.
Genomic Filtering: Converts the MAF (Mutation Annotation Format) into a binary patient-by-pathway matrix.
TDA & Clustering: Computes the Euclidean distance matrix and applies PCA-filtered TDA Mapper. Patients are clustered into communities (e.g., TP53, RTK-RAS, Epigenetics, and Low_Burden).
Survival Analysis: Merges derived subtypes with clinical survival data to visualize prognostic implications.
"Dark Matter" Investigation: Isolates the Low_Burden cohort, cross-references with FISH translocation and Hyperdiploidy status, and plots a curated Oncoplot revealing true underlying drivers.
# Outputs & Results
# Final Exported Dataset: TDA_Clusters.csv 
# Click here to view the final results dataset https://github.com/Chromanon/Multiple_Myeloma/blob/main/TDA_Clusters.csv
This file is the primary output of the pipeline, containing the final mathematical-to-clinical mapping for all analyzed patients. It bridges the gap between the unsupervised TDA algorithm and real-world clinical data.
Data Dictionary:
Patient_ID: Unique identifier for the Multiple Myeloma patient (matches standard TCGA/cBioPortal barcodes).
TDA_Cluster: The mathematically derived phenotype via TDA (e.g., Low_Burden, TP53, RTK-RAS).
FISH: Presence of specific FISH translocations (e.g., t(11;14)).
Hyperdiploid: Hyperdiploidy status (Yes/No).
Status: Clinical outcome (Alive / Dead) derived from PATIENT_DEATH_REASON.
# Visualizations Generated
Topological Networks: Interactive or static network graphs of patient clusters.
Kaplan-Meier Survival Curves: Demonstrating the clinical validity and prognostic value of the TDA-derived phenotypes.
Cleaned Oncoplots: Mutational landscapes for specific sub-cohorts (like the Low_Burden group), filtered for false positives and passenger genes.
# References & Acknowledgements
Genomic Dataset: Lohr, J. G., et al. (2014). Widespread genetic heterogeneity in multiple myeloma: implications for targeted therapy. Cancer Cell, 25(1), 91-101. doi:10.1016/j.ccr.2013.12.015
Oncogenic Pathways: Sanchez-Vega F, et al. (2018). Oncogenic Signaling Pathways in The Cancer Genome Atlas. Cell, 173(2):321-337.e10.
Bioinformatics Tools: Mayakonda A, et al. (2018). Maftools: efficient and comprehensive analysis of somatic variants in cancer. Genome Res, 28(11):1747-1756.
TDA Algorithm: Executed using the TDAmapper R package (Singh, Mémoli, and Carlsson, 2007).
Created as a proof-of-concept pipeline for computational oncology and precision medicine.
