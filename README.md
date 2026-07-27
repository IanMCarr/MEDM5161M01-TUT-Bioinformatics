
# Graphical output

## Volcano plots

Volcano plots are used to visualise the results of differential gene expression analysis. The fold change in transcript expression between the two sample conditions is shown on the x-axis. While statistical significance is shown on the y-axis. Both values are visualised as the log of the value, so the graph's scale is more informative. Similarly, the "-" value of the log(p-value) is shown so that significant transcripts are at the top of the graph.

Transcripts with large changes in their expression occur on the left and right of the graph, while those with a statistically significant change appear at the top of the graph.

When used with a large number of data points, they enable the viewer to understand the general trends of an analysis. If used with fewer data points, they may allow individual transcripts to be visualised.

![Figure 1](images/volcanoplots2.png)

Figure 1: See Table 1 for description

__Table 1__

|Colour|Description|
|-|-|
|Grey|Transcripts with small changes in expression that are not statistical significant|
|Green|Transcripts with larger changes in expression that are not statistical significant|
|Blue|Transcripts with small changes in expression that are statistical significant|
|Red|Transcripts with large changes in expression that are are statistical significant|


## Heat maps

Heatmaps provide a simple way to visualise the differences between different samples. The display can consist of the comparison of single value in each sample ([see here](#heatmaps-comparing-the-samples-to-each-other)) or an array of values for each sample ([see here](#heatmaps-of-expression-level-changes-of-transcripts)).

- ## Heatmaps of expression level changes of transcripts

Heatmaps are often used to display the clustering of differentially expressed transcripts or genes in the samples. The gene's/transcripts colour is determined by its expression level.
The clustering is performed by comparing each transcript's expression level in each sample to the other transcripts and then placing transcripts with similar expression profiles closer to each other. The clustering of the samples is preformed by comparing the transcript expression profiles of each sample to the other samples and placing samples most similar samples closer to each other. The clustering may be shown as a dendrogram.

In Figure 2a, the colouring of the transcripts is determined by the transcripts expression level in a sample relative to its expression level in the other samples. However, in Figure 2b, the colour of a transcript is dictated by its expression level in a sample relative to the expression level of all the transcripts in that sample.

__Note__: the data in Figures 2a and 2b is the same, but the way the expression levels are compared for each heatmap is different.

![Figure 2a](images/DEGHeatmap_1.png)

![Figure 2b](images/DEGHeatmap_3.png)

Figure 2: Heatmaps showing the expression profiles in the modified samples (siCK 1 to 3) and the control samples (siNT 1 to 3). The dendrograms on the left show how the transcripts cluster, while the dendrogram across the top show how the samples cluster.

- ## Heatmaps comparing the samples to each other

Heatmaps can be used to compare the samples in the analysis so that its possible to determine which samples are more alike. In Figure 3, the expression values of the transcripts in each sample are used to make a distance score between each pair of samples. These values are then used to create the heatmap where the darker the blue is the more alike the pair of samples are. The diagonal line of squares represents the results of comparing each sample to itself. 

![Figure 3](images/heatmapSamples_3.png)

Figure 3: Heatmap showing how alike the sample's expression profiles are to each other. The order of the rows is the same as the order of the columns. Each label is comprised of the samples _condition_ (control or siCk) and the samples name.

## PCA plots

A PCA plot shows how samples relate to one another by reducing transcript expression measurements into just a few values called principal components. These capture the major sources of variation in the dataset. Each point on a PCA plot represents a sample, and the distance between points reflects how similar or different their overall expression profiles are. The x-axis is the value of the first principal component (PCA1) while the y-axis shows the value of the second principal component (PCA2). 

![Figure 4](images/PCAPlots_1.png)

Figure 4: In this PCA plot the samples are individually colour codes with their  sample type (control or siCK) and sample name shown in the Group key.

## ReactomePA graphs

Reactome is a manually curated, peer‑reviewed database of biological pathways that are know to occur in cells. There are lists of genes linked by a biological activity, such as __rRNA processing__, __Organelle biogenesis and maintenance__ and __Chromatin modifying enzymes__. Each pathway will contain multiple genes and a gene may be linked to more than one pathway.

ReactomePA, identifies which genes in a pathway are differentially expressed and whether the number of genes linked to a pathway is statistically significant. The results of the analysis can then be exported as graphs showing the pathways whose expression/activity varies the most between the different types of sample.

![Figure 5](images/ReactomePA_2.png)

Figure 5: A ReactomePA graphic in which the top 25 pathways are shown. Table 2 describes the graph's scaling.

|Feature|Description|
|-|-|
|Colour of data point|The colour of each data point indicates its statistical significance|
|Size of data point|Number of DEGs linked to pathway|
|Data point's x-axis value|The ration of DEGS in pathway to number of all genes in the pathway|

## KEGG pathways

KEGG pathways are another set manually curated, peer‑reviewed database of biological pathways that are know to occur in cells. Like the Reactome pathways, each pathway describes a specific function such as __Central carbon metabolism in cancer__, __Cytokine-cytokine receptor interaction__ and 
__Virion - Hepatitis viruses__. Each pathway will contain multiple genes and a gene may be linked to more than one pathway.

The KEGG organisation has created a graphic for each pathway showing how different items in the pathway interact. It is possible to colour code genes in the a pathway's graphic based on its change in expression allowing the visualisation of a pathways activation or deactivation based on the differences between the two types of samples.

![Figure 6](images/hsa04218.siCK4_v_control__0.01_Cellular_senescence.png)

Figure 6: The KEGG pathway map of the __Cellular senescence__ pathway with genes with increased expression shown in red and those with reduced expression shown in green.

## 
