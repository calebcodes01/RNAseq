trim_galore -q 20 --paired cont1_1.fastq cont1_2.fastq
ls *_R1.fastq.gz | cut -d "_" -f 1 > seqlist
for filn in `cat seqlist`; do trim_galore -q 20 --paired $filn"_R1.fastq.gz" $filn"_R2.fastq.gz"; done
bwa index pa14.fna 
for filn in `cat seqlist`; do bwa mem pa14.fna $filn"_R1_val_1.fq.gz" $filn"_R2_val_2.fq.gz" | samtools sort | samtools view -F 4 -o $filn".sorted.bam"; done
for filn in *sorted.bam; do samtools index $filn; done
grep -P "\tCDS\t" pa14.gff | cut -f 1,4,5 > pa.bed
for filn in 'cat seqlist'; do multiBamCov -bams $filn".sorted.bam -bed pa.bed > pa-bwa.counts.txt; done
grep -P "\tCDS\t" pa14.gff | cut -f 9 | cut -d "=" -f 3 | sed "s/gene-PA_//" | sed "s/;.*//" > pa_tags.txt
paste sa_tags.txt pa-bwa.counts.txt | cut -f 1,5-8 > pa-bwa.countsR.txt 


library(DESeq2)
BiocManager::install("tximport")
library(tximport)
files = file.path(c("544_quant.sf", "221_quant.sf", "222_quant.sf"))
names(files) <- c("544", "221", "222")
txi = tximport(files, 'salmon', txOut=TRUE)
ColData <- read.table("ColData.txt", header=TRUE, sep = '\t')
dds = DESeqDataSetFromTximport(txi, ColData, ~Condition)
dds <- dds[rowSums(counts(dds)) >100, ]
dds <- DESeq(dds)
res <- results(dds, contrast=c("Condition", "ko", "control"))
write.table(res, file="544_DESeq2_results.txt", sep='\t')
