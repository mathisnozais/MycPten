# FASTQ Preprocessing
## Overview
This repository contains the instructions and material to reproduce fastq pre-processing reported in the article. Required data and Singularity images are respectively available in SRA and Zenodo. Intructions to reproduce the analysis are provided below.
To reproduce the analysis, you have to first, prepare the environments (see "Prerequisites" section below), then execute the analysis described in the "Run the analysis" section below.

If you don't want to redo data pre-processing directly go to (link to 02_Seuratanalysis)
---

## Setup the experiment
### Prerequisites
Singularity container images are available in zenodo :
- CellRanger : link
- CITE-seq-Count : link

Transcriptome is available at 10xGenomics website (http://cf.10xgenomics.com/supp/cell-exp/refdata-cellranger-mm10-3.0.0.tar.gz) and in Zenodo (link)
J'explique eYFP ou donne directement Zenodo ref avec eYFP ??

```bash
#Download the transcriptome files to the reference folder and unzip it
wget link -o $WORKING_DIR/01_FASTQ_Preprocessing/data/Reference/
```

In order to prepare the environment for analysis execution, it is required to:
- Clone this github repository and set the WORKSPACE variable
- Download the Cell ranger and CITEseq count Singularity image tar file
- Load Singularity image on your system
- Download raw files to perform the analysis

#### Clone Github repository
Use your favorite method to clone this repository in a chosen folder.This will create a "MycPten" folder with all the source code. <br/>
You must set an environment variable called WORKING_DIR with a value set to the path to this folder.

revoir cette histoire de workin dir quand clone a test


#### Singularity Images
Singularity image tar file is stored on Zenodo. Open a shell ..... give instruction to where put it


#### Run the preprocessing
