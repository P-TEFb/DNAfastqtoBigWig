# DNAfastqtoBigWig
Converts fastq.gz files for a sample into bigwig tracks for data visusalization on UCSC browser or IGV.

## Usage:
DNAfastqtoBigWig <URL> <fastq folder> <sample #'s> <min insert> <max insert> <# of threads> <bowtie index> <chr size file> <genome assembly> <sample key>

### Parameter description:
```
URL: provide a link to download the data.
fastq folder: provide a path/foldername to download all the fastq files.
sample #'s: provide the sample numbers for DNASEQ such as 1-10 or 1-5,7-8 or for single sample 6-6.
min insert: <int> provide the minimum length of an insert.
max insert: <int> provide the maximum length of an insert.
threads: <int> provide the number of threads. For example, given there are 80 threads, you may assign a min of 1 or 8 threads for each of 10 samples.
bowtie index: provide the path to the combined index of only the genomes used in the sequencing. If you are trying to build a new index use bowtie-build.
chr size file: provide the path to the combined chromsome size fasta file of only the genomes used in the sequencing.
               If you are trying to generate a chromsome size file use samtools faidx combined.genome.fa
               and cut -f1,2 combined.genome.fa.fai > combined.genome.sizes.
genome assembly: provide a comma separated list of genome assemblies used in the sequencing such as hg38,KF297339.1,JQCY02.1
sample_key: provide sample key in a .csv format where sample#'s and sample names are separated by a comma or simply mention no.
```
