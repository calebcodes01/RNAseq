#Trim galore trims adaptors and requires a minimum depth of 20. The input files are paired-end .fastq files (1 being the forward read and 2 the reverse)
trim_galore -q 20 --paired cont1_1.fastq cont1_2.fastq

#This can be done on many files using a for loop. The next two commands make a list "seqlist" which will contain the unique name for every file with the given extension "_R1.fastq.gz" and iterates trim_galore across every pair of files in "seqlist".

ls *_R1.fastq.gz | cut -d "_" -f 1 > seqlist
for filn in `cat seqlist`; do trim_galore -q 20 --paired $filn"_R1.fastq.gz" $filn"_R2.fastq.gz"; done

#indexing the reference genome
bwa index pa14.fna 

#Mapping trimmed reads to a reference genome and using samtools to sort the alignment and convert to a .bam file for downstream use.
bwa mem pa14.fna filename_R1_val_1.fq.gz" filename_R2_val_2.fq.gz" | samtools sort | samtools view -F 4 -o filename.sorted.bam

#Can be done on many files using a for loop.
for filn in `cat seqlist`; do bwa mem pa14.fna $filn"_R1_val_1.fq.gz" $filn"_R2_val_2.fq.gz" | samtools sort | samtools view -F 4 -o $filn".sorted.bam"; done

#Before counting the number of reads that map to a CDS, the .sorted.bam files need to be indexed, I like to do this all at once.
for filn in *sorted.bam; do samtools index $filn; done

#This line extracts only coding sequences from the reference .gff file and renames it to a new file "pa14.bed
grep -P "\tCDS\t" GCF_006974045.1_ASM697404v1_genomic.gff | cut -f 1,4,5 > pa14.bed

#Counting the number of reads. Ideally, this is done with duplicate samples.
multiBamCov -bams file1.sorted.bam file1_duplicate.sorted.bam file2_.sorted.bam file2_duplicate.sorted.bam -bed pa14.bed > pa-bwa.counts.txt

#The next three lines will clean up our output and give each line a unique and meaningful name.
grep -P "\tCDS\t" GCF_006974045.1_ASM697404v1_genomic.gff | cut -f 9 | cut -d "=" -f 3 | sed "s/gene-PA_//" | sed "s/;.*//" > pa_tags.txt
paste pa_tags.txt pa-bwa.counts.txt | cut -f 1,5-8 > pa-bwa.countsR.txt
sed -i 's/gene-EIP97_//' pa-bwa.countsR.txt

#DESEQ will not allow duplicate values so to get rid of them.
cut -f 1 pa-bwa.countsR.txt | sort | uniq -c > newfile.countsR.txt

#At this point, "pa-bwa.countsR.txt" can be downloaded and opened in excel or opened with a text editor. Each column needs to be given a header. There should be four columns, a list of counts for each of the 4 samples inputed into multiBamCov. I usually name the columns 1,2,3,4.
