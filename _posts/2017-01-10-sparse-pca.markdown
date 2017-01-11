---
layout: post
title:  "Sparse PCA"
date:   2017-01-10
category: statistics
---

<script type="text/javascript"
src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

### Abstract
Principal component analysis (PCA) is a widely used technique in machine learning and computational biology.
Although dimension reduction can be easily achieved by using the top principal directions, a large number of
loadings in the principal directions are non-zero, making interpretation difficult. This paper reviews several
algorithms to perform sparse PCA that improves interpretability of PCA as well as an application of sparse PCA
in computational biology.

### Introduction

Principal component analysis (PCA) is a dimension reduction technique widely used in the field of
machine learning, computational biology, image processing, etc.
Various interpretations
of PCA exist. However, perhaps the most intuitive interpretation of PCA is that it
aims to find orthogonal directions \(principal directions\) such that when data points are projected
onto these directions, variance of data along these directions are maximized. In a typical
PCA, the top principal directions explain most of the variance in the data, and therefore can be used
to accurately reconstruct the data. This property of PCA enjoys wide applications in image compression. What's more, components of these principal directions (loadings) offer great insight as to
which variables contribute greatly in explaining variance in the data. For example, in a PCA on gene
expression data, the loadings of principal directions tell researchers the most relevant genes
(eigen genes) to follow up in downstream analysis.  However, as PCA does not impose sparsity
constraints on the loadings of principal directions, the loadings are non-zero in general,
making interpretations of PCA very difficult.

To improve interpretability of PCA, various approaches to obtain sparse principal direction loadings
have been proposed. These methods are termed "sparse principal component analysis" (sparse PCA).
In general, sparse PCA can be formulated as an optimization problem over the vector of loadings, with
constraints on the\\(\ell_0\\)norm of the vector. Since optimization problems involving\\(\ell_0\\)norms are in
general NP-hard, most methods impose an\\(\ell_1\\)norm in the objective function to promote sparsity
in the vector of loadings as a relaxation of the\\(\ell_0\\)norm.

This literature survey focuses on two aspects of sparse PCA -- algorithms for performing sparse
PCA and applications in computational biology that harness the interpretability of sparse PCA.
The rest of this review paper is composed of three parts. The first part of this survey reviews
general formulations of PCA and establishes sparse PCA as optimization problems. The second part of
this survey reviews various optimization algorithms to obtain sparse PCA loadings. And finally,
the third part of this survey reviews an application of sparse PCA in the field of
computational biology.

### Formulations of PCA and sparse PCA as optimization problems

#### Formulation of PCA

In this survey, we adopt the interpretation of PCA as finding directions of projection such that when data
points are projected onto these directions, variance of data along that direction is maximized.
Let\\(\mathbf{X}\\)be the\\(n \times p\\)data matrix, where\\(n\\)is the number of observations and\\(p\\)the number of variables.
We assume that each column (\\(\mathbf{X}_i\\)) in\\(\mathbf{X}\\)have mean 0. Let\\(\mathbf{v}\\)be a direction for projection such
that\\(\|\mathbf{v}\| = 1\\) Then the projection of each row (\\(\mathbf{x}_i\\)) onto\\(\mathbf{v}\\)is\\(\mathbf{x}_i^T \mathbf{v}\\) and the
vector of projections for all data points is\\(\mathbf{X}\mathbf{v}\\) Because\\(E[\mathbf{X}] = \mathbf{0}\\) we have
\\(E[\mathbf{X}\mathbf{v}] = \mathbf{0}\\) And therefore the variance of\\(\mathbf{X}\mathbf{v}\\)is simply\\({1 \over n} \mathbf{v}^T\mathbf{X}^T\mathbf{X}\mathbf{v}\\)
where\\({1 \over n} \mathbf{X}^T\mathbf{X}\\)is nothing more than the sample covariance matrix (\\(\pmb{\Sigma}\\)) of\\(\mathbf{X}\\)
Therefore, PCA can be formulated as the following optimization problem
\\[
    \text{maximize } {1 \over 2} \mathbf{v}^T\pmb{\Sigma}\mathbf{v}       \text{}    \mathbf{v}^T\mathbf{v} = 1,
\\]
which has Lagrangian
\\(L(\mathbf{v}, \lambda) = {1 \over 2} \mathbf{v}^T\pmb{\Sigma}\mathbf{v} + \lambda \mathbf{v}^T\mathbf{v} - \lambda\\) Setting
derivative of the Lagrangian with respect to\\(\mathbf{v}\\)to 0, we arrive at the equation\\(\mathbf{\Sigma}\mathbf{v} = \lambda \mathbf{v}\\)
Therefore, the PCA optimization problem can be solved by finding the eigenvectors of the covariance matrix\\(\pmb{\Sigma}\\)
The optimal\\(\mathbf{v}\\)for this problem however can have many non-zero elements, which makes the result difficult to interpret.

#### Formulation of sparse PCA

To address the non-sparsity issue of traditional PCA, sparse PCA imposes additional constraint on the number of non-zero element
in the vector\\(\mathbf{v}\\) This is achieved through the\\(\ell_0\\)norm, which gives the number of non-zero element in the vector
\\(\mathbf{v}\\) A sparse PCA with at most\\(k\\)non-zero loadings can then be formulated as the following optimization problem
\\[
    \text{maximize } {1 \over 2} \mathbf{v}^T\pmb{\Sigma}\mathbf{v}       \text{ subject to }    \mathbf{v}^T\mathbf{v} = 1, \|\mathbf{v}\|_0 \le k.
\\]
Optimization problems with\\(\ell_0\\)norm constraint is in general NP-hard. Therefore, most methods for sparse PCA relaxes
the\\(\ell_0\\)norm constraint with\\(\ell_1\\)norm appended to the objective function. The following sections
reviews different formulations of sparse PCA as well as algorithms for optimizing the objective.

### Sparse PCA algorithms

#### Sparse PCA via thresholding and rotation

Prior to the invention of "least absolute shrinkage and selection operator" (LASSO), sparse PCA is
mostly achieved through  thresholding and rotation.

The thresholding method improves
interpretability of PCA by restricting interest to variables with large loadings and filters out
variables with small loadings. This method is useful if the difference between loadings of different
variables is clear, but less useful when there is no clear cut between the loadings.

The rotation method
aims to find a transformation matrix\\(\mathbf{T}\\)such that the loading matrix (\\(\mathbf{A}\\)) after
transformation by\\(\mathbf{T}\\)(i.e. the matrix\\(\mathbf{AT}\\)) is simple, in the sense that there's clear
cut between large and small values of\\((\mathbf{AT})\_{ij}\\)
Various criteria to define the simplicity criteria exist, the most widely used criteria is the varimax
criteria, which aims to find\\(\mathbf{T}\\)such that variance of\\((\mathbf{AT}\_{ij})^2\\)is maximized.
Specifically, varimax finds the rotation matrix\\(\mathbf{T}\\)that maximizes
\\[
    {1 \over {kp}} \sum\_{1=1}^k \sum_{j=1}^p (\mathbf{AT}\_{ij})^4
    -\left( {1 \over {kp}}\sum\_{1=1}^k \sum\_{j=1}^p (\mathbf{AT}\_{ij})^2 \right)^2,
\\]
where\\(k\\)is the number of principal directions to include in the analysis.
However, a major drawback of the transformation approach is that the property that each principal
direction explains successively less variance is lost, introducing ambiguity as to which principal
direction should be kept.

#### Sparse PCA via LASSO (SCoTLASS)

Since its invention, LASSO has been widely applied in regression as a powerful method to perform variable
selection, as it efficiently sends the effect estimation of irrelevant variables to 0. The paper
is the first method to apply the concept of LASSO in the problem of sparse PCA.

SCoTLASS (Simplified Component Technique-LASSO) imposes a constraint on the\\(\ell_1\\)norm of the vector
of loadings, which can be viewed as a relaxation of the\\(\ell_0\\)norm. Specifically, SCoTLASS aims to solve the
following optimization problem
\\[
\text{maximize } \mathbf{v}_i^T\pmb{\Sigma}\mathbf{v}_i      
\text{ subject to }    \mathbf{v}_i^T\mathbf{v}_i = 1, \|\mathbf{v}_i\|_1 \le k \text{, }
\mathbf{v}_i^T\mathbf{v}_k = 0 \text{ for } i < j.
\\]
When\\(k\\)is greater than\\(\sqrt{p}\\) SCoTLASS reduces to the traditional PCA, as\\(\|\mathbf{v}_i\|_1\\)is naturally
upper-bounded by\\(\sqrt{p}\\)by the constraint\\(\mathbf{v}_i^T\mathbf{v}_i=1\\) When\\(k = 1\\) then exactly one component
of each\\(\mathbf{v}_i\\)is 1 and all other components are 0. Variable degrees of sparsity can be achieved by setting
\\(k\\)between\\(1\\)and\\(\sqrt{p}\\) In general, one should test different values of\\(k\\)and choose the value of
\\(k\\)that makes the most sense.

The authors proposed a projected gradient algorithm to optimize the above constrained optimization problem.
Since the problem is not convex, multiple random starts are necessary to find the global optimal. This
potentially increases the run time of the algorithm.

Although SCoTLASS gives sparse loading vectors through the\\(\ell_1\\)norm constraint, the principal components,
projections of the data points onto the principal directions, are not necessarily independent. One
can replace the constraint\\(\mathbf{v}_i^T\mathbf{v}_k = 0\\)(every principal directions are independent) with the constraint
\\(\mathbf{v}_i^T \pmb{\Sigma} \mathbf{v}_k = 0 \text{ for }\\)to enforce independent principal components.
However, both constraints cannot be satisfied at the same time.

SCotLASS also suffers from the drawback that when the number of variables is much larger than the number of observations
(i.e.\\(p \gg n\\)) then SCoTLASS only selects at most\\(n\\)non-zero elements in the loading vectors.
This is of course not a desired property, as in computational biology it's often the case that\\(p \gg n\\) and
that selecting only\\(n\\)variables is in general not very informative.

#### Sparse PCA as a regression-type problem (SPCA)

In the paper, the authors offer an alternative solution to sparse PCA by framing PCA as
a regression-type problem, and enforcing sparsity by imposing the elastic-net penalty involving both
\\(\ell_1\\)norm and\\(\ell_2\\)norm of the loading vector\\(\mathbf{v}\\)

SPCA views PCA from the angle of singular value decomposition. Let\\(\mathbf{X}\\)be the\\(n \times p\\)data matrix,
then PCA can be performed by performing a SVD and\\(\mathbf{X} \\)
\\[
\mathbf{X} = \mathbf{U} \mathbf{D} \mathbf{V}^T,
\\]
where\\(\mathbf{Z}_i = \mathbf{U}_i \mathbf{D}\_{ii}\\)gives the principal component of each observation, and\\(\mathbf{V}_i\\)is the corresponding
principal direction. Since\\(\mathbf{Z}_i\\)can also be obtained by projecting\\(\mathbf{X}\\)on the the vector\\(\mathbf{V}_i\\)(i.e.\\(\mathbf{Z}_i = \mathbf{X}\mathbf{V}_i\\)),
one can view PCA as a regression problem where\\(\mathbf{Z}_i\\)is the response vector and\\(\mathbf{V}_i\\)the regression coefficient.
To improve sparsity, authors of SPCA propose to impose the elastic-net penalty, resulting in the optimization problem
\\[
\text{maximize } \|\mathbf{Z_i} - \mathbf{X}\pmb{\beta}\|^2 + \lambda_1 \|\pmb{\beta}\|^2 + \lambda_2 \|\pmb{\beta}\|_1.
\\]
Let\\(\hat{\pmb{\beta}}\\)be the optimal solution to the above problem, then sparse PCA loading vector can then be approximated
by\\(\mathbf{V}_i = { {\hat{\pmb{\beta}}} \over {\|\hat{\pmb{\beta}}\|} }\\) The elastic-net penalty also allows for more than\\(n \\)
selected variables when\\(p \gg n\\) an improvement from SCoTLASS.

The formulation of the problem above requires an initial PCA to obtain the principal components. The authors also proposed
a self-contained method to obtain sparse PCA loadings by maximizing the following objective function over\\(\mathbf{A}\\)and\\(\mathbf{B} \\)
\\[
\sum_{i=1}^n \|\mathbf{x}_i - \mathbf{AB}^T\mathbf{x}_i\|^2 + \lambda_1 \|\pmb{\beta}\|^2 + \lambda_2 \|\pmb{\beta}\|_1,
\\]
with the constraint that\\(\mathbf{A}^T\mathbf{A} = \mathbf{I}_k\\) The optimal\\(\mathbf{B}\\)gives the sparse loading vectors.
The authors propose to use block descent to perform the optimization, that is first fix\\(\mathbf{A}\\)maximize over\\(\mathbf{B} \\)
and then fix\\(\mathbf{B}\\)maximize over\\(\mathbf{A}\\) repeat until convergence.

#### Sparse PCA via penalized matrix decomposition

Instead of formulating sparse PCA as a regression-type problem, the paper propose to perform sparse PCA using
penalized matrix decomposition (PMD). A regular SVD of a matrix\\(\mathbf{A}\\)aims to find\\(\mathbf{u}\_i\\)\\(d\_i\\) and\\(\mathbf{v}\_i \\)
such that
\\[
    \sum\_{i=1}^p d_i \mathbf{u}\_i \mathbf{v}\_i^T = \mathbf{A}.
\\]
(And it's proven by Eckart and Young that the best, in the sense of Frobenius norm, rank\\(r\\)approximation of a matrix\\(\mathbf{A}\\)
is\\(\sum\_{i=1}^r d\_i \mathbf{u}\_i \mathbf{v}\_i^T = \mathbf{A}\\))
However, this often yields\\(\mathbf{u}\\)and\\(\mathbf{v}\\)that contain many non-zero elements. To improve sparsity in\\(\mathbf{u}\\)and
\\(\mathbf{v}\\) the authors propose to constraint\\(\mathbf{u}\\)and\\(\mathbf{v}\\)with sparsity penalties, and obtain the following formulation
for rank-1 approximation of the matrix\\(\mathbf{A} \\)
\\[
        \text{minimize  }  {1 \over 2} \|\mathbf{A}-d\lambda \mathbf{u}\mathbf{v}^T\|^2_F
        \text{ subject to  } \mathbf{u}^T\mathbf{u} = 1, \mathbf{v}^T\mathbf{v} = 1 \text{, }  d \ge 0 \text{, }
                               P_1(\mathbf{u}) \le c\_1 , P\_2(\mathbf{v}) \le c\_2,
\\]
where\\(P_1\\)/\\(P_2\\)are convex penalty functions on the sparsity of\\(\mathbf{u}\\)/\\(\mathbf{v}\\)and\\(c_1\\)/\\(c_2\\)are the maximum
allowable sparsity for\\(\mathbf{u}\\)/\\(\mathbf{v}\\) The problem is convex if one of\\(\mathbf{u}\\)and\\(\mathbf{v}\\)is fixed, and therefore
the problem can be solved by iteratively maximizing over\\(\mathbf{u}\\)and\\(\mathbf{v}\\)while fixing the other.
To obtain the\\((i+1)\\)th decomposition, one subtracts\\(d_i\mathbf{u}_i\mathbf{v}_i^T\\)from\\(\mathbf{A}\\)and solve the above optimization
problem. This allows one to obtain the full spectrum of decomposition while keeping the orthogonality between
\\(\mathbf{u}_i\\)and\\(\mathbf{v}_i\\)

#### Sparse PCA via semidefinite programming (DSPCA)

While all previous sparse PCA methods focus on obtaining the full spectrum of principal directions,
the paper focuses on obtaining a sparse rank-1 approximation of a positive definite matrix\\(\mathbf{A}\\)
using only the top principal direction. Here, the optimization problem is formulated as
\\[
        \text{ minimize  } \|\mathbf{A}-\lambda \mathbf{x}\mathbf{x}^T\|^2\_F
        \text{ subject to  } \mathbf{x}^T\mathbf{x} = 1, \text{ } \lambda \ge 0 \text{, }
                             card(\mathbf{x}) \le k ,
\\]
where\\(\mathbf{x}\\)is the variable being optimized over and\\(card(\mathbf{x})\\)gives the number of non-zero elements
in the vector\\(\mathbf{x}\\) and is used to control sparsity in\\(\mathbf{x}\\)
The problem above is equivalent to the problem
\\[
        \text{ minimize  } \mathbf{x}^T\mathbf{A}\mathbf{x}
        \text{ subject to  } \mathbf{x}^T\mathbf{x} = 1 \text{, }
                              card(\mathbf{x}) \le k.
\\]
The constraint on\\(card(\mathbf{x})\\)in general makes the problem NP-hard, therefore, the authors relaxes this constraint
with matrix\\(\ell_1\\)norm and obtains the following optimization problem
\\[
        \text{ minimize   }    tr(\mathbf{AX})
        \text{ subject to  } tr(\mathbf{X}) = 1 \text{, }
                                   \mathbf{1}^T |\mathbf{X}| \mathbf{1} \le k \text{, }
                                   \mathbf{X} \succeq \mathbf{0},
\\]
where\\(|\mathbf{X}|\_{ij} = |\mathbf{X}\_{ij}|\\) The sparse loading vectors\\(\mathbf{x}\\)is obtained by performing an eigen-decomposition
on the matrix\\(\mathbf{X}\\) Although not theoretically guaranteed, in practice, the matrix\\(\mathbf{X}\\)has low rank.

The optimization problem above is a type of semidefinite programming problem, and can be solved using interior-point solvers.
The same problem formulation can also be generalized to non-square matrices. For large-scale problems, the authors
conjecture that first-order methods might speed up the optimization procedure.

#### Sparse PCA via truncated power method (TPower)

The paper also focuses on sparse rank-1 approximation of a positive semidefinite matrix\\(\mathbf{A}\\)
In the paper, the authors proposed a modification of the iterative power method for approximately finding the largest
eigenvalue (\\(\lambda_{max}\\)) and its corresponding eigenvector (\\(\mathbf{v}\\)) with sparsity constraint that\\(\|\mathbf{v}\|_0 \le k\\)
Here,\\([|\mathbf{v}|]_k\\)gives the\\(k\\)th largest value in\\(|\mathbf{v}| = (|\mathbf{v}_i|)\\) and\\(\text{Truncate}(\mathbf{v}, S)\\)
truncates\\(\mathbf{v}\\)such that\\(\mathbf{v}_i = 0\\)for all\\(i \notin S\\) Line 4 of the algorithm performs a normal
iterative power method for finding the eigenvector corresponding to the largest eigenvector of\\(\mathbf{A}\\) And
line 6 and 7 of the algorithm performs the truncation and the normalization. Obviously, in each iteration the constraints
\\(\|\mathbf{v}\|_0 \le k\\)and\\(\|\mathbf{v}\| = 1\\)are satisfied. The authors proves convergence by showing that sequences
\\(\mathbf{v}_t^T\mathbf{A}\mathbf{v}_t\\)decreases monotonically for the sequence of updates\\(\mathbf{v}_t\\)


### Identifying ancestry-informative markers in GWAS via sparse PCA

Genome-wide association study (GWAS) aims to find genetic markers that are significantly associated with diseases/traits.
For example, for case-control trait studies, one tests if the frequency of any specific allele of a genetic marker is significantly different
in the cases than in the controls. However, when collecting samples for GWAS, the sample collected often consists
of individuals of different ancestries, which have different allele frequencies for some genetic markers. In the study
of genetics, we call this non-homogeneous sample "population stratification". Population stratification causes
allele frequency difference of a genetic marker in case-control studies, which in turn causes spurious associations
that are not informative because the association is induced by different ancestry rather than underlying biology.

To account for population stratification, researches perform principal component analysis on genetic data, and use
principal component scores, which captures the amount of information on ancestry genetic markers carry, as covariates
in association studies. This approach has been very successful in reducing uninformative associations in GWAS. However,
very often people also wants to find out which genetic markers are informative in determining ancestry
(i.e. ancestry informative markers, or AIM) so that when performing
GWAS, researchers can pay extra attention to those markers.

The paper applies sparse PCA, formulated as a regression-type problem with LASSO penalty, to identify AIMs,
which are genetic markers with 0 loadings. By analyzing 1000 Gnome Project data, the authors found, among a set of 24,395
genetic makers, about 5,000 ancestry informative genetic markers. And they show that these markers are accurate in
determining the ancestry of an individual.

### Conclusion

In this literature survey, I have reviewed the basic formulation of sparse PCA, algorithms to perform sparse PCA,
as well as an application of sparse PCA in identifying ancestry informative markers. Most algorithms to perform
relaxes the sparsity constraint using the\\(\ell_1\\)norm penalty. However, there are also a few algorithms that directly
enforce sparsity via semidefinite formulation or truncating. In this literature survey, my focus is on the general algorithm
instead of the details (i.e. complexity, memory footprint). As dimension of data becomes larger, algorithms to perform
sparse PCA must be efficient in time as well as in memory.
