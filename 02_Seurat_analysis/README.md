# Seurat analysis
## Overview
This repository describes how the scRNAseq data analysis was performed with Seurat. It contains the instructions and material to reproduce the analysis reported in the article.
Source code is directly available in the github repository (https://github.com/mathisnozais/MycPten/02_Seurat_analysis/01_Script).
Html report produce through the analysis is directly availabe (https://github.com/mathisnozais/MycPten/02_Seurat_analysis/02_Output).
The Seurat analysis is divided in two script :
- *Experiment_preprocessing.rmd* to load our data and obtain our final Seurat object before starting the scRNA seq analysis
- *Experiment_analysis.rmd* to start the scRNA seq analysis

Required data, builded Docker images and Robj are all available in SRA/GEO and Zenodo. Intructions to reproduce the analysis are provided below.

---

## Setup the experiment
### Prerequisites
Docker container images are available on zenodo : link

In order to prepare the environment for analysis execution, it is required to:
- Clone this github repository and set the WORKSPACE variable
- Download the RStudio / Seurat docker image tar file
- Load the docker image on your system
- Download files to perform the analysis on Zenodo (link)

#### Clone Github repository
Use your favorite method to clone this repository in a chosen folder.This will create a "MycPten" folder with all the source code. <br/>
You must set an environment variable called WORKING_DIR with a value set to the path to this MycPten folder.

revoir cette histoire de workin dir quand clone a test

#### Docker images
Docker image tar file is stored on Zenodo. Open a shell ..... give instruction to where put it
In order to execute analysis, you must load the provided docker images onto your Docker.Docker must be installed on your system. See https://docs.docker.com/install/ for details on Docker installation.
give code example
```bash
code to put here
```
#### Download data
The preprocessed data are already in this github (MycPten/02_Seurat_analysis/03_Data), alternatively you can download different files to start the analysis at different entry point:
- Experiment_preprocessing.rmd
  - Files after Fastq Preprocessing (count matrix) are already in github repository
  - Preprocessed Seurat objects of each replicate (link ZENODO)
  - First integration object (link ZENODO) Seurat-integrated_rep1_rep2
- Experiment_analysis.rmd
  - Final integrate object to launch the scRNAseq analysis (link ZENODO) T-Seurat-merged_clean-subset

```bash
  example code to put here
```

### Run the R/Seurat analysis
Analysis can be directly run inside docker containers by compiling Rmarkdown files. The Rmarkdown file knit compilation will launch the required analysis for the step and produce a final HTML report.

NB : An already generated report is available in the <WORKING_DIR>/1-Seurat_analysis/output.

- Experiment_preprocessing.rmd <br/>
You can either launch all the code (starting with count matrix in repository by default) or launch only part of the code with our intermediate Robj.
If you want to launch only part of the code download necessary object and put it in the Output folder the script will automatically skip the unnecessary chunk.
- Seurat_analysis.Rmd <br/>
Download and put in the Output folder the merge object (link ZENODO)
