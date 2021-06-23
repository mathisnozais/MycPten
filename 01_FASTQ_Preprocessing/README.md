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
wget $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Reference/ https://zenodo.org/record/4636520/files/genome.fa
wget $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Reference/ https://zenodo.org/record/4636520/files/genes.gtf
```

#### Singularity Images
Singularity image.tar files are stored on Zenodo.

```bash
#Download the singularity images
# To download CellRanger
wget -P $WORKING_DIR/Images/Singularity/MycPten_Cellranger https://zenodo.org/record/4636520/files/cellranger2.1.0.img

# To download CiteSeqCount
wget -P $WORKING_DIR/Images/Singularity/MycPten_CITE https://zenodo.org/record/4636520/files/citeseqcount141_image.tar

```
#### Launch Singularity images
Singularity must be installed on your system. In order to execute analysis, you must first launch the singularity image you want to use. See https://singularity.lbl.gov/quickstart for details on Singularity installation.


#### Download RAW Files
Fastq files available on SRA. <br/>
To processed with cell ranger :
- rep1_mRNA
- rep2_mRNA

To processed with CITEseq Count:
- rep1_HTO
- rep2_HTO
- rep2_ADT

```bash
#Download the Fastq files
# HTO rep1
wget $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/ https://sra-download.ncbi.nlm.nih.gov/traces/sra4/SRR/013708/SRR14037861
# HTO rep2
wget $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/ https://sra-download.ncbi.nlm.nih.gov/traces/sra71/SRR/013708/SRR14037863
# mRNA rep1
wget $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/ https://sra-download.ncbi.nlm.nih.gov/traces/sra25/SRR/013708/SRR14037860
# mRNA rep2
wget $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/ https://sra-download.ncbi.nlm.nih.gov/traces/sra4/SRR/013708/SRR14037862
# ADT rep2
wget $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/ https://sra-download.ncbi.nlm.nih.gov/traces/sra48/SRR/013708/SRR14037864
```

### Run the Fastq preprocessing
#### CellRanger
Input : Fastq files download from SRA [SRP311697](https://trace.ncbi.nlm.nih.gov/Traces/sra/?study=SRP311697) <br/>
Output : The ouput directory will contain the classical cellranger output with the pre-processed data that is used later in the Seurat analysis
- mRNA count per cells
  - mRNA_barcodes.tsv.gz
  - mRNA_features.tsv.gz
  - mRNA_matrix.mtx.gz

and it also produce an html report.

To run cell ranger:
```bash
# Launch singularity image
singularity shell $WORKING_DIR/Images/Singularity/MycPten_Cellranger/cellranger2.1.0.img

bash

#Go to the output directory
cd  $WORKING_DIR/01_FASTQ_Preprocessing/02_Output

#Run CellRanger
#replace by good link to file
#Replicate 1
nohup /usr/local/share/cellranger/cellranger-2.1.0/cellranger count --id=MycPten_mm10_rep_1_mRNA --expect-cells=6000 --transcriptome=$WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Reference/cellranger_mm10-eYFP --fastq=$WORKING_DIR/03_Data/FASTQ/ --sample=rep1_mRNA &

#Replicate 2
nohup /usr/local/share/cellranger/cellranger-2.1.0/cellranger count --id=MycPten_mm10_rep2_mRNA --expect-cells=6000 --transcriptome=$WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Reference/cellranger_mm10-eYFP --fastq=$WORKING_DIR/03_Data/FASTQ/ --sample=rep2_mRNA &
```
Once the analysis is done, you should get result files in the WORKING_DIR/01_FASTQ_Preprocessing/02_Output folder (with the newly created "MycPten_mm10_rep_1_mRNA" and rep2 folder)

#### cite-seq-Count
input : Fastq files are avaible in [SRP311697](https://trace.ncbi.nlm.nih.gov/Traces/sra/?study=SRP311697) <br/>
output : The ouput directory will contain the classical CiteSeqCount output with the pre-processed data that is used later in the Seurat analysis.
- HTO count per cells
  - HTO_barcodes.tsv.gz
  - HTO_features.tsv.gz
  - HTO_matrix.mtx.gz

And only for replicate 2 :
- ADT count per cells
  - ADT_barcodes.tsv.gz
  - ADT_features.tsv.gz
  - ADT_matrix.mtx.gz

Execution :
```bash
# Launch singularity image
singularity shell $WORKING_DIR/Images/Singularity/MycPten_CITE/citeseqcount141_image.tar

bash

#Go to the output directory
cd /MycPten/01_FASTQ_Preprocessing/02_Output

#FOR REPLICATE 1
# HTO
CITE-seq-Count -R1 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep1_HTO_S2_R1.fastq.gz -R2 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep1_HTO_S2_R2.fastq.gz -t $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/HTOlist_rep1.csv -cbf 1 -cbl 16 -umif 17 -umil 26 --max-errors 2 -cell 40000 -o MycPten_rep1_HTO

#FOR REPLICATE 2
#HTO
CITE-seq-Count -R1 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep2_HTO_S2_R1.fastq.gz -R2 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep2_HTO_S2_R2.fastq.gz -t $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/HTOlist_rep2.csv -cbf 1 -cbl 16 -umif 17 -umil 26 --max-errors 2 -cell 40000 -o MycPten_rep2_HTO

#ADT
CITE-seq-Count -R1 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep2_ADT_S3_R1.fastq.gz -R2 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep2_ADT_S3_R2.fastq.gz -t $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/ADTlist_rep2.csv -cbf 1 -cbl 16 -umif 17 -umil 26 --max-errors 2 -cell 40000 -o MycPten_rep2_ADT
```
