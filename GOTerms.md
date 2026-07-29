# Gene ontology terms

Gene ontologies are an evolving set of phrases used to define proteins with respect to their biological process, molecular function or cellular compartment. The phrases or gene ontology terms (GO terms) are ordered in a hierarchical manner similar to a tree and are currently annotated by the [Gene Ontology Consortium](http://geneontology.org/). 

> Ashburner et al. Gene ontology: tool for the unification of biology. Nat Genet. 2000 May;25(1):25-9. DOI: 10.1038/75556
> 
> The Gene Ontology Consortium. The Gene Ontology knowledgebase in 2023. Genetics. 2023 May 4;224(1):iyad031. DOI: 10.1093/genetics/iyad031

The base of the tree consists of terms with vaguer, generic meanings such as ‘Growth’ or ‘Immune system process’ each of which catches a wide range of processes. These terms are then linked to more specific child terms such as 

‘Growth’ > ‘Cell growth’ 

or  

‘Growth’ > ‘Developmental growth’,

with ‘Growth’ being a parent term to its child term ‘Cell growth’. These in turn are linked to even more specific terms such as 

‘Growth’ > ‘Developmental growth’ > ‘Developmental cell growth’ 

and 

‘Growth’ > ‘Developmental growth’ > ‘Developmental growth involved in morphogenesis’.

While in principle the arrangement is simple, in practice it can become complex as a term may have more than one parent term. For instance ‘Developmental cell growth’ is linked to both ‘Developmental growth’ and ‘Cell growth’

‘Growth’ > ‘Developmental growth’ > ‘Developmental cell growth’

and 

‘Growth’ > ‘Cell growth’ > ‘Developmental cell growth’

Proteins are linked to GO terms either through direct experimental investigation or by sequence or structural homology to a protein that has been previously linked to a term. Consequently, while it may seem logical that a protein linked to a term will also be linked to that terms parent term(s), this is not explicitly stated. 

While the current usage of GO terms has its limitations, they can still be very useful when describing biological phenomena such as attempting to determine a cells physiological response to stimuli or genetic mutation. The analysis of gene expression microarrays and NGS RNAseq is routinely preformed to identify changes in gene expression profiles between various cohorts of biological material. However, simple lists of differentially expressed genes can often be too large to be easily used to describe any changes in sample physiology. To resolve this a number of applications have been developed that link differentially expressed genes (DEG) to their GO terms and then determine if a GO term is linked to more or less genes in the dataset than expected, when compared to how common that term is in a reference gene set such as all the genes expressed in a sample or those present in the organism’s genome. One such application is the R package s which has been cited over 2000 times since its publication in 2007:

> Falcon S, Gentleman R (2007). “Using s to test gene lists for GO term association.” Bioinformatics, 23(2), 257-8.

This R package compares two lists of genes and determines if a GO term is under or over represented in one list when compared to the other reference list. GO terms linked to genes in the DEG list that are significantly over-or under-enriched can then be exported along with their level of significance as measured by their p value and odds ratio value along with the number of genes linked to the term and the expected number of genes for a comparably sized random list of genes.

[Back to the description of text data](TextBasedOutputs.md/#go-term-enrichment)
