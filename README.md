# DNAfastqtoBigWig
Converts fastq.gz files into bigwig tracks for visusalization on UCSC browser or IGV.

Author: Mrutyunjaya Parida, David Price Lab, UIOWA

## Usage:
DNAfastqtoBigWig runs on Python 2.7+. It is a linux based, multi-thread capable, Next Generation Sequencing (NGS) data analysis program with a command line interface.
It checks for 10 parameters in the user input. If the number of parameters are less than 10 the program displays the following usage example and parameter description prior to exiting the run.This program is written to accomodate the fastq sample file structures of PriceLab. We receive 3 fastq files for each sample R1 (forward), R2 (UMI info), and R3(reverse). To download DNAfastqtoBigWig use this link: "link to be provided". The program folder contains installations of samtools, bedtools, trim_galore, and bedGraphToBigWig. Please run DNAfastqtoBigWig from the program folder. This program was published in https://pubmed.ncbi.nlm.nih.gov/35048979/.

```
python DNAfastqtoBigWig.py <URL> \
                 <fastq folder> \
                 <sample #'s> \
                 <min insert> \
                 <max insert> \
                 <# of threads> \
                 <bowtie index> \
                 <chr size file> \
                 <genome assembly> \
                 <sample key>
                 
Example run: python  DNAfastqtoBigWig www.DNA-Seqdata.com /home/xyz-user/fastq-folder 1-10 18 \
             1000 8 /home/xyz-user/genome-bowtie-index /home/xyz-user/genome-chrom.sizes hg38,KF297339.1 samplekey.csv                 
```

Note: The genome-bowtie-index consists of both the human (hg38) and the HCMV TB40e (KF297339.1) genomes. To create a bowtie index like this I combined the human and HCMV genomes into one fasta file and ran bowtie-build on this combined.fasta file.I used a minimum insert length of 18bp and maximum insert length of 1000bp. My goal is retain all fragments between 18-1000bp for further analysis. Please consider the strategy suitable for your sequencing library.

### Parameter description:
```
URL: provide a link to download the data.
fastq folder: provide a path/foldername to download all the fastq files.
sample #'s: <int> provide the sample numbers such as 1-10 or 1-5,7-8 or for single sample 6-6.
min insert: <int> provide the minimum length of an insert.
max insert: <int> provide the maximum length of an insert.
threads: <int> provide the number of threads. For example, if there are 80 threads available and 10 samples to process then you may assign atmost 8 threads for each sample.
bowtie index: provide the path to the combined index of all the genomes that part of your library. If you are trying to build a new index use bowtie-build.
chr size file: provide the path to the combined chromsome size fasta file of only the genomes used in the sequencing.
               If you are trying to generate a chromsome size file use samtools faidx combined.genome.fa
               and cut -f1,2 combined.genome.fa.fai > combined.genome.sizes.
genome assembly: provide a comma separated list of genome assemblies used in the sequencing such as hg38,KF297339.1.
sample_key: provide sample key in a .csv format where sample#'s and sample names are separated by a comma as follows:
            Sample1,Control1
            Sample2,Control2
            Sample3,Exp1
            Sample4,Exp2
            or simply mention no.

```
## Requirements:
Python libraries: ``` joblib, and glob. ```

Software requirements: ``` zcat (v 1.10), samtools(v1.14), bedtools(v2.29.1), bowtie(1.3.1), trim_galore(0.6.0), and bedGraphToBigWig(v4). ```

This program is designed to run on paired end data only. Sample file names must follow the following format and order:

Format:
```
Sample#_lane#_yearmonthdate000_Sequencing#_Lane#_Read#_001.fastq.gz
```
Order:

Sample1_lane1_20200324000_S1_L001_R1_001.fastq.gz (forward)

Sample1_lane1_20200324000_S1_L001_R2_001.fastq.gz (UMI sequences for deduping)

Sample1_lane1_20200324000_S1_L001_R3_001.fastq.gz (reverse)

Path to trim_galore,samtools, bedtools, bowtie, and bedGraphtoBigWig installations are hardcoded inside this program. They can be changed based on user preferences.

Fastq files must be in fastq.gz format for the program to run. 

Adapter sequences are hard coded but can be changed as per the users preference in the TRIM function.

Samples sequenced in 2 lanes are automatically merged into one alignment file as long the lane #'s are mentioned in the sample file name following the above format.

Please make sure that the sample numbers are mentioned in Sample# format without a delimiter. If sample numbers are mentioned such as Sample_# the program will produce errors and exit.

### Output:
A BIGWIG folder is created where bigwig files for each sample can be found. Bigwig files can be loaded onto Integrative Genomics Viewer (IGV) to visualize the number of fragments aligned to any genomic position.

Based on the example run the BIGWIG folder should be under /home/xyz-user/fastq-folder/MAPPED/BIGWIG.
