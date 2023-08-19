# RNAseq data visualization of DEG's
This repository is a walkthrough on how to:

# Perform RNA-seq analyses: 
RNAseq_analysis.md

~  Trimming raw fastq reads
<br>
~  Map reads to a reference genome 
<br>
~  Quantify transcripts with Salmon
<br>
~  Perform DESeq2 analysis with Salmon output

# Visualize the data:
~  Install ggvolc and its dependencies (ggvolc_installation.md)
<br>
~  Uploading DESeq2 data (data_upload.md)
<br>
~  Generating volcano plots (making_figures.md)

# Citation information
List of packages, versions used, citations, and relevant links
 
```
ggvolc v0.1.0
https://github.com/loukesio/ggvolc

TrimGalore v0.6.7
https://github.com/FelixKrueger/TrimGalore
https://www.bioinformatics.babraham.ac.uk/index.html
doi.org/10.5281/zenodo.7598955

samtools v3.3.2
https://github.com/samtools/
https://www.htslib.org/
Li, H. et al. The Sequence Alignment/Map format and samtools. Bioinformatics. 2009; (25)2078.
doi:10.1093/bioinformatics/btp352

Salmon v0.12.0
https://github.com/COMBINE-lab/salmon
https://combine-lab.github.io/salmon/
Patro R. et al. Salmon provides fast and bias-aware quantification of transcript expression. Nature Methodss. 2021; (14)4.  doi.org/10.1038/nmeth.4197

DESeq2 v3.1.7
https://github.com/thelovelab/DESeq2
https://bioconductor.org/packages/release/bioc/html/DESeq2.html
Love MI. et al. Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2. 2014; (15)550.
doi:10.1186/s13059-014-0550-8

```
