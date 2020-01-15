# rna-seq-date-download
step1: download SRR1542484
$ wget -c https://trace.ncbi.nlm.nih.gov/Traces/sra/?run=SRR1542484
step2: unzip
$ conda activate rna/fastq-dump --split-3 SRR1542484
step3: download genome index of human
$ wget -c ftp://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/hg38.chromFa.tar.gz # downlosad genome index
$ ftp://ftp.ccb.jhu.edu/pub/infphilo/hisat2/data/grch38.tar.gz  #anotherway $ bowtie2-build hg38.fa index_hg38 1>hg38.bowtie_index.log
$ tar -zxvf hg38.chromFa.tar.gz
$ cat *.fa > hg38.fa
$ rm -rf chr*
step4:  download annotation file
$ wget -c ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/001/405/GCF_000001405.39_GRCh38.p13/GCF_000001405.39_GRCh38.p13_genomic.gff.gz 
$ gunzip GCF_000001405.39_GRCh38.p13_genomic.gff.gz
step5: 
$ hisat2 -p 10 -x ../homo_sapiens/index_hg38.fa -1 SRR1542484_1.fastq -2 SRR1542484_2fastq -S SRR1542484.sam 2>> mapping_repo.txt
