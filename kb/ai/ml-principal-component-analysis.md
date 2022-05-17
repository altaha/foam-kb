# Principal Component Analysis

One of the most fundamental techniques for representation learning.

Professor's thoughts:
- A fair bit of his research has been a variation of PCA in some way.

## PCA
Motivation/Idea: Learn a low dimensional subspace s \in R^m that encodes the most important aspects of our data.

Inputs: features X \in R^m
- might be raw features
- might be designed features
- m is reasonably large
- Not all features are necessarily useful.

Outputs: low-dimensional codes z \in R^d to replace our features, where d << m

## Projecting to a subspace
$x^\sim = Uz + \mu = z_1 u_1 + z_2 u_2 + \mu$

z = U^T (x - \mu)
- U is the project matrix. U \in R^{m, d} with orthonormal rows. i.e: UU^T = I
- \mu is the mean or origin point. $\mu = 1/|D| * \sum_{x \in D} x$

## What makes a good projection?
Reconstruction Error

Define the reconstruction of a point x from z as
$$x^\sim = Uz + \mu \qquad z = U^T (x-\mu) \qquad z \in R^d, X \in R^m$$

Define the reconstruction error as
$$||X - X^\sim||^2 ...$$

Another way to define reconstruction quality, is the retained variance:

Retained Variance:
$$ \sum_{j=0}^{d-1} Var(z[j]) = \frac{1}{|D|} \sum_{j=0}^{d-1} \sum_{i=0}^{|D|-1} (z_i[j] - z_{jbar})^2 = \frac{1}{|D|} \sum_{i=0}^{|D|-1} ||z_i[j] - z_{jbar}||^2 = $$
$$ = \frac{1}{|D|} \sum_{i=0}^{|D|-1} ||z_i[j]||^2 \qquad , since z_{jbar} = 0 (proven in practice assignment)  $$

**Retained Variance and Reconstruction error are equivalent**
- So minimizing recontruction error is equivalent to maximizing retained variance.

Peshi was having her interview. I kinda need to review the entire lecture and notes.

## References:
1. ML 451 lecture
