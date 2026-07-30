### Contents
[Main page](README.md) 

- [Analysis validation](#analysis-validation)
    - [Mean expression versus log2[fold change]](#mean-expression-versus-log2fold-change)
    - [Expression mean versus transcript variance](#expression-mean-versus-transcript-variance)
    - [PCook's distance](#cooks-distance---samples-with-unusual-transcript-levels)
    - [Dispersion plots](#dispersion-plots)
    - [Independent filtering of results](#independent-filtering-of-results)
    - [Rank of Wald statistic](#rank-of-wald-statistic)
    - [Histogram of p-values that passed or failed filter at each cutoff value](#histogram-of-p-values-that-passed-or-failed-filter-at-each-cutoff-value)
    - [–log10(p‑value) vs mean normalised counts](#log10pvalue-vs-mean-normalised-counts)

---

# Analysis validation

As well as producing data intended to instigate further work, a good analysis pipeline will also generate images that allow you to check the integrity of the analysis. The following sections show some images a standard DESeq2 analysis may produce and briefly explain what they mean. For more information, read the DESeq2 [vignette](https://www.bioconductor.org/packages/release/bioc/vignettes/DESeq2/inst/doc/DESeq2.html).


## Mean expression versus log2[fold change]

Figure 1 shows a graph of how a transcript's expression changes with respect to its expression level in individual samples. The blue points represent differentially expressed transcripts. Typically, low-count transcripts show more variability, which can inflate fold changes, as it's easier to go from 10 counts to 20 by random sampling variation than it is to go from 1 million to 2 million. Therefore, large changes in lowly expressed transcripts are more likely not to be statistically significant.

![Figure 1](images/Expression_vs_FoldChange.png)

Figure 1: Expression levels versus Log2[fold change]. The STD title indicates the data has been normalised by the default (standard) DESeq2 function.

## Mean expression versus transcript variance

After normalisation of the data, the standard deviation for the transcripts read count is consistent across the range of mean read counts. These graphs show the effect of this normalisation, with the outlying data points hopefully representing differentially expressed transcripts. If the graph shows a red line significantly different from the one in Figure 2 or there is a substantial number of outliers, it suggests there are issues with the imported read count data.

![Figure 2](images/Expression_vs_Variance.png)

Figure 2: Graph of mean expression versus transcript variance.

## Cook's distance - samples with unusual transcript levels

When viewing a very large number of transcripts some will have an unusual expression profile compared to the other samples. This is not an issue unless a large number of transcripts display unexpected expression levels in one or a few samples. DESeq2 calculates the Cook's distance for each sample's transcripts and displays the results as a series of box plots. If one sample appears to be noticeably different from the other, it may be reasonable to remove it from a subsequent analysis.

![Figure 3](images/cooksdistances.png)

Figure 3: Series of box plots showing distribution of each sample's Cook's distances

## Dispersion plots

RNA-seq data is very noisy, and the analysis has to reduce the level of noise so the final statistical analysis will work. To show how the lowering the dispersion (noise) for each gene's expression has been reduced, a dispersion plot is produced showing the original dispersion value for each gene (black dots in Figure 4) and the shrunken dispersion values (blue dots in Figure 4) plotted against the gene's mean expression level. It is expected that the blue points lay closer to the line of red data points than the black data points and that there are only a few outliers scattered about the graph.

![Figure 4](images/DisperionPlot.png)

Figure 4: A dispersion plot. The data points on the x-axis represent genes with very little variation in expression.

## Independent filtering of results

Since transcripts with very low expression levels are unlikely to become significantly differentially expressed due to the adverse effects of random noise, DESeq2 removes them from the analysis. This is done to stop them from perturbing the analysis. To do this, transcripts are ordered by their mean normalised count and then binned in to quantiles, with each division representing 1% of the transcripts. The threshold is then moved from the first quantile to the last, calculating the number of transcripts above the cutoff that have significant adjusted p‑values. The threshold with  maximises the number of significant adjusted p‑values is then used to score the transcripts. This filtering step is shown in the independent filtering graph (Figure 5). Ideally, the cutoff is placed near the curve's peak and the curve is smooth.

![Figure 5](images/readCountThresholdGraph.png)

Figure 5: Lowly expressed transcripts are sequentially removed, and the number of significant adjusted p‑values is checked to find the best cutoff (vertical line).

## Rank of Wald statistic

The Wald value is created by dividing a transcript's estimated Log2 [fold change] its standard error. Large values indicate stronger evidence for differential expression. This value is then graphed with respect to the transcript's Cook's distance. Transcripts should appear evenly spread along the x-axis with low Cook's distance values.
![figure 6](images/RankWaldStat.png)

Figure 6: Graph of the Wald value (x-axis) against the Cook's distance (y-axis).

## Histogram of p-values that passed or failed filter at each cutoff value

To visualise the effect of the filtering threshold, the graph in Figure 7 shows the number of transcripts included and excluded for each bin of the mean of normalised count values. The histogram is tallest at x = 0, as most genes are either poorly expressed or not expressed at all, and so the bin with 1% of reads is linked to the most transcripts and as they have the lowest read counts, they tend to not be statistically significant.

Ideally, the majority of filtered (removed) transcripts are at the left of the graph (low read counts) and the majority of all transcripts passed the test (blue histogram). __Note:__ the base of each _pass_ (blue) column is the y = 0 point and not the top of the _do not pass_ (tan) column.

![Figure 7](images/pvaluesVsReadCountbin.png)

Figure 7: Graph of tests that were either filtered (_do not pass_) or retained (_pass_) for each read count bin. 

## –log10(p‑value) vs mean normalised counts

This graph shows how the significance of a gene's differential expression varies as a function of its expression level. You would expect to see the following:
- A dense cloud of low‑count genes with low –log10(p‑value), which are transcripts unaffected by the treatment.
- A spread of higher‑count genes with larger –log10(p‑value) which are differentially expressed transcripts.

Ideally, the two groups of transcripts overlap with no clear boundary effect.

![Figure 8](images/pvalue_vs_readCounts.png)

Figure 8: Graph plotting each transcript's p-value (-log10[p-value]) against its expression level (mean normalised counts).

