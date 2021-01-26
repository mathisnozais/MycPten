## TEST PULL
# Seurat analysis
## Overview
This repository describes how the scRNAseq data analysis was performed with Seurat. It contains the instructions and material to reproduce the analysis reported in the article (and more).

## Prerequisites
Docker container image is available on zenodo : link
Link to docker and load...

In order to prepare the environment for analysis execution, it is required to:
- Clone GIT ???
- Download the RStudio / Seurat docker image tar file
- Load the docker image on your system
- Download files (au choix un des fichier pour commencer l'analyse soit au tout debut soit des save a des bout de code strategique)


Download files
- Files after Fastq Preprocessing (count matrix)
- Files after ... (Seurat object)

Experiment_preprocessing.rmd -->
to load our data and obtain our Seurat object before starting the analysis
You can either launch all the code (starting with count matrix) or launch only part of the code with our Robj.
If you want to launch only part of the code download Seurat_clean-subset1_tomerge_ Robj and put it in the Output folder the script will automaticaly skip the necessary chunk to generate those objects.


Seurat_analysis.Rmd --> to load our Seurat object and start a the analysis step
