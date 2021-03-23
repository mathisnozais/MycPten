# Seurat analysis
## Overview
This repository describes how the scRNAseq data analysis was performed with Seurat. It contains the instructions and material to reproduce the analysis reported in the article.
Source code is directly available in the github repository (link).
Html report produce through the analysis is directly availabe (link).

Required data, builded Docker images and Robj are all available in SRA/GEO and Zenodo. Intructions to reproduce the analysis are provided below.

---

## Setup the experiment
### Prerequisites
Docker container images are available on zenodo : link

In order to prepare the environment for analysis execution, it is required to:
- Clone this github repository and set the WORKSPACE variable
- Download the RStudio / Seurat docker image tar file
- Load the docker image on your system
- Download files to perform the analysis

#### Clone Github repository
Use your favorite method to clone this repository in a chosen folder.This will create a "MycPten" folder with all the source code. <br/>
You must set an environment variable called WORKING_DIR with a value set to the path to this folder.

revoir cette histoire de workin dir quand clone a test

#### Docker images
Docker image tar file is stored on Zenodo. Open a shell ..... give instruction to where put it
In order to execute analysis, you must load the provided docker images onto your Docker.Docker must be installed on your system. See https://docs.docker.com/install/ for details on Docker installation.
give code example
```bash
code to put here
```
#### Download data
The preprocessed data are already in this github, alternatively you can download different files to start the analysis at different entry point: (attention a ajouter ! )
- Files after Fastq Preprocessing (count matrix) --> already in github folder or use what you produce with 01_FASTQ_Preprocessing
- Preprocessed Seurat objects
- Final integrate object

### Run the R/Seurat analysis
Analysis can be directly run inside docker containers by compiling Rmarkdown files. The Rmarkdown file compilation will launch the required analysis for the step and produce a final HTML report.

NB : An already generated report is available in the <WORKING_DIR>/1-Seurat_analysis/output.

There is two different Seurat script :
- Experiment_preprocessing.rmd
to load our data and obtain our Seurat object before starting the analysis
You can either launch all the code (starting with count matrix) or launch only part of the code with our Robj.
If you want to launch only part of the code download Seurat_clean-subset1_tomerge_ Robj and put it in the Output folder the script will automaticaly skip the necessary chunk to generate those objects.

- Seurat_analysis.Rmd --> to load our Seurat object and start a the analysis step
