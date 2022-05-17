# Feature Design

- In Supervised learned, our goal is to map X->Y
- In Un-supervised learned, our goal is to find hidden structure in X
- In Representation learning: Extract structure in X to facilitate supervised learning

Feature Design: Manual heuristics that we use to create useful representations.

## Feature Design
Assume we are given raw features $X^{\prime} \in R^{m^{\prime}}$. Eg:
- Raw pixel data for images
- Word counts in text
- Raw measurements from sensors.

Goal is to extract *useful* features X \in R^{m} from this raw input.

Typical pipeline (manual feature desig)
- Generate candidate featurs
- Select a subset of the candidate features
- Test on validation data and iterate

## Feature Generation
Domain agnostic strategies (feature expansion strategies)

1) Polynomial feaure expansions

X = [x'[0], x'[0]^2 , x'[0]x'[1], x'[1]^2, ..., x'[i]x'[j], ..., x'[m']^2]

2) Interaction features:
X[k] = x'[i]x'[j]

3) Log transforms:
    - X[k] = log(x'[i]) , x[i] > 0
    - or
    - X[k] = log(x'[i] + 1) , x[i] >= 0
    - Not used on negative valued fatures.

Log transforms are useful for count data, which are positive and long tailed (number of followers, etc). Log transforms turn tailed distributions into normal distributions. This is very helpfull, especially if using linear models.

4) Domain-Specific feature design (Examples from NLP):
    - Raw features $X^{\prime} \in R^{m^{\prime}}$ contain word counts
        - Lexicon based features: 1 if one of list of features exist
        - Frequency transformations:
          - log transform: X[k] = log(x + 1)
          - Weighted by sum
          - Binarization: 1 if word exists, 0 otherwise.
        - Inverse document frequency (IDF)
          - Define I(j) = |X \in D, x[j] > 0|. i.e: how many inputs have word j
          - tf-idf: X[k] = x[j] / log(I(j)). i.e: term frequecy inverse document frequecy.

## Feature Selection
Feature Ranking: Idea is to rank all features and select top-k.
- eg: Rank by correlation to the target
  - r(x[j], y) = | cov(x[j], y) / (\sigma_j \sigma_y) | > threshold
  - Limitation: only captures linear relationships
- eg: Rank by mutual information with the target
  - Can capture non-linear relationships, but prof said only tractable for binary/categorical features&targets.

Both methods above do not capture interactions. So we can do
- Subset Selection: Evaluate different subsets of feature


## References:
1. ML 451 lecture
