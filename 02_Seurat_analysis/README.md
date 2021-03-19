# Seurat analysis
## Overview
This repository describes how the scRNAseq data analysis was performed with Seurat. It contains the instructions and material to reproduce the analysis reported in the article.
Source code is directly available in the github repository (link).
Html report produce through the analysis is directly availabe (link).

Required data, builded Docker images and Robj are all available in SRA/GEO and Zenodo. Intructions to reproduce the analysis are provided below.

## Setup the experiment
### Prerequisites
Docker container images are available on zenodo : link

In order to prepare the environment for analysis execution, it is required to:
- Clone this github repository and set the WORKSPACE variable
- Download the RStudio / Seurat docker image tar file
- Load the docker image on your system
- Download files to perform the analysis

### Clone Github repository
Use your favorite method to clone this repository in a chosen folder.This will create a "MycPten" folder with all the source code. <br/>
You must set an environment variable called WORKING_DIR with a value set to the path to this folder.

revoir cette histoire de workin dir quand clone a test

### Docker images
Docker image tar file is stored on Zenodo. Open a shell ..... give instruction to where put it
In order to execute analysis, you must load the provided docker images onto your Docker.

### Download files
 (au choix un des fichier pour commencer l'analyse soit au tout debut soit des save a des bout de code strategique)
- Files after Fastq Preprocessing (count matrix)
- Files after ... (Seurat object)

Experiment_preprocessing.rmd -->
to load our data and obtain our Seurat object before starting the analysis
You can either launch all the code (starting with count matrix) or launch only part of the code with our Robj.
If you want to launch only part of the code download Seurat_clean-subset1_tomerge_ Robj and put it in the Output folder the script will automaticaly skip the necessary chunk to generate those objects.




Seurat_analysis.Rmd --> to load our Seurat object and start a the analysis step
