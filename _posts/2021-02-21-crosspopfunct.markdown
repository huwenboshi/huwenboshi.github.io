---
layout: post
title:  "Population-specific Disease Effect Sizes and Where to Find Them"
date:   2021-02-21
category: genetics
tags: [cross-population]
---

<script type="text/javascript" async
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

A few days ago, we published a [paper](https://www.nature.com/articles/s41467-021-21286-1)
on Nature Communications that looks at the genetics of human diseases (e.g. type 2 diabetes, rheumatoid arthritis)
and complex traits (e.g. height, body mass index) across populations. In this
blog post, I hope to give a simple and intuitive understanding of our work to a broad audience.

### What did we study?

We studied the effects of genetic variants have on diseases
and traits across different populations (East Asians and Europeans, in particular).
In summary, we wanted to answer the following questions.

1. How similar/dissimilar are genetic effects across different populations,
across the entire human genome?

2. For which components of the human genome are genetic effects more similar/dissimilar
across populations, compared to the rest of the genome?

The metric we used to assess similarity/dissimilarity in genetic effects
across populations is called trans-ethnic genetic correlation,
which,as the name suggests, measures the correlation of genetic
effects in different populations.

We developed a [statistical tool](https://github.com/huwenboshi/s-ldxr) to
quantify trans-ethnic genetic correlation for the entire genome, and for
specific components of the human genome, such gene regions, and regions
that regulates expression of genes, etc.

### Why do we care?

First, some background. Genetic studies have been rare
for non-European populations. In fact, non-European populations only make up
20% of genetic studies, which is very small, considering about 90% of the world
populations are non-Europeans. Because genetic study in non-Europeans is so limited,
it makes the most practical sense to transfer what we can learn fron
Europeans to non-Europeans. But the transferrability seems limited. For example,
in genetic risk prediction using genetic effects learned from Europeans, the
relative prediction accuracy for non-Europeans can
be 50% to 80% lower compared to that for Europeans (see this [paper](https://www.nature.com/articles/s41588-019-0379-x?WT.ec_id=NG-201904&sap-outbound-id=2C9E78DECC81D5016FE335EAE68FF5C714553CD4)).

This limited cross-population transferrability is often attributed to differences in frequencies
and correlation patterns of genetic variants in different populations. But
we are curious if the limited transferrability can be also driven by
specific differences in the underlying genetic effects in important part
of the human genome (e.g. around genes). Investigating if this is indeed the
case can provide additional understanding of the sources of limited
cross-population transferrability, and may guide genetic researchers on how
to perform future genetic studies.

### What did we find?

We analyzed the studies of 31 diseases and complex traits from UK Biobank (Europeans)
and Biobank Japan (East Asians). Averaging across the traits, we found that
the cross-population genetic correlation across East Asians and Europeans was
about 0.85, although for some traits this quantity was much lower (e.g. ~0.3
for major depressive disorer). This results suggest that genetic effects
in different populations are, overall, similar to each other. But, they are
not *exactly* the same, suggesting genetic effects are dissimilar, in
other words, population-specific, for some parts of the genome.

### What are the implications?
