# Gaussian Mixture Models (GMM)

- In Supervised learned, we model P(y | X)
- In Unsupervised learned, we model P(X)
    -- Often called Density Estimation
    -- We saw an example when we did Maximum Likelihood for Gaussian.
    -- In GMM, we model our data as being a result of sum/mix of multiple gaussians.

- Single Gaussian model: one $\mu$ and $\Sigma$.
- A mixture of Gaussians is a weighted sum of K $\mu$'s and $\Sigma$'s.

## Likelihood of a GMM
Model parameters: $\Theta = \{ \pi_z, \mu_z, \Sigma_z, z=1,..,K \}; \quad note: \sum_K(\pi_z) = 1$

- Assume that the points X are independent.
- The log likelihood expression is complex because we have a log of a sum.
- The log likelihood is not convex.

### Latent Variables
Consider the following generative process that generates a point X
1.) First, we sample a cluster id from z ~ Categorical(\pi)
2.) Next, we generate x by sampling from cluster z, i.e N(\mu_z, \Sigma_z)

Under this latent generative process, we get the same Likelihood, i.e:
$$
log(L(D, \Theta)) = \sum_{X \in D} log \left( \sum_{k=1}^{K}  P(z=k)P(X | z=k) \right)
                  = \sum_{X \in D} log \left( \sum_{k=1}^{K} \pi_k \cdot \mathcal{N}(\mu_k, \Sigma_k) \right)
$$

Key idea: if we knew the cluster assignment for each point X_i \in D, then the max likelihood becomes easy o solve (eliminates the log of a sum).
$$ log(L(D, \Theta)) = \sum_{X \in D} log( \pi_k \cdot \mathcal{N}(\mu_z, \Sigma_z) ) $$

Hence the MLE solution would be:
- $$ \mu_k = \sum_{(x, z) \in D; \ s.t \ z=k} \frac{x}{|(x, z) \in D; \ s.t \ z=k|} $$
- $$ \Sigma_k = \sum_{(x, z) \in D; \ s.t \ z=k} \frac{(x-\mu_k)(x-\mu_k)^T}{|(x, z) \in D; s.t \ z=k|} $$
- \pi_k = (I missed it), but probably just a proportion

Of course we dont know these latent cluster assignments beforehand..

## Expectation Maximization
1.) Guess some initial $\pi_z, \mu_z, \Sigma_z, \forall z=1,..,K$

2.) Based on our current guess params, make a soft assignment of each point to each cluster. i.e estimate $z_i \ \forall x_i \in D$ . This is the **Expectation** step

3.) Recompute our Parameters based on the estimated cluster assignments (**Maximization** step).

4.) Repeat steps 2 and 3 until convergence.

### Expectation step
$$
\begin{aligned}
r(x, k) = P(z=k | x) &= \frac{ P(x | z=k) P(z=k) }{ P(x) } \\
                      &= \frac{ P(x | z=k) P(z=k) }{ \sum_{j=1}^{K} P(x | z=j) P(z=j) } \\
                      &= \frac{ \pi_k \cdot \mathcal{N}(x | \mu_k, \Sigma_k) }{ \sum_{j=1}^{K} \pi_j \cdot \mathcal{N}(x | \mu_j, \Sigma_j) }
\end{aligned}
$$
Note: $\sum_{K} r(x, k) = 1$

### Maximization step
$$ log(L(D, \Theta)) = \sum_{X \in D} log( \pi_k N(\mu_z, \Sigma_z) ) $$
To solve for the $\mu_k$'s: Take the drivative of ^ with respect to $\mu_k$:
- covered quickly. Need to review notes.

But it leads to quick closed form MLE solutions for $\mu_k$, $\Sigma_k$, and $\pi_k$

Remaining Questions:
- Is EM guaranteed to converge?
- Which aspects of EM are generic? can it be used for other problems besides GMM?

## References:
1. ML 451 lecture
