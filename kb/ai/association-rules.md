# Association Rules Mining

Rule-based machine learning techniques
- Became popular due to (Agrawal, R.; Imieliński, T.; Swami, A. (1993). "Mining association rules between sets of items in large databases").
- Focus is on finding patterns and associations between in a sales/transactions database.

Given
- set of items I = {i_1, i_2, ..., i_n}
- a transactions Database T = {t_1, t_2, ..., t_m}, each transaction consists of a subset of I.

Find Rules, such as:
> X -> Y, where X, Y are subsets of I

in original paper |X| <= n, |Y| = 1

## Techniques
### Constraints on significance and interestingness
Best known constraints are minimum thresholds on Support and Confidence. Used to select interesting rules. Rules are usually required to satisfy some minimum Support and minimum Confidence.

**Support(X)**: Number of transactions where an itemset, like X, appears in database T, divided by |T|
- Support X = (Number_of_Transactions conaining X) / |T|
- kind of like a marginal P(X)

**Confidence(X, Y)**: Proportion of transactions which contain X, that also contain Y
- Confidence(X, Y) = Support(X U Y) / Support (X)
- Kind of like a conditional P(Y | X)

**Lift(X, Y)** = Support(X U Y) / (Support(X) * Support(Y))
- Ratio of observed support over that if X, Y were assumed to be independent. Lift > 1 indicates a relationship/dependence. Lift < 1 means they are substitutes. Lift = 1 means their occurence is independent and no rule can be used.

**Conviction**: seems like a proxy for precision, or how many errors a rule can make.

### Process to find Rules
1. Find all frequent itemsets (X) that satisfy minimum Support
2. A minimum Confidence threshold is applied to itemsets from 1 to form rules.

Step 1 in a large database is difficult. There are 2^(n) - 1 possible itemsets (this is number of subsets from set size n, minus the empty set).
- But subsets have a property, for a frequent itemsets, all of its subsets are also frequent. That is, no infrequent itemset can be subset of a frequent itemset. This is called the **downward closure property**, and is the basis of Apriori and Eclat aglorithms.
Step 2 is easy, given step 1 (Wikipedia says this, I still dont see it).

With large datasets, there may be lots of spurious associations. Statistical confidence may be used to reduce the risk of spurious associations. But not much more info was given.

### Algorithms for generatin rules
- **Apriori algorithm**: uses a breadth-first search strategy to count the support of itemsets and uses a candidate generation function which exploits the **downward closure property**.
- **Eclat algorithm**: depth-first search based on set intersection, allows parallel execution.
- **FP Growth**:

## FP-Growth Algorithm
- This was first referred to me by interview candidat from Grab.

FP stands for Frequent Pattern.

Seems to recursively build a [[Trie]] structure of transactions (itemsets). Items in a transaction are sorted in descending order of most frequently occuring items. When growing the trie, nodes that dont meet minimum support are pruned.

Once the recursive process completes, all frequent itemsets with minimum support have been found. Then, the second step of forming association rules can be done.

## References
Source: [Wikipedia Article](https://en.wikipedia.org/wiki/Association_rule_learning)
