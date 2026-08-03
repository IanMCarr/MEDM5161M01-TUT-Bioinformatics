### Contents
[Main page](README.md) 

- [Description of data](#description-of-data)
    - [Gene count plots](#gene-count-plots)
    - [Graphics based data](#graphics-based-data)
    - [KEGG pathway maps](#kegg-pathway-maps)
    - [Text based data](#text-based-data)
    
  ---


# Description of data

The data folder contains four zip files, each containing a series of data files as described below.

## Gene count plots

The genecounts.zip contains over 9,000 PNG image files, each showing the expression level of a specific transcript in all the 6 samples. Each image's file name consists of its gene symbol (if known) and its GeneBank accession ID. Consequently, the data should be extracted from the ZIP file and transcripts of interest found by searching for the transcript's gene symbol or accession ID.

These graphs are explained [here](GraphicalOutputs.md/#gene-expression-plots). 

## Graphics based data

The GraphicsBasedData.zip file contains a copy of the images referenced in this repository. 

These graphics are explained on this [page](GraphicalOutputs.md). 

## KEGG pathway maps

The Kegg_Pathway_DeSeq2.zip file contains over 320 annotated KEGG pathway maps. Some of the KEGG pathway maps are not relevant to this work as they relate to no human/mammal pathways or are not affected by CDK4 levels. Like the gene count graph file names, you can select pathways by searching the filenames for key words. 

These graphics are explained on this [page](GraphicalOutputs.md/#kegg-pathway-maps). 

## Text based data

The TextBasedData.zip file contains text-based data that lists differentially expressed transcripts, enriched GO terms and Reactome and KEGG pathways. 

These text files are described [here](TextBasedOutputs.md).