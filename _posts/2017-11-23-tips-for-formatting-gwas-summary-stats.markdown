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

### Step 1 - Take A Look at the Header

The header of GWAS summary statistics data files tells you what information
of the GWAS is in the file. The following is just a list of headers that I have
come across.

```
snp effect_allele other_allele maf effect stderr pvalue

snpid hg18chr bp a1 a2 zscore pval CEUmaf

SNPID CHR POS A1 A2 Freq_HapMap Zscore Pvalue

Chromosome Position MarkerName Effect_allele Non_Effect_allele Beta SE Pvalue

Marker Chrom Pos Allele1 Allele2 Ncases Ncontrols GC.Pvalue Overall

SNPID CHR BP Allele1 Allele2 Freq1 Effect StdErr P.value TotalN
```
