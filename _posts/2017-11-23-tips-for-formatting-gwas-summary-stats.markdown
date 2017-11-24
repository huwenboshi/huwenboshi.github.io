---
layout: post
title:  "Tips for Formatting GWAS Summary Association Statistics Data"
date:   2017-11-23
category: data management
tags: [summary statics]
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
This page aims to provide some tips, guidelines, and protocols that I find
useful for formatting a lot of GWAS summary statistics data to help prevent
pitfalls in post-GWAS analyses.

### Step 0 - Rename, Date, and Record the Publication of the Data

GWAS summary stats data files often come with file names that are also all
over the place. Before looking into the details of the data, we recommend
to come up with an abbreviation for the phenotype, and rename the files in
a consistent fashion. This will make your life a lot easier in the long run.
For example, for the 2014 schizophrenia GWAS summary stats data, the file
name could be ```SCZ_2014.txt```, and for the 2014 rheumatoid arthritis
GWASs in multiple populations, one could rename the files as
```RA_ASN_2014.txt```, ```RA_EURO_2014.txt```, and ```RA_TE_2014.txt```,
where TE stands for transethnic. With each GWAS summary stats data, we also
recommend to include a readme document to record the publication of the GWAS
summary data, and the URL the data was downloaded from. And the file names of
the readme document could be something like ```SCZ_2014.readme```. Lastly,
we recommend to store all the readme files and freshly downloaded summary
stats files in a folder called ```0_Raw```.

### Step 1 - Take A Look at the Header and Figure Out What's Missing

The header of GWAS summary statistics data files tells what type of
information of the GWAS is available and unavailable in the file. The
following is a list of some typical headers. If the information that
one need for their analyses is not in the header (e.g. sample size, number
of cases and controls, etc.), then one will have to read the GWAS paper
to extract these information.

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

#### Note on Genome Build
Many freshly downloaded GWAS summary stats also only contain SNP ID and
not chromosome number or base pair positions. In some cases, some old GWASs
before 2012 use HG18 (NCBI B36) for base pair positions. For these type of
data, one has to match the SNP IDs against the reference panel legend to
find out the chromosome number and base pair positions.

#### Note on Sample Size
Note that some GWASs report the total sample size, which includes samples both
in the discovery stage, and samples in the replication stage. However,
it's often the case that sample size of the discovery GWAS stage is the
one that matches the data.

### Step 2 - Create Your Own Headers and Compute the Relevant Information

Most GWAS summary stats data do not come with all the information one needs.
For example, it's very often the case that GWAS summary stats file do not
contain Z-scores, but rather effect size (odds ratio for case-control traits)
and its standard error, and some GWASs provide p-values and effect size. Since
Z-score information is used in many summary-data-based software such as LDSC
and HESS, it's highly recommended to include Z-score information in the
formatted summary stats file. In general, it's highly convenient to always
have the following 7 columns in the formatted summary stats file.

```
SNP : SNP ID (it's recommended to only include SNPs with rs IDs in the data,
as these SNPs are often more well-characterized)

CHR : Chromosome number (some GWAS summary data contain SNPs on chromosome X,
Y, and MT, but usually these SNPs are filtered out during QC)

BP : Base pair positions (make sure all formatted summary stats use the same
genome build)

A1 : Effect allele (also sometimes called risk allele, reference allele,
effect allele, coded allele, etc.)

A2 : Non-effect allele (also some times called alternate allele, the other
allele etc.)

Z : Z-score with respect to the effect allele, i.e. if Z-score is positive
then the effect allele increases the phenotype

N - Sample size (this is often the discovery stage sample size, not maximum
sample size)
```

#### Note on Computing Z-scores

If effect size and standard error are included in the freshly downloaded GWAS
summary stats file, then Z-score can be computed as
\\[
  Z = {\text{Effect Size} \over {S.E.}}
\\]

If odds ratio and standard error are include, then Z-score can be computed as
\\[
  Z = {\log (\text{Odds Ratio}) \over {S.E.}}
\\]

If p-value and effect size (odds ratio) are available then Z-score can be
computed as
\\[
  Z = \text{sign(Effect Size)} \times |\Psi^{-1}(p / 2)|
\\]
or
\\[
  Z = \text{sign(log Odds Ratio)} \times |\Psi^{-1}(p / 2)|
\\],
where \\(\Psi^{-1}\\) is the inverse cumulative distribution function of the
normal distribution.
