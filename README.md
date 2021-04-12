# DNAfastqtoBigWig
Converts fastq.gz files into bigwig tracks for visusalization on UCSC browser or IGV.

Author: Mrutyunjaya Parida, David Price Lab, UIOWA

## Usage:
DNAfastqtoBigWig runs on Python 2.7+. It is a linux based, multi-thread capable, Next Generation Sequencing (NGS) data analysis program with a command line interface.
It looks for 10 parameters in the user input. If the number of parameters are less than 10 the program displays the following usage example and parameter description prior to exiting the run.
```
python DNAfastqtoBigWig <URL> \
                 <fastq folder> \
                 <sample #'s> \
                 <min insert> \
                 <max insert> \
                 <# of threads> \
                 <bowtie index> \
                 <chr size file> \
                 <genome assembly> \
                 <sample key>
                 
Example run: python  DNAfastqtoBigWig www.DNA-Seqdata.com /home/xyz-user/fastq-folder 1-10 18 1000 8 /home/xyz-user/hg38-bowtie-index /home/xyz-user/hg38-chrom.sizes hg38 samplekey.csv                 
```
### Parameter description:
```
URL: provide a link to download the data.
fastq folder: provide a path/foldername to download all the fastq files.
sample #'s: <int> provide the sample numbers such as 1-10 or 1-5,7-8 or for single sample 6-6.
min insert: <int> provide the minimum length of an insert.
max insert: <int> provide the maximum length of an insert.
threads: <int> provide the number of threads. For example, if there 80 threads available and 10 samples to process then you may assign atmost 8 threads for each sample.
bowtie index: provide the path to the combined index of only the genomes used in the sequencing. If you are trying to build a new index use bowtie-build.
chr size file: provide the path to the combined chromsome size fasta file of only the genomes used in the sequencing.
               If you are trying to generate a chromsome size file use samtools faidx combined.genome.fa
               and cut -f1,2 combined.genome.fa.fai > combined.genome.sizes.
genome assembly: provide a comma separated list of genome assemblies used in the sequencing such as hg38,KF297339.1,JQCY02.1
sample_key: provide sample key in a .csv format where sample#'s and sample names are separated by a comma or simply mention no.
```

### Output:
A BIGWIG folder is created where bigwig files for each sample can be found. Bigwig files can be loaded onto Integrative Genomics Viewer (IGV) to visualize the number of fragments aligned to any genomic position.
Based on the example run the BIGWIG folder should be under /home/xyz-user/fastq-folder/MAPPED/BIGWIG.
