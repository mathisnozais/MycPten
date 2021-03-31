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
Docker container images are available on zenodo : https://doi.org/10.5281/zenodo.4636520

In order to prepare the environment for analysis execution, it is required to:
- Clone this github repository and set the WORKSPACE variable
- Download the RStudio / Seurat docker image tar file
- Load the docker image on your system
- Download files to perform the analysis on Zenodo https://doi.org/10.5281/zenodo.4636520

#### Clone Github repository
Use your favorite method to clone this repository in a chosen folder.This will create a "MycPten" folder with all the source code. <br/>
You must set an environment variable called WORKING_DIR with a value set to the path to this MycPten folder.

revoir cette histoire de workin dir quand clone a test

#### Docker images
Docker image tar file is stored on Zenodo. Open a shell ..... give instruction to where put it
In order to execute analysis, you must load the provided docker images onto your Docker.Docker must be installed on your system. See https://docs.docker.com/install/ for details on Docker installation.
give code example

```bash
# To download Seurat301v2
wget -P $WORKING_DIR/Images https://zenodo.org/record/4636520/files/Seurat301v2.tar?download=1
```
#### Download data
The preprocessed data are already in this github (MycPten/02_Seurat_analysis/03_Data), alternatively you can download different files to start the analysis at different entry point:
- Experiment_preprocessing.rmd
  - Files after Fastq Preprocessing (count matrix) are already in github repository
  - Preprocessed Seurat objects of each replicate
  - First integration object Seurat-integrated_rep1_rep2
- Experiment_analysis.rmd
  - Final integrate object to launch the scRNAseq analysis T-Seurat-merged_clean-subset

```bash
#Link to all data available for Seurat Analysis
  ## Preprocessed Seurat object for rep1 and 2
wget -P $WORKING_DIR/02_Seurat_analysis/02_Output https://zenodo.org/record/4636520/files/Seurat_clean-subset_tomerge_replicate1.Robj?download=1
wget -P $WORKING_DIR/02_Seurat_analysis/02_Output https://zenodo.org/record/4636520/files/Seurat_clean-subset_tomerge_replicate2.Robj?download=1

  ## Integrate object
wget -P $WORKING_DIR/02_Seurat_analysis/02_Output https://zenodo.org/record/4636520/files/Seurat-integrated_rep1_rep2.Robj?download=1

  ## Final integrate object
wget -P $WORKING_DIR/02_Seurat_analysis/02_Output https://zenodo.org/record/4636520/files/T-Seurat-merged_clean-subset.Robj?download=1
```

### Run the R/Seurat analysis
Analysis can be directly run inside docker containers by compiling Rmarkdown files. The Rmarkdown file knit compilation will launch the required analysis for the step and produce a final HTML report.
You will need a function R script that can be download here:
```bash
#Function download
  wget -P $WORKING_DIR/02_Seurat_analysis/01_Script https://zenodo.org/record/4636520/files/Workflow_function.R?download=1
```

NB : An already generated report is available in the <WORKING_DIR>/1-Seurat_analysis/output.

- Experiment_preprocessing.rmd <br/>
You can either launch all the code (starting with count matrix in repository by default) or launch only part of the code with our intermediate Robj.
If you want to launch only part of the code download necessary object and put it in the Output folder the script will automatically skip the unnecessary chunk.
- Seurat_analysis.Rmd <br/>
Download and put in the Output folder the merge object (https://doi.org/10.5281/zenodo.4636520)
