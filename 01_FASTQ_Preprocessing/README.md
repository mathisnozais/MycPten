# FASTQ Preprocessing
## Overview
This folder contain the instructions and material to reproduce fastq pre-processing reported in the article. Required data and Singularity images are respectively available in SRA and Zenodo. Intructions to reproduce the analysis are provided below.
To reproduce the analysis, you have to first, prepare the environments (see "Prerequisites" section below), then execute the analysis described in the "Run the analysis" section below.

If you don't want to redo data pre-processing you can directly go to [02_Seurat_analysis](02_Seurat_analysis/README.md)

---

## Setup the experiment
### Prerequisites
In order to prepare the environment for analysis execution, it is required to:
- Clone this github repository and set the WORKING_DIR variable
- Download reference genome
- Download the Cell ranger and CITEseq count Singularity image tar file
- Load Singularity image on your system
- Download raw files to perform the analysis

#### Clone Github repository
Use your favorite method to clone this repository in a chosen folder. This will create a "MycPten" folder with all the source code. <br/>
You must set an environment variable called WORKING_DIR with a value set to the path to this Myc_Pten folder. For instance, if I clone the Git repository in "/home/nozais/workspace", then the WORKING_DIR variable will be set to :

```bash
export WORKING_DIR=/home/nozais/workspace/Myc_Pten
```

#### Reference Genome
The original version of the tanscriptome used is available at 10xGenomics website (http://cf.10xgenomics.com/supp/cell-exp/refdata-cellranger-mm10-3.0.0.tar.gz). We modify it in order to add eYFP. Thus the mm10-eYFP transcriptome can be download in Zenodo.

```bash
#Download the eYFP-transcriptome files to the reference folder
wget $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Reference/ https://zenodo.org/record/4636520/files/genome.fa?download=1
wget $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Reference/ https://zenodo.org/record/4636520/files/genes.gtf?download=1
```

#### Singularity Images
Singularity image.tar files are stored on Zenodo.

```bash
#Download the singularity images
# To download CellRanger
wget -P $WORKING_DIR/Images/Singularity/MycPten_Cellranger https://zenodo.org/record/4636520/files/cellranger2.1.0.img?download=1

# To download CiteSeqCount
wget -P $WORKING_DIR/Images/Singularity/MycPten_CITE https://zenodo.org/record/4636520/files/citeseqcount141_image.tar?download=1

```
#### Launch Singularity images
Singularity must be installed on your system. In order to execute analysis, you must first launch the singularity image you want to use. See https://singularity.lbl.gov/quickstart for details on Singularity installation.


#### Download RAW Files
Fastq files available on SRA
To processed with cell ranger :
- rep1_mRNA
- rep2_mRNA

To processed with CITEseq Count:
- rep1_HTO
- rep2_HTO
- rep2_ADT

```bash
#Download the Fastq files
wget $WORKING_DIR/03_Data/Fastq/ link SRA
wget $WORKING_DIR/03_Data/Fastq/
wget $WORKING_DIR/03_Data/Fastq/
wget $WORKING_DIR/03_Data/Fastq/
```

### Run the Fastq preprocessing
#### CellRanger
Input : Fastq files download from SRA (SRP311697)link to check number when public data release <br/>
Output : The ouput directory contains the classical cellranger output with the pre-processed data that is used later in the Seurat analysis
- mRNA count per cells
  - mRNA_barcodes.tsv.gz
  - mRNA_features.tsv.gz
  - mRNA_matrix.mtx.gz

and it also produce an html report.

To run cell ranger:
```bash
# Launch singularity image
singularity shell $WORKING_DIR/MycPten/Images/Singularity/MycPten_Cellranger/cellranger2.1.0.img

bash

#Go to the output directory
cd  $WORKING_DIR/MycPten/01_FASTQ_Preprocessing/02_Output

#Run CellRanger
#replace by good link to file
#Replicate 1
nohup /usr/local/share/cellranger/cellranger-2.1.0/cellranger count --id=MycPten_mm10_rep_1_mRNA --expect-cells=6000 --transcriptome=$WORKING_DIR/01_FASTQ_Preprocessing/Reference/cellranger_mm10-eYFP --fastq=$WORKING_DIR/03_Data/Fastq/ --sample=rep1_mRNA &

#Replicate 2
nohup /usr/local/share/cellranger/cellranger-2.1.0/cellranger count --id=MycPten_mm10_rep2_mRNA --expect-cells=6000 --transcriptome=$WORKING_DIR/01_FASTQ_Preprocessing/Reference/cellranger_mm10-eYFP --fastq=$WORKING_DIR/03_Data/Fastq/ --sample=rep2_mRNA &
```
Once the analysis is done, you should get result files in the WORKING_DIR/01_FASTQ_Preprocessing/02_Output folder (with the newly created "MycPten_mm10_rep_1_mRNA" and rep2 folder)

#### cite-seq-Count
input : Fastq files are avaible in SRA (SRP311697). To check number when public data release <br/>
output : The ouput directory contains the classical CiteSeqCount output with the pre-processed data that is used later in the Seurat analysis and a hmtl report.
- HTO count per cells
  - HTO_barcodes.tsv.gz
  - HTO_features.tsv.gz
  - HTO_matrix.mtx.gz

And only for replicate 2 :
- ADT count per cells
  - ADT_barcodes.tsv.gz
  - ADT_features.tsv.gz
  - ADT_matrix.mtx.gz

To run :
```bash
# Launch singularity image
singularity shell $WORKING_DIR/Images/Singularity/MycPten_CITE/citeseqcount141_image.tar

bash

#Go to the output directory
cd /MycPten/01_FASTQ_Preprocessing/02_Output

#FOR REPLICATE 1
# HTO
CITE-seq-Count -R1 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Fastq/rep1_HTO_S2_R1.fastq.gz -R2 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Fastq/rep1_HTO_S2_R2.fastq.gz -t $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/HTOlist_rep1.csv -cbf 1 -cbl 16 -umif 17 -umil 26 --max-errors 2 -cell 40000 -o MycPten_rep1_HTO

#FOR REPLICATE 2
#HTO
CITE-seq-Count -R1 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Fastq/rep2_HTO_S2_R1.fastq.gz -R2 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Fastq/rep2_HTO_S2_R2.fastq.gz -t $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/HTOlist_rep2.csv -cbf 1 -cbl 16 -umif 17 -umil 26 --max-errors 2 -cell 40000 -o MycPten_rep2_HTO

#ADT
CITE-seq-Count -R1 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Fastq/rep2_ADT_S3_R1.fastq.gz -R2 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Fastq/rep2_ADT_S3_R2.fastq.gz -t $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/ADTlist_rep2.csv -cbf 1 -cbl 16 -umif 17 -umil 26 --max-errors 2 -cell 40000 -o MycPten_rep2_ADT
```
