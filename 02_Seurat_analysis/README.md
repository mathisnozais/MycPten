# Seurat analysis
## Overview
This repository describes how the scRNAseq data analysis was performed with Seurat. It contains the instructions and material to reproduce the analysis reported in the article.To reproduce the analysis, you have to first, prepare the environments (see "Prerequisites" section below), then execute the analysis described in the "Run the analysis" section below.
Source code is directly available in the github repository (https://github.com/mathisnozais/MycPten/02_Seurat_analysis/01_Script).
Html report produce through the analysis is directly availabe (https://github.com/mathisnozais/MycPten/02_Seurat_analysis/02_Output).
The Seurat analysis is divided in two script :
- *Experiment_preprocessing.rmd* to load our data and obtain our final Seurat object before starting the scRNA seq analysis
- *Experiment_analysis.rmd* to start the scRNA seq analysis

You can also just generate the plot used in the paper :
- *Figure.rmd*

Required data, builded Docker images and Robj are all available in SRA/GEO and Zenodo. Instructions to reproduce the analysis are provided below.

---

## Setup the experiment
### Prerequisites
Docker container images are available on [zenodo](https://doi.org/10.5281/zenodo.4636520).

In order to prepare the environment for analysis execution, it is required to:
- Clone this github repository and set the WORKING_DIR variable
- Download the RStudio / Seurat docker image tar file
- Load the docker image on your system
- Download files to perform the analysis on [zenodo](https://doi.org/10.5281/zenodo.4636520)

#### Clone Github repository
Use your favorite method to clone this repository in a chosen folder.This will create a "MycPten" folder with all the source code. <br/>
You must set an environment variable called WORKING_DIR with a value set to the path to this Myc_Pten folder.
For instance, if I clone the Git repository in "/home/nozais/workspace", then the WORKING_DIR variable will be set to :

```bash
export WORKING_DIR=/home/nozais/workspace/Myc_Pten
```

#### Docker images
> :warning: In order to execute analysis, you must load the provided docker images onto your Docker. Docker must be installed on your system. See https://docs.docker.com/install/ for details on Docker installation.

Docker image file is stored on Zenodo :

```bash
# To download Seurat301v2
wget -P $WORKING_DIR/Images/Docker https://zenodo.org/record/4636520/files/Seurat301v2.tar?download=1
```
#### Download data
The fastq preprocessed data are already in this github (MycPten/02_Seurat_analysis/03_Data), alternatively you can download different files to start the analysis at different entry point:
- Experiment_preprocessing.rmd
  - Files after Fastq Preprocessing (count matrix) are already in this repository
  - Preprocessed Seurat objects of each replicate
  - First integration object : Seurat-integrated_rep1_rep2
- Experiment_analysis.rmd
  - Final integrate object, produce by Experiment_preprocessing, to launch the scRNAseq analysis : T-Seurat-merged_clean-subset

> :warning: **Do not move any data.**  When launching Experiment_preprocessing.rmd it will automatically detect if you run de 01_FASTQ_Preprocessing step and create output matrix. If not it will use our data in 02_Seurat_analysis/03_Data.

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
Analysis can be directly run inside docker containers by compiling Rmarkdown files. The Rmarkdown file knit compilation will launch the required analysis and produce a final HTML report.
You will need a function R script that can be download here:

//// add a command to ask to change WORKING_DIR inside R ??? a voir Delphine ///
```bash
#Function download
  wget -P $WORKING_DIR/02_Seurat_analysis/01_Script https://zenodo.org/record/4636520/files/Workflow_function.R?download=1
```

NB : An already generated report is available in xxx

- Experiment_preprocessing.rmd <br/>
You can either run all the code (starting with count matrix in repository by default) or run only part of the code with our intermediate Robj.
If you want to run only part of the code download the necessary object and put it in the Output folder the script will automatically skip the unnecessary chunk.
- Seurat_analysis.Rmd <br/>
Download and put in the Output folder the merge object (https://doi.org/10.5281/zenodo.4636520)
