
# Data exported as part of a DESeq2 analysis

When RNA-seq data is analysed with DESeq2, a range of data is exported. Some data is generated  by DESeq2 itself, while other data is produced by other software packages using the data exported by DESeq2. This data falls into three main sets:
- Text-based data: Tables of differentially expressed sequences, GO term enrichment or pathway enrichment
- Graphics summarising the analysis: Graphs showing transcript read count, heatmaps and volcano plots    
- Graphics visualising quality control data based on DESeq2 generated data.



## Important points: 
- When talking about the results of an RNA-seq analysis, the term 'DEG' (differentially expressed genes) is routinely used; however, many analyses are performed using transcript annotations  rather than gene annotations. Consequently, the output is a list of differentially expressed transcripts. This means a specific gene may occur multiple times in a data set. once for each of its transcripts. 
- Also, since alternatively spliced transcripts from the same gene share exons, if one alternatively spliced transcript is differentially expressed, other transcripts may be identified as differentially expressed even if they are not expressed. This is because reads from the differentially expressed transcript also align to shared exons in other transcripts from the same gene.


## The following pages describe these three types of outputs.
 - [Graphical outputs](GraphicalOutputs.md)
 - [Text based data](TextBasedOutputs.md)
 - [Quality control data](QualityControlImages.md)