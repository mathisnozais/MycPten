# Images
## Overview
This directory contain downloading link for docker and singularity images you will need to use to perform the different analysis once you cloned this repository.
All docker and singularity images are available on [Zenodo](https://doi.org/10.5281/zenodo.4636520).
Docker must be installed on your system. See https://docs.docker.com/install/ for details on Docker installation.

#### What do you need to download ?
- 01_FASTQ_Preprocessing
  - CellRanger (singularity)
  ```bash
  # To download CellRanger
  wget -P $WORKING_DIR/Images/Singularity/MycPten_Cellranger https://zenodo.org/record/4636520/files/cellranger2.1.0.img
  ```
  - Cite-seq-count (singularity)
  ```bash
  # To download CiteSeqCount
  wget -P $WORKING_DIR/Images/Singularity/MycPten_CITE https://zenodo.org/record/4636520/files/citeseqcount141_image.tar
  ```
- 02_Seurat_analysis
  - Seurat301v2 (Docker)
  ```bash
  # To download Seurat301v2
  wget -P $WORKING_DIR/Images/Docker https://zenodo.org/record/4636520/files/Seurat301v2.tar
  ```
