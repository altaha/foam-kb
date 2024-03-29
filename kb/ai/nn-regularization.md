# Regularization - Neural Netowrks

Use to comate overfitting in NNs

## L2 regularization
Standard approach is to apply L2-regularization to certain layers
$$ J_{reg} = J + \lambda \left( \sum_{i=1}^{H} ||\textbf{W}^{(i)}||_F^2 + ||\textbf{w}_{out}||_2^2 \right) $$

i.e Add a Frobenius (aka matrix L2) norm of hidden layer and output weights to our loss function J.
$$ ||\textbf{A}_{m \times n}||_F = \sqrt{\sum_{i=1}^m \sum_{j=1}^n a_{ij}^2 } $$

We could also use L1 regularization, or different norms. But L2 is typically most popular.

Referred to as "L2 regularization", "Weight Decay", or "Ridge style regularization" in the NN community.

## Dropout
[[todo]]

#neural-networks #regularization

[//begin]: # "Autogenerated link references for markdown compatibility"
[todo]: ../../todo.md "Todo"
[//end]: # "Autogenerated link references"