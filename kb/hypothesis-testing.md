# Hypothesis Testing

## Interesting notes
1. When the null hypothesis is true (and all test-assumtpions are met), p-values are uniformly distributed.
    - Using appropriate distributions for a given test statistic transforms the test-statistic to a uniform p-value.
    - If the null hypothesis is false, then the distribution of the p-value will be more weighted towards zero.
    - reference: [Stats stackexchange](https://stats.stackexchange.com/a/10617)

## Comparing means of multiple samples

### ANOVA: Analysis of Variance [1]
Null hypothesis: Mean of two or more groups are equal
$$ H_0 : \mu_i = \mu_j \qquad \forall i, j \in \{1, .., k\} $$
Alternate hypothesis: At least one two groups have different mean
$$ H_1 : \mu_i \neq \mu_j \ \text{for some} \ i \neq j $$

Assumptions:
1. All samples are independent
2. The data is normally distributed: i.e, the individual observations in each group are normally distributed (can test for normality, see below).
3. Each group has the same variance (can test for equal variance, see below).

In R, perform test using `aov` function.
```
summary(aov(time ~ hospital, data = data))
```

**Anova as a linear model:**
$$ y_{ij} = \mu + \tau_i + \epsilon_{ij} $$
Where $y_{ij}$ is an individual outcome, $\mu$ is the global mean, $\tau_i$ is the mean shift of each group from global mean, and $\epsilon_{ij}$ is the individual noise.

Assumptions:
- $E[\epsilon_{ij}] = 0$
- $\sum_i^k \tau_i = 0$

How is the linear model equivalent to the original hypothesis test?
$$ H_0 : \tau_i = 0 \quad \forall i \implies \mu_i = \mu_j = \mu \quad \forall i, j  $$

**Common pitfalls of ANOVA (and extensions)**:
- Using one-way ANOVA when there is more than one grouping variable
    - **Two-way ANOVA** (for example, measuring wait times across departments in different hospitals)
    - **Nested ANOVA** (for example, measuring wait times across hospitals with different departments)
- Conducting ANOVA multiple times for multiple outcomes
    - example: we measure multiple outcomes for each observation. Incorrect to creat separate ANOVA model for each type of outcome (multiple testing and possible dependence between the outcomes).
    - **MANOVA**: Multivariate Analysis of Variance.
$$ [y_{ij1}, \ y_{ij2}, \ y_{ij3}]^T = \mu + \tau_i + \epsilon_{ij} $$
- Incorrectly conducting multiple pair-wise comparisons following ANOVA
    - After a significant ANOVA p-value, we should **not** naively test all the pairs to identify the different ones. Instead, we should apply corrections for [multiple testing](https://en.wikipedia.org/wiki/Multiple_comparisons_problem). [[multiple-testing-problem]]
- Using ANOVA to analyse repeated-measures data
    - The samples are not independent (repeat measures at each group on same individuals). Use **rANOVA (repeated measures ANOVA)**.

If we are not sure or unable to satisfy the normality assumption, then a non-parametric test can be used instead. See below.

### Kruskal-Wallis test: nonparametric alternative to ANOVA
More details on [Wiki page](https://en.wikipedia.org/wiki/Kruskal%E2%80%93Wallis_one-way_analysis_of_variance)
- Does not assume normaly distributed data
- But also assumes that the population variances are similar.

## Test of Normality
Shapiro-Wilks test is a test of normality in frequntist statistics. It has the highest power for a given significance compared to several popular tests of normality. [2]

Null hypothesis: the data is normally distributed.

## Test of equal variance
Common tests such [Bartlett test](https://en.wikipedia.org/wiki/Bartlett%27s_test) and [Fligner-Killeen test](http://www.statsref.com/HTML/index.html?fligner-killeen_test.html)

## References
1. Analysis of Variance: [url](https://www.rebeccabarter.com/blog/2017-02-17-anova/)
2. Shapiro-Wilk test wiki: [url](https://en.wikipedia.org/wiki/Shapiro%E2%80%93Wilk_test)