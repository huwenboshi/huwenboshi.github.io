---
layout: post
title:  "Population-specific Genetic Effects and Where to Find Them"
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
across the entire genome?

2. For which components of the human genome are genetic effects more similar/dissimilar
across populations, compared to the rest of the genome?

The metric we used to assess similarity/dissimilarity in genetic effects
across populations is called cross-population genetic correlation,
which, as the name suggests, measures the correlation of genetic
effects in different populations. We developed a [statistical tool](https://github.com/huwenboshi/s-ldxr) to
quantify cross-population genetic correlation for the entire genome, and for
specific components of the human genome, such as gene regions, and regions
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

We analyzed genetic studies of 31 diseases and complex traits from UK Biobank (Europeans)
and Biobank Japan (East Asians). Averaging across the traits, we found that
the cross-population genetic correlation across East Asians and Europeans was
about 85%, although for some traits this quantity was much lower (e.g. ~30%
for major depressive disorer). This results suggest that genetic effects
in different populations are, overall, similar to each other. But, they are
not *exactly* the same, suggesting that genetic effects are dissimilar, in
other words, population-specific, for some parts of the genome.

We then looked specifically for components of the human genome that have
population-specific genetic effects. To our surprise, we found them in
functionally important components of the genome, such as gene regions, and
regions that regulate levels of expression of genes! This revealation is
in direct contrast to what we expected at the beginning of this project -- we
were expecting to find more shared genetic effects in functionally important
regions of the genome.

Now that we knew there are more population-specific genetic effects around
gene regions. We wanted to further understand what biological processes could
lead to such observations. To this end, we looked at cross-population genetic
correlation in different subsets of gene regions. Specifically, we looked at
regions of the genes that are specifically expressed in a tissue (e.g.
brain, liver, spleen, etc.). From this analysis, we realized that not all
gene regions have the same level of population-specific genetic effects.
For example, regions of immune genes have more population-specific
genetic effects, whereas regions of brain genes have less population-specific
genetic effects. Since immune genes are typically associated with positive selection
and brain genes negative selection, we conjecture that population-specific
genetic effects have something to do with gene-environment interactions
at genomic regions impacted by positive selection. However, we are not 100%
sure if this is indeed the right explanation, as biology is super complicated.

### What are the implications?

Perhaps the most relevant implication pertains to cross-population genetic
risk prediction. Most existing approaches to perform cross-population
genetic risk prediction first select some candidate genetic predictors
based on European studies, and then apply those predictors on non-Europeans.
These predictors tend to be around gene regions, and other functionally
important genomic regions. However, our results showing there are more
population-specific genetic effects around gene regions, suggest that these
approaches might not be optimal, because the effects of these predictors
might be different on non-Europeans than they are on Europeans. A more
accurate approach should select and prioritize genetic predictors, based on how important
they are in the European study, and how likely they will have the same effect
in the target non-European populations.

Since we hypothesize that gene-environment interaction is likely stronger
in functionally important genomic regions, we also think it would be important
for future genetic studies to collect and model environmental effects,
to better reveal the *true* genetic effects.
