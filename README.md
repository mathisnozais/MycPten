#MYC-deficiency impairs the development of effector/memory T lymphocytes<br/>
Authors :Mathis Nozais1*, Marie Loosveld1,2*, Saran Pankaew1, Clémence Grosjean1, Noémie Gentil1, Julie Quessada1, Cyrille Mionnet1, Delphine Potier1@ & Dominique Payet-Bornet1@

*These authors contributed equally: Mathis Nozais, Marie Loosveld; @ Corresponding authors: Dr Delphine Potier and Dr Dominique Payet-Bornet

Link to article : (TO come)

---

### Overview
This repository contains the instructions and material to reproduce the analysis reported in the article. Source code is available in the github repository. Required data and builded Docker/singularity images are available respectively in SRA/GEO and Zenodo. Intructions to reproduce the analysis are provided in the different subdirectories:

- Fastq preprocessing is discribed in the 01_FASTQ_Preprocessing folder
In order to re do Fastq preprocessing you can follow guidelines and script here : link to readm me 01_FASTQ_Preprocessing
- Seurat analysis is discribed in the 02_Seurat_analysis
In order to re do Seurat Analysis you can follow guidelines and script here : link to Readme 02_Seurat_analysis

---

### Data Availability
#### Fastq preprocessing
- 10 Fastq are availabe in SRA under the accession ID xxxxxxx
  - 4 Fastq files containing paired-end reads sequenced from the mRNA library of replicate 1 and 2
  - 4 Fastq files containing paired-end reads sequenced from the HTO library of replicate 1 and 2
  - 2 Fastq files containing paired-end reads sequenced from the ADT library of replicate 2
- Cellranger output and CITE-seq-count output that can be load in Seurat are available in GEO (xxxxxx)respectively under accession number xxxxxxxxx and xxxxxx :
  - link Cell ranger
  - link CITE seq count

#### Seurat analysis
- Seurat Html report containing figures generated in R from article can be downloaded here : link githtml report
- Seurat rmd script to reproduce the analysis can be found here : link to git script
Rmd script can be found here : link script


#### Docker and Singularity images
Singularity/Docker images and Robj are all availabe in Zenodo : link
