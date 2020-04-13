# SARS-CoV-2_pipeline
SARS-CoV-2 analysis pipeline for multiplex-PCR MPS(Massive Parrallel Sequencing) data.

## Introduction
This pipeline could accurately and efficiently identify SARS-CoV-2 reads from multiplex PCR sequencing data, and report the infection status of sequencing samples with positive/negative/uncertain label. At the same time, pipeline could get the vatiant information of each sample such as SNP/INDEL, which then helps generate the consensus sequence of SARS-CoV-2 genome. All of results are merged into an html report.

![Image](https://github.com/BGI-IORI/nCoV/blob/master/Image.png)

## Requirements:
Before running this pipeline, you need to make sure that several pieces of software and/or modules are installed on the system:  

perl: v5.26.0  
python: v3.4.3  
R: v3.3.2

Library for python3 and R:  
* python3: pysam  
* R: Cairo

Softwares for data quality control:  
* seqtk v1.2 (https://github.com/lh3/seqtk)
* SOAPnuke v1.5.6 (https://github.com/BGI-flexlab/SOAPnuke)  

Software for alignment and bam file statistics:
* BWA v0.7.16 (https://github.com/lh3/bwa)
* Samtools v1.3 (https://github.com/samtools/samtools)
* bamdst v1.0.6 (https://github.com/shiquan/bamdst)  

Software for variant calling:  
* freebayes v1.3.0 (http://cab.spbu.ru/software/spades/)  

Other required softwares:  
* bedtools v2.26.0 (https://bedtools.readthedocs.io/en/latest/)
* bcftools v1.6 (https://github.com/samtools/bcftools/)
* tabix v1.9 (https://github.com/samtools/tabix/)
* bgzip v1.9 (https://github.com/samtools/tabix/)
* mosdepth v0.2.9 (https://github.com/brentp/mosdepth)

## Installation

To clone the repository:

    git clone https://github.com/meizhiying/UAP.git


Notes: The above dependent software needs to be installed separately according to their instructions. After installing, the users should edit the input.json file, and change the software path to your own path.


## Usage
### 1.Prepare the input.json file
The details for input.json file are as follows:
* FqType, sequencing type(PE100/SE50). 
* sample_list, sample list file(sample_name/barcode_information/data_path).  
* workdir, analysis result directory.  
* SplitData, downsampling size of each sample(1G/1M/1K).
* consensus_depth, threshold of the point depth in consensus sequence,below which the point will be signed as 'N'.
* python3, path to python3.
* python3_lib, path to python3 library.
* Rscript, path to Rscript.
* R_lib, path to R library.
* tools(bwa,samtools....), path to this tool.

### 2.Run the pipeline.
```
python3 Main_SARS-CoV-2.py -i input.json 
cd path/to/workdir
nohup sh main.sh &
```
### 3.Analysis result.
1.Quality control result
```
path/to/workdir/result/*/05.Stat/QC.xlsx
```
2.Identification result
```
path/to/workdir/result/*/05.Stat/Identification.xlsx
```
3.Variant calling result
```
path/to/workdir/result/*/05.Stat/*.vcf.gz
path/to/workdir/result/*/05.Stat/*.vcf.anno
```
4.HTML report
```
path/to/workdir/result/*/05.Stat/*.html
```
