# Comparison of RNA expression in Fetal and Adult Brain Tissue
## Capstone project for the Coursera Genomic Data Science Specialization

Publically available RNASeq data obtained from BioProject PRJNA245228 and analyzed in Galaxy (alignment step) and RStudio


## This analysis is split into 6 main parts:

**1)	Import of raw fastq data into Galaxy from SRA**

**2)	Alignment of fastq files in Galaxy using STAR**

**3)	Count matrix generation using featureCounts in Galaxy**

**4)	Exploratory analysis of counts using PCA**

**5)	Differential expression between Fetal and Adult Brain**

**6)	Comparison of DEGs to H3K4me3 methylation near promoters**




**The first 3 steps were performed using Galaxy. Briefly:**

1. Fastqs imported into Galaxy using the “EBI SRA” tool in Galaxy. Paired-end fastqs were imported for 6 runs (corresponding to 3 Fetal and 3 Adult samples) from experiment SRX683795: SRS686965 / SRS686966 / SRS686969 / SRS686967 / SRS686962 / SRS686964

2. Fastqs aligned in Galaxy using STAR. Paired fastqs were aligned in Galaxy using RNA STAR Gapped-read mapper for RNA-seq data (Galaxy Version 2.6.0b-1). The built-in index for Human (Homo sapiens) (b37): hg19 was used as the reference genome. Length of the genomic sequence around annotated junctions was set at 99. Defaults were used for all other settings. Mapped.bam files were QC’d using FastQC Read Quality reports (Galaxy Version 0.72+galaxy1). No additional filtering or trimming was performed post-QC. 

3. Mapped.bam files were quantified in Galaxy using featureCounts (Galaxy Version 1.6.4+galaxy1). Strand information was set as Unstranded. The built in hg19 genome was used for quantifying read counts. Output format was set as Gene-ID “\t” read-count (MultiQC/DESeq2/edger/limma-voom compatible). Gene-length file was not created. Job resource parameters were left at defaults. The tabular counts matrix for each sample (6 total) was used as input into RStudio for steps 4-6


**Steps 4-6 were performed in R. The code used for performing this analysis is included in this repository.**


4. Exploratory analysis: PCA plotted for several phenotype characteristics, including average Q30, age, sex, and race to determine if any batch effects need to be controlled for in DE.

5. Differential expression: DESeq2 used for DE analysis. Hierarchical clustering and heatmap plottin performed using pheatmap. 

6. Comparison of DEGs to H3K4me3 methylation near promoters. Here, the genes that were found to be significantly DE between three Fetal and three Adult samples are compared to genes that have H3K4me3 modification near their promoters, in Adult and Fetal Brain samples. H3K4me3 is a histone methylation modification that causes an increase in expression of nearby genes. As a control, genes found signifcantly increased in Adult Brain are compared to H3K4me3 modification in Liver samples. Overall: of the 8,451 genes with their promoter near H3K4me3 only in Adult brain tissues, 1,995 (23%) were also significantly increased in Adult brain samples in differential expression. Of the 15 genes with their promoter near H3K4me3 only in Fetal brain, 3 (20%) were also significantly increased in Fetal brain samples during differential expression.
