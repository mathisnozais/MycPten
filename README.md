#Myc Pten Analysis
## MYC-deficiency impairs the development of effector/memory T lymphocytes<br/>
Authors :Mathis Nozais1*, Marie Loosveld1,2*, Saran Pankaew1, Clémence Grosjean1, Noémie Gentil1, Julie Quessada1, Cyrille Mionnet1, Delphine Potier1@ & Dominique Payet-Bornet1@

*These authors contributed equally: Mathis Nozais, Marie Loosveld; @ Corresponding authors: Dr Delphine Potier and Dr Dominique Payet-Bornet

Link to article : (TO come)
### Overview
This repository contains the instructions and material to reproduce the analysis reported in the article. Source code is available in the github repository. Required data and builded Docker/singularity images are available respectively in SRA/GEO and Zenodo. Intructions to reproduce the analysis are provided in the different subdirectories:

- Fastq preprocessing is discribed in the 01_FASTQ_Preprocessing folder
- Seurat analysis is discribed in the 02_Seurat_analysis

### Data Availability
#### Fastq preprocessing
- 10 Fastq are availabe in SRA under the accession ID xxxxxxx
  - 4 Fastq files containing paired-end reads sequenced from the mRNA library of replicate 1 and 2
  - 4 Fastq files containing paired-end reads sequenced from the HTO library of replicate 1 and 2
  - 2 Fastq files containing paired-end reads sequenced from the ADT library of replicate 2

Explanation to reproduce are located in : link
#### Seurat analysis
Rmd script can be found here : link


#### Docker and Singularity images
Singularity/Docker images are all availabe in Zenodo : link
