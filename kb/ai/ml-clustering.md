# Clustring

Unsuperviised ML: Given only an X dataset (no labels).
Examples:
- Dimensionality reduction / compression
- Anomaly Detection
- Clustering

## Clustering
Assume that X \in D belong to one of K distinct clusters

Clustering function: f(x): R^m -> Z
- Z = {1, ..., K}
- z \in Z to denote a particular cluster. z is a latent variable.
- K is a hyperparameter

## Agglomerative Clustering
Bottom-up clustering. From aggolmerate.

Algorithm:
1. Let x_i \in D and x_j \in D be two points such that
```
x_i, x_j = argmin ||x_1 - x_2||
x_1, x_2 \in D;  x_1 != x_2
```
2. Merge x_i and x_j into a cluster, C = {x_i, x_j}
3. Create a new point x_c = (x_i + x_j)/2. Add x_c to D and remove x_i and x_j from D.
4. Repeat 1-3 until |D| < \gamma or if ||x_1 - x_2|| = \alpha \forall x_1, x_2 \in D, x_1 != x_2

As a result, you get a clustering heirarchy. You can choose how to treat the heirarchy.

## K-Means
1. For each z \in {1, 2, ..., k} start wtith a random guess \mu_c_z \in R^m
2. For x \in D, assign to a cluster
```
C_z = {X \in D: ||x - \mu_c_z|| ||x - \mu_c_j|| \forall j \in [k], j != z}
```
3. Recompute the cluster centroids based on the assignments from step 2:
```
\mu_c_2 = 1 / (|C_2|) * \Sum_{x \in C2} (x)
```
4. Repeat steps 2 and 3 until no reassignments are made.

### K-Means issues:
- Initilaization is important, and can affect the result.
- Initializing centroids close to each other can lead to poor cluster
- Heuristics exist to reduce chance of bad clustering.
  - For example: pick a random point as centroid, pick next centroid at least some distance away.

### Convergence of K-Means
- Theorem: K-Means always convergees in a finite number of iterations

Lemma:
- Let \mu_c = 1 / |C| * \Sum_{X \in C} (X_c), then
- \Sum_{X \in C} ||X - \mu_c|| <= \Sum_{X \in C_complement} ||X - q||, \forall q \in R^m (q is any vector)
  - That is, \mu_c minimizes the sum of distances of points in C to any point.

Definitions:
- S(C_z, \mu_c_z) = \Sum_{X \in C_z} ||X - \mu_c_z||^2   (S is a scoring function)
- I missed something here, about S_^_*

Proof of convergence theorem:
- Key idea: If K-Means did not converge, then at least one point is re-assigned.
- We show that S_{*}_{t+1} < S_{*}_{t} if any points are re-assigned.
- Every assignment always improves our sum of square errors, and there is a finite number of clustrings, so it will converge in finite iterations.

- Fact1: when we change cluster assignments, we reduce the sum of squarred errors (strictly less than).
- Fact2: When we recompute centroids after re-assignments, we don'tt make things worse (less than or equal to).
- Combining fact 1 and fact 2 proves convergence

### Soft K-Means
1. For each z = 1, ..., k, initializee a random \mu_c_z \in R^m
2. For each x \in D, compute:
```
- r(x, z) = \frac_{ e^-(||x-|mu_c_z||^2) }_{ \sum_{j=1,..,K} ( e^-(||x-|mu_c_j||^2 )}
- r is a score/probability that x \in  C_z. It is a softmax computation of distance to centroid normalized by sum of distance to all centroids.
```
3. Recompute the cluster centroids:
    \mu_c_z = [ \sum_{x \in D} r(x, z) * x ] / [ \sum_{x \in D} r(x, z) ]


## References:
1. ML 451 lecture
