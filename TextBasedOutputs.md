### Contents
[Main page](README.md) 

- [Text based outputs](#text-based-outputs)
    - [General comments](#general-comments)
        - [Viewing in Excel](#viewing-in-excel)
        - [ Using a reference set of genes](#using-a-reference-set-of-genes)
        - [Filtering by significance](#filtering-by-significance)
    - [List of all transcripts in the analysis along with the analysis values by DESeq2](#list-of-all-transcripts-in-the-analysis-along-with-the-analysis-values-by-deseq2)
    - [List of all differentially expressed  transcripts in the analysis along with the analysis values by DESeq2](#list-of-all-differentially-expressed--transcripts-in-the-analysis-along-with-the-analysis-values-by-deseq2)
    - [GO term inrichment](#go-term-enrichment)
    - [KEGG pathway enrichment](#kegg-pathway-enrichment)
    - [Reactome pathway enrichment](#reactome-pathway-enrichment)
    - [Multiple testing](#multiple-testing)
 

# Text based outputs
The main output from a RNA-seq analysis is a table that lists all the genes or transcripts in the analysis along with various metrics that identify statistically significant differentially expressed sequences, how large the change in expression was, whether it was up or down regulated and consistent the expression level was in each sample type.  
The analysis may also contain results of secondary analysis that identify what biological processes were up or down regulated due to the changes in transcription. These process are normally listed enrichment of Gene Ontology terms (GO terms), KEGG pathways and Reactome pathways.  
Example outputs from the RNA-seq analysis are shown below.

## General comments

The tables discussed below can be used as either a source of data to be imported into other programs, R packages or webpages to for further analysis or manually viewed in Excel or similar spread sheet application. 

#### Viewing in Excel
Special care should be used when opening these files in Excel as it may convert a value to some other data type, for instance a number of gene symbols may be converted to dates. Once changed they cannot be retrieved: always keep a second copy of your data in case some thing happens to the one you are working on.

#### Using a reference set of genes
 Some analysis compare a list of differentially expressed genes to a reference set of genes. This reference set may be all the genes in the genome (referred here as __"Universe"__) or all the genes in the analysis (referred here as __"Transcriptome"__)

#### Filtering by significance
Generally speaking, researches use these files by either ordering the data by padj and looking to see what is significant or by searching the data for a sequence(s) they are interested in. See the section on [multiple testing](#multiple-testing).

## List of all transcripts in the analysis along with the analysis values by DESeq2

The [TextBasedData.zip](data/TextBasedData.zip) in the _Data_ folder contains the _Counts_and_analysis_data.csv_ file. This file contains the results of the DESeq2 analysis to which the read counts for each sample as been added. The file's format is shown in Table 1 with the contents of each column explained in Table 2. 

__Table 1__: File containing results and read counts

||siCK4_1|siCK4_2|siCK4_3|siNT3_1|siNT3_2|siNT3_3|baseMean|log2FoldChange|lfcSE|stat|pvalue|padj|RefSeq|
|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|NM_001174166|1,050.10|641.93|968.25|80.46|139.69|103.59|497.34|3.04|0.25|-12.36|4.57E-35|3.64E-30|NM_001174166|
|NM_001363705.8|7.79|7.43|3.87|13.41|9.38|8.04|8.319|-0.67|0.61|1.10|0.27|NA|NM_001363705.8|

__Table 2__ Description of Table 1

|Header text|Description|
|-|-|
|Blank|Row name used by R, in this case its the transcript's GenBank accession ID|
|siCK4_1, siCK4_2, siCK4_3, siNT3_1, siNT3_2 and siNT3_3|The read count data for each of the samples|
|baseMean|The mean value of the normalised read counts used in the analysis. Since, DESeq2 doesn't export the normalised data, the mean value doesn't match the mean value of the sample read counts.|
|log2FoldChange|This shows the change in express between the two types of samples in the analysis. Rather than give the value of the change, the value is given as Log2 value of the expression. To convert the value to a decimal calculate 2 to the power of the value i.e., 2^3.04 = 8.23. In Excel the formula is __"=POWER(2,I2)"__ where I2 is the cell containing the value,|
|lfcSE|This is the log2FoldChange value divided by the standard error (SE) of the log2FoldChange. The standard error (SE) of the log2FoldChange is determined by DESeq2 and not exported by DESeq2.|
|stat|This is the Wald test value and is calculated as __"log2FoldChange / lfcSE"__
|pvalue|This is the p-value for the null hypothesis of __"The sequence not differentially expressed"__. This value should only be used if you intend to only look at one sequence from the analysis ans you'll ignore all other data for the other transcripts. (See below about multiple testing)|
|padj|This the probability that the sequence is not differently expressed when multiple testing is taken in to consideration. This the value that is generally used when viewing the data as a whole. (See below about multiple testing)|

## List of all differentially expressed  transcripts in the analysis along with the analysis values by DESeq2

An import omission from the data shown in Table 1 is the absence of the transcripts' gene symbol. This data has been added to the _sig_Deseq2_names.csv_ (also in the [TextBasedData.zip](data/TextBasedData.zip) file) from which the read count data and transcripts that are not statistically differentially expressed. Table 3 show a few lines from this file with Table 4 describing the fields that differ from the Table1.

__Table 3__: File containing results and gene symbols

| |RefSeq|baseMean|log2FoldChange|lfcSE|stat|pvalue|padj|SYMBOL|
|-|-|-|-|-|-|-|-|-|
|1522|NM_001174166|497.3|3.04|0.24|12.35|4.56e-35|3.63e-30|SLC16A6|
|5727|NM_004694|497.3|3.04|0.24|12.35|4.58e-35|3.63e-30|SLC16A6|
|4501|NM_001410944|189.3|3.23|0.27|11.78|4.45e-32|1.42e-27|KMO|
|4|NM_000075|256.543|-1.58|0.22|-6.91|4.82e-12|2.83e-09|CDK4|
|1624|NM_001197115.14|30.0|-1.09|0.36|-3.00|0.01|0.04|NA|

__Table 4__: Description of Table 3
|Header text|Description|
|-|-|
|Blank|Row name used by R, in this case its a number to gives the transcript's location in the original file|
|SYMBOL|The gene symbol when the GenBank accession ID can be mapped to a gene.| 

### How to use this data
Generally speaking, researches use these files by either ordering the data by padj and looking to see what is significant or by searching the data for a sequence(s) they are interested in. Before any serious work is performed, the read count data and DESeq2 analysis values should be viewed to make sure its believable. Special care should be given to look at the read count data and make sure the change in the expression is in the direction you think: its ease to get DESeq2 to compare the data the wrong with round. 

## GO term enrichment

GO or Gene Ontology terms are a set of short phrases that describe biological activities. A short description is give on this [page](GOTerms.md).

Once a list of differentially expressed sequences have been identified, they can be used to identify what GO terms have been linked to them. This list of GO terms can then be compared a list of GO terms linked all the genes in the test species' genome or all the genes present in the original read count file. By comparing the list of linked GO terms, those that are over or under represented in the list can be identified and then used to indicate what biological functions have been up or down regulated in the samples. This test is not performed by DESeq2, but by R packages such as ___GOSTAT___. 

The results of a a series of analysis is present in the [TextBasedData.zip](data/TextBasedData.zip). The files consist of those that compare the differentially expressed genes to all the genes in the human gene (filename contains __"Universe"__) and to all the genes sample transcriptome (filename contains __"transcriptome"__). The analysis also compare the terms present in the three GO term trees __"Cellular componet"__, __"Molecular function"__ and __"Biological process"__. The filenames contained the text __"CC"__, __"MF"__ and __"BP"__ respectively.

Table 5 contains a few lines from the __"BP_transcriptome_GO_all.xls"__ file with Table 6 describing each fields.

 _An interesting/irritating feature of tables exported by R is that they sometimes lack a header for the first data column in a file. Consequently, when you open these files in Excel you have shift the column titles to the right._

__Table 5__: GO term enrichment file

||GOBPID|Pvalue|OddsRatio|ExpCount|Count|Size|Term|
|-|-|-|-|-|-|-|-|
|1|GO:0098609|1.634e-07|2.256|34.505|65|244|cell-cell adhesion|
|2|GO:0009888|3.407e-07|1.656|100.572|148|722|tissue development|
|3|GO:0007156|3.484e-07|3.0155|15.952|37|112|homophilic cell adhesion via plasma membrane adhesion molecules|

__Table 6__: Description of Table 5

|Header text|Description|
|-|-|
|Blank|Row index|
|GOBPID|GO term ID|
|Pvalue| The p-value indicating if the term is enriched __Note__: This has been adjusted for multiple testing|
|OddsRatio|The odds ratio for the enrichment. Positive vales are enriched, negative terms are depleted.|
|ExpCount|The number of genes expected to be linked to the GO term.|
|Count|The number of genes observed to be linked to the GO term.|
|Size|Number of genes linked to the term in the reference data set.|
|Term|The GO term phrase|

### How to use this data

Like viewing the list of differentially expressed sequences, these files are typically viewed in Excel and either ordered by p-value and then the statistically significant terms are read or the phrases are scanned for those of interest. Some terms are so generic, such as __"cell-cell adhesion"__ that they offer very little insight and can be ignored. Similarly, some terms are so niche that only a few genes are linked to them, if one of these genes is differentially expressed the term will appear highly enriched, but really is ao little importance.

## KEGG pathway enrichment

Each KEGG pathway consist of a series of known gene networks that are involved in a specific process like __"Estrogen signaling"__ or __"Glutathione metabolism"__. As with the identification of GO terms that are enriched in the DEG list, differentially regulated KEGG pathways are identified by comparing the presence of gene in the pathway that are in reference set and or the list of DEGs. This reference set can be all genes in the genome or all expressed genes in the sample ([see this discussion](#using-a-reference-set-of-genes)).

__Table 7__: KEGG pathway enrichment file

|category|subcategory|ID|Description|GeneRatio|BgRatio|RichFactor|FoldEnrichment|zScore|pvalue|p.adjust|qvalue|geneID|Count|
|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|NA|NA|hsa04382|Cornified envelope formation|37/898|102/5537|0.36|2.24|5.55|5.64e-07|0.0001|0.00016|5317/3918/...|37|
|NA|NA|hsa04519|Cadherin signaling|69/898|267/5537|0.26|1.59|4.37|2.55e-05|0.004|0.003|5317/1952/...|69|
|Human Diseases|Cancer: overview|hsa05230|Central carbon metabolism in cancer|19/898|56/5537|0.34|2.09|3.61|0.0008|0.095|0.084|8503/110117499/...|19|
|Cellular Processes|Cell growth and death|hsa04218|Cellular senescence|36/898|136/5537|0.26|1.63|3.28|0.001|0.11|0.103|8503/110117499...|36|

__Table 8__: Description of Table 7

|Header text|Description|
|-|-|
|category|The broad description of the pathways class|
|subcategory|A more specific description of the pathways class|
|ID|The pathways ID|
|Description|Name of the KEGG pathway|
|GeneRatio|Number of DEGs linked to the pathway divided by the number of DEGs|
|BgRatio|The number of genes in the reference list linked to the pathway divided by the number of genes in the reference list|
|RichFactor|GeneRatio / BgRatio|
|FoldEnrichment|Value indicating how strong the enrichment is. Positive vales are enriched, negative terms are depleted.|
|zScore|A directional enrichment score. Positive vales are enriched, negative terms are depleted.|
|pvalue|The raw p‑value from Fisher’s exact test |
|p.adjust|The adjusted p-value calculated with Benjamini–Hochberg FDR method|
|qvalue|The Storey q‑value (False Discovery Rate)|
|geneID|List of ensembl gene ids (limited to 2 in this table)|
|Count|The number of DEGs that are linked to the pathway|

### How to use this data

As with the list of enriched GO terms, this data may be ordered by p.adjust to see the statistically significantly enriched terms or scanned for text of interest.


## Reactome pathway enrichment

Like the KEGG pathways, Reactome pathways link genes involve in a specific process, but like the GO terms the Reactome pathways form a hierarchical structure. Consequently, some pathways are very generic while others or very specific to a pathway. Reactome pathway enrichment is performed by comparing a list of DEGs to a reference set of genes ([see here](#using-a-reference-set-of-genes)). The R package ReactomePA can export the enrichment as a text file as shown in Table 9 and described in table 10. Unlike the GO term and KEGG pathway enrichment you do not supply a list of reference gene; however, you do indicate what species the data is from.

__Table 9__: Reactome pathway enrichment file

||ID|Description|GeneRatio|BgRatio|RichFactor|FoldEnrichment|zScore|pvalue|p.adjust|qvalue|geneID|Count|
|-|-|-|-|-|-|-|-|-|-|-|-|-|
R-HSA-72766|R-HSA-72766|Translation|363/7482|368/11230|0.986|1.48|13.24|1.287e-57|2.17e-54|1.05e-54|EIF2B3/DAP3/...|363|
R-HSA-72203|R-HSA-72203|Processing of Capped Intron-Containing Pre-mRNA|288/7482|294/11230|0.979|1.47|11.54|3.50e-43|2.95e-40|1.42e-40|HNRNPR/RNPC3/...|288|
R-HSA-68886|R-HSA-68886|M Phase|380/7482|405/11230|0.938|1.40|11.82|5.10e-41|2.87e-38|1.38e-38|PMF1-BGLAP/PMF1/...|380|

__Table 10__: Description of Table 9

|Header text|Description|
|-|-|
|Blank|ID used by R to identify each row|
|ID| Reactome pathway identifier|
|Description|Name of the Reactome pathway|
|GeneRatio|Number of DEGs linked to the pathway divided by the number of DEGs|
|BgRatio|The number of genes in linked to the pathway divided by the number of genes in the reference list|
|RichFactor|GeneRatio / BgRatio|
|FoldEnrichment|Value indicating how strong the enrichment is. Positive vales are enriched, negative terms are depleted.|
|zScore|A directional enrichment score. Positive vales are enriched, negative terms are depleted.|
|pvalue|p‑value indicating significance of its enrichment|
p.adjust|The adjusted p-value calculated with Benjamini–Hochberg FDR method|
|qvalue|The Storey q‑value (False Discovery Rate)|
|geneID|Gene symbols of DEGs linked to the pathways (limited to two for this table).|
|Count|The number of DEGs that are linked to the pathway|

### How to use this data

As with the list of enriched GO terms and KEGG pathways, this data may be ordered by p.adjust to see the statistically significantly enriched terms or scanned using text of interest.

## Multiple testing

When screening the results of a differential expression analysis whether is the list of transcripts, GO terms or pathways, you should use the p-value adjusted for multiple testing. However, if you are only interested in one sequence you can look at the unadjusted p-value, but only if you intend to ignore all the other data. This is because, the p-value of 0.05 is used to answer the question: Could the distribution of reads counts occur by chance once in twenty randomly generated datasets. If the p-value is 0.01, then the data would be seen by chance in 1 in a hundred random data sets and so passes the 0.05 cutoff. However, the _Counts_and_analysis_data.csv_ contains the results of 309,009 tests so if you test for hits that could be seen one in twenty tests, that means you would expect to see about 15,540 false positives (309,009 * 1/20). Consequently, you have to adjust your p-value to take into account all the multiple testing. DESeq2 uses the Benjamini–Hochberg FDR correction to adjust the p-value. If a sequence doesn't appear to be statistically significant after multiple testing the padj value is set to NA. 

This raises an important issue when testing all the transcripts in a genome, the more you look at the more large (and consistent) the affect has to be. So if you include all the lncRNAs and all alternatively spliced transcripts in an analysis the level of differential expression has to be stronger than if you just included the conical protein coding transcripts in the analysis. Similarly, if you are only interested in proteins that form a complex, then you need to adjust the p-value yourself based on the number of proteins of interest. All the other data has to be ignored, however since DESEq2 uses the expression profiles of all the transcripts to create its analysis model, its best to analyse all the data and then manually adjust the p-value rather than remove all the unwanted sequences and then analysing only the genes of interest with DESeq2.