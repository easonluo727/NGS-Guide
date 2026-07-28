# RNA-seq Environment Setup

This guide will help you setup the environment for RNA-seq on your PC. 

# Windows 

## 1. Install Linux on your Windows PC

Windows system alone cannot process RNA-Seq. To do RNA-Seq on our PC, you must install Linux System (WSL) first. 

* Open your Terminal/PowerShell on your PC

* Type `wsl -- install` and press Enter. This would automatically install WSL on your PC. 

* Wait until the installation is complete. Then restart your computer. 

* Open your Start Menu and search for Ubuntu. Then Open it.  

* A command prompt window will open. When prompted, create your own UNIX username and password. When typing in password, no symbols would appear on the command prompt window. After you finished creating your username and password, press Enter. 

Linux system should be successfully installed on your Windows PC by now. 

## 2. Set-up RNA-seq Environment 

After installing Linux, you can start installing tools necessary for bulk RNA analysis. 

* Open Ubuntu and a command prompt window will open.

* Enter the following code to install Miniconda3. Press Enter or input yes whenever a new line comes up. 

    wget -c https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
    bash  Miniconda3-latest-Linux-x86_64.sh

* Input the following code to set up environment rna_p3. p3 represents the version of python (which should be 3). Remember to enter conda rna_p3 environment before you start doing rna analysis.  

    conda create -n rna_p3 python=3              
    conda env list                                         Check the environment
    conda activate rna_p3                                  Enter conda environment
    conda deactivate                                       Exit current conda environment

* Install tools for bulk rna analysis after setting up rna_p3. You must enter conda environment before downloading these tools. You can use `conda install -y` to download each tool, but do not download too many tools simultaneously because it may produce error. The following are some examples. 

    conda install -y sra-tools  fastqc  multiqc  fastp                        
    conda install -y hisat2  subread  samtools=1.6  salmon star trimmomatic
    conda install -c bioconda bioconductor-deseq2

* Download R and RStudio on your PC. 

# MacOS

## 1. Install Conda

* Open your Terminal

* Download the Miniforge3 macOS Apple Silicon (arm64) installer from Conda-forge.

    bash Miniforge3-MacOSX-arm64.sh  

* Restart your computer after finishing installation. 

## 2. Set-up RNA-seq Environment 

* Add the necessary channels

    conda config --add channels defaults
    conda config --add channels bioconda
    conda config --add channels conda-forge
    conda config --set channel_priority strict

* Install tools for RNA-seq. 

    conda create -n rnaseq fastqc fastp hisat2 star subread samtools multiqc rstudio





