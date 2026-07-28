
# Data exported as part of a DESeq2 analysis

When RNA-seq data is analysed with DESeq2 a range of data is exported. Some data is generated  by DESeq2 itself, while other data is produced by other software packages using the data exported by DESeq2. This data falls in in to three main sets:
- Text based data:
    - Directly fromm: DESeq2 - tables of the differentially expressed transcripts
    - Created by other packages using DESeq2 data - tables of GO term enrichments or KEGG pathway enrichment
- Graphics summarising the analysis
    - Directly from DESeq2: transcript read count graphs
    - Created by other packages using DESeq2 data - annotated KEGG pathway maps
- Quality control data based on DESeq2 generated data.

While the list distinguishes between data exported by DESeq2 and data exported by other packages using DESeq2 data, the division is very lose main of DESeq2 graphics created using image drawing packages like ggplot2. The division used here is the data modify the other package or just annotated by it. 

The following pages describe these three sets of data.
 - [Graphical outputs](GraphicalOutputs.md)
 - [Text based data]()
 - [Quality control data](QualityControlImages.md)