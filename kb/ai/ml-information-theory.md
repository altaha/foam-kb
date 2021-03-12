# Information Theory

## Information Content in an event
Information content in an event h(p(x)) = -log(p(x))

We choose log because:
- we want it to be inversely proportional to probability (0 surprise if event with probability 1 occurs. Infinite probability if even with probability 0 occurs).
- We could use 1/p, but log allows information to be additive
  - For example, information in two independent events x and y = -log(p(x)) - log(p(y))
- Has the nicee property of being interpretable as bits or nats (log base 2 and natural log, respectively).

## Entropy: Expected Information Content in a distribution
Generalize this to an entire distribution, not just an event:

Entropy: H(X) = E[-log(X)] = -1 * \Sigma_{x \in X} p(x) log(p(x))

## Entropy between RVs
1) Conditional Entropy
- How surprised we would be to observe Y given we know X.
Conditional Entropy (Y|X) = -1 * \Sigma_{x \in X, y \in Y} p(x, y) log(p(y | x))
- if X independent with Y: H(Y|X) = H(Y)
- if Y a deterministic function of X: H(Y|X) = 0

2) Relative Entropy (KL-Divergence):
KL(P || Q) = -1 * \Sigma_{x \in X} P(x) log(q(x) / P(x))
           = E_{x~P(x)} [-log(Q(x)/P(x))]

P and Q assign different probabilities to the same set of events X.

How many extra bits we need if we encode P using Q.

### Cross-Entropy and KL-Divergence
Recall: L(y, y_hat) = -y log(y) - (1-y)log(1-y_hat)
- This cross-entropy loss (assuming binary values) is the same as KL-Divergence of approximating y with y_hat.

##### KL-Divergence and Maximum Likelihood:
- KL(P || P_theta) : P is true distro, P_theta is estimated distro
- KL(P || P_theta) = -1 E_{x~P(x)} [log(P_theta(x) / P(x))]
                    = -1 E_{x~P(x)} [log(P_theta(x))] + E_{x~P(x)} [log(P(x))]
                                                        (the second term is just H(P(X)) and we ignore it)
                    = - Sigma_{x \in X} P(x) log(P_theta(x))
                    ~= -1/|D| * Sigma_{x \in D} log(P_theta(x)) ; with D ~ P(X) - approx equal by the law of large numbers

So minimizing Negative Log Likelihood is equivalent to minimizing KL-Divergence from P_theta to P

## Mutual Information
I(X, Y) = KL( P(X, Y) || P(X)P(Y))
        = H(X) - H(X|Y)
        = H(Y) - H(Y|X)
- If X and Y are independent, I(X,Y) = 0
- If X and Y are deterministic on each other, I(X,Y) = max(H(X), H(Y))

It is useful as a measure of independence (with no linearity assumpions like correlation). The downside is that it is expensive to compute.
