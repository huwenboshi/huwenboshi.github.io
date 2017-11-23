---
layout: post
title:  "Tips for Formatting GWAS Summary Association Statistics Data"
date:   2017-11-23
category: data management
tags: [mixed model]
---

<script type="text/javascript" async
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

### Summary

Publicly available GWAS summary association statistics data are in all kinds
of formats. The diversity of data formats is often attributable to the nature
of the phenotypes being studied (e.g. case-control trait / quantitative traits)
and the software used to perform the analysis. However, before anly post-GWAS
analyses, one needs to convert data in various formats into the same format.
This page aims to provide some tips, guidelines, and protocols for formatting
GWAS summary statistics data to help prevent pitfalls in post-GWAS analyses.

### Step 0 - Rename, Date, and Record the Publication of the Data

GWAS summary stats data files often come with file names that are also all
over the place. Before looking into the details of the data, we recommend
to come up with an abbreviation for the phenotype, and rename the files in
a consistent fashion. For example, for the 2014 schizophrenia GWAS summary
stats data, the file name could be ```SCZ_2014.txt```, and for the 2014
rheumatoid arthritis GWASs in multiple populations, one could rename the
files as ```RA_ASN_2014.txt```, ```RA_EURO_2014.txt```, and
```RA_TE_2014.txt```, where TE stands for transethnic.

### Step 1 - Take A Look at the Header

The header of GWAS summary statistics data files tells one what type of
information of the GWAS is available and unavailable in the file. For example,
if a GWAS summary stats file does not contain sample size information, then
one needs to read through the corresponding publication

The following is a list of some typical headers.

```
snp effect_allele other_allele maf effect stderr pvalue
snpid hg18chr bp a1 a2 zscore pval CEUmaf
SNPID CHR POS A1 A2 Freq_HapMap Zscore Pvalue
Chromosome Position MarkerName Effect_allele Non_Effect_allele Beta SE Pvalue
Marker Chrom Pos Allele1 Allele2 Ncases Ncontrols GC.Pvalue Overall
SNPID CHR BP Allele1 Allele2 Freq1 Effect StdErr P.value TotalN
SNP CHR BP A1 A2 OR SE P INFO EUR_FRQ
rsID,allele1,allele2,freqA1,beta,se,pval,N
Marker Chr Position PValue OR(MinAllele) LowerOR UpperOR Alleles(Maj>Min)
Chr Position Allele1 Allele2 Freq1 Pvalue EffN
```
