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

```bash
#Download the singularity images
wget link -o $WORKING_DIR/Images/
```

Singularity must be installed on your system. In order to execute analysis, you must first launch the singularity image you want to use

#### Download raw Files
Fastq files available on SRA link
To processed with cell ranger :
- nanan
- nana

To processed with CITEseq Count:
- nanan
- nanan

### Run the preprocessing
#### CellRanger
input :
output :

To run :

```bash
# Launch singularity image
singularity shell /MycPten/Images/Singularity/MycPten_Cellranger/cellranger2.1.0.img

bash

#Go to the output directory
cd /MycPten/01_FASTQ_Preprocessing/Output

#Run CellRanger
#replace by good like to file
nohup /usr/local/share/cellranger/cellranger-2.1.0/cellranger count --id=MycPten_mm10 --expect-cells=6000 --transcriptome=/MycPten/01_FASTQ_Preprocessing/Reference/finish line --fastq= --sample=rep1_cDNA &

```
#### cite-seq-Count
input
Output

To run :
```bash
# concatenate FASTQ
to put code


# Launch singularity image
singularity shell /MycPten/Images/Singularity/MycPten_CITE/citeseqcount141_image.tar

bash

#Go to the output directory
cd /MycPten/01_FASTQ_Preprocessing/Output
```
