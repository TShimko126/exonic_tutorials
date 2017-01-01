# Illumina's bcl2fastq2 conversion software
Congratulations, your sequencing run was a success and now you need to process the data. 

Depending on how much preprocessing was done by the sequencer software, the outputed data exists as \*.bcl and/or \*.fastq files. The \*.bcl files can be thought of as the rawest form of sequencing data, essentially the sequencing instrument's readout in binary code. The \*.bcl files are used to make \*.fastq files, which are formatted text files that contain information about each sequencing read. This is where bcl2fastq2 comes in!

The bcl2fastq2 program is especially important for multiplexed libraries because the \*.bcl to \*.fastq conversion step is when demultiplexing happens. 

## Table of contents
1) Requirements
2) Installation
3) Usage

## Requirements
* Data generated with Illumina's MiSeq, HiSeq 4000, 3000, 2500, and 2000, NextSeq, and HiSeq X Systems
* Ubuntu server

## Installation
* Install dependencies
```{ubuntu}
sudo apt-get update # retreives newly-released updates
sudo apt-get upgrade # upgrades existing packages
sudo apt-get install zlibc # installs on-fly auto-uncompressing C library
sudo apt-get install libc6 # installs GNU C library 
sudo apt-get install gcc # installs GNU C compiler
sudo apt-get install g++ # installs GNU C++ compiler
sudo apt-get install libboost1.54-all-dev # installs Boost C++ Libraries development files
sudo apt-get install cmake # installs make system
sudo apt-get install alien --assume-yes # install alien installation utility
```
* Download and install
```{ubuntu}
wget ftp://webdata2:webdata2@ussd-ftp.illumina.com/downloads/software/bcl2fastq/bcl2fastq2-v2.17.1.14-Linux-x86_64.zip # download Linux bcl2fastq2 (check Illumina downloads page for newer versions)
unzip bcl2fastq2-v2.17.1.14-Linux-x86_64.zip # unzip to *.rpm file
sudo alien bcl2fastq2-v2.17.1.14-Linux-x86_64.rpm # install bcl2fastq2
sudo dpkg -i bcl2fastq2_0v2.17.1.14-2_amd64.deb # associated deb package handling
```
* Remove installation files
```{ubuntu}
rm bcl2fastq2-v2.17.1.14-Linux-x86_64.zip bcl2fastq2-v2.17.1.14-Linux-x86_64.rpm bcl2fastq2-v2.17.1.14-Linux-x86_64.deb # remove installation files
```

## Usage
* Complete the SampleSheet.csv file: A preformatted spreadsheet to specify multiplexing barcode sequences.
* Change directory into runfolder (e.g. 170101\_M00904\_0102_000000000-AXXHN) and execute bcl2fastq2 to run with default settings
```{ubuntu}
cd <runfolder-dir>
bcl2fastq
```
* Output *.fastq.gz files (e.g. barcode1\_S1\_L001\_R1_001.fastq.gz) written to <runfolder-dir>/Data/Intensities/BaseCalls/
* Use the gunzip utility to unpack compressed files to *.fastq
```{unbuntu}
gunzip -d <runfolder-dir>/Data/Intensities/BaseCalls/*.fastq.gz
```
* For custom settings (e.g. resource allocation, adapter/barcode processing, file output), check out the available options: 
```{ubuntu}
bcl2fastq -h
```