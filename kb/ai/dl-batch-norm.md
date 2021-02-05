# Batch Normalization (DL)

Typically your NN model (usually deep NN) is a chain of transformations. Like

$$y = f(f(x, \theta_1), \theta_2)$$

A typical practice is to standardize (or whiten) the input data. Such that we normalize the mean and stanadrd deviation of all input dimensions. Many ML models benefit from this.

The idea of batch-normalization is, why not do this standardization for each layer, or before each transformation, not only at the input. But it should not be done in the most naive way.

## Normalization via Mini-Batch statistics
- It is applied immediately before nonlinearities (ReLu or sigmoid), so on the result of x = W\*u+b
- It is applied separately per dimension/activation
- It is applied per mini-batch, not across entire dataset, for computation efficiency

**Steps** (for a mini-batch of size m, per dimension x):

- mini-batch mean: estimate mini-batch mean
$$ \mu_B = (1/m) * Sum[x_i], i=1,..,m $$
- mini-batch variance: estimate mini-batch mean
$$ \sigma^2_B = (1/m) * Sum[(x_i-\mu_B)^2], i=1,..,m $$
- normalize (scale to standard normal rv. add epsilon in denom to prevent divide by zero)
$$ x_i = (x_i - \mu_B) / \sqrt(\sigma^2_B + \epsilon)  , i=1,..,m $$
- scale and shift: allow arbitrary shift and rescaling
$$ y_i = \gamma x_i + \beta => BN_\gamma,_\beta(x_i) $$

Note, gamma and Beta parameters in last step are learned during training. They allow arbitrary linear shift and rescaling from standard normal to whatever best suits the model.

Implications of adding the batch norm:
1. The beta (shift) parameter in last step of BN replaces bias terms in the previous layer (whose output goes to BN then to nonlinearity). So we can replace (x = W\*u + b) with (x = W\*u)
2. At test time, how do you estimate the mini-batch mean and variance? What they do is during training, **they maintain a running mean of min-batch mean and variance, and this is used during test**.

### Backpropagation through Batch-Norm
In the paper, they derive and show the partial derivatives of loss by the batch norm components, and show that it is fully differentiable.

## Results (discussed in paper)
> paper from 2015 so discussion based on small older networks

With MNIST and simple network.
- **Networks train faster** and achieve similar or better accuracy with much fewer steps
- **Reducs internal covariate shift**: The distribution of inputs to the layers are stable from the start. Whereas without BN, it takes many iterations before becoming similarly stable. This is probably intuitive, because we expect that while the lower layer weights are varying, the inputs to higher layers have high variance, until earlier layers stabilise.

ImageNet classification With INCEPTION
- They showed that just adding BN allowed reaching same accuracy with less than half the iterations.
- Also, with BN, they were **able to increase learning rate from 5x to 30x**. Allowing it train with < 10x fewer iterations and reach higher accuracy. Increasing learning rate with standard inception broke it. intuitively this is because BN reduces possibility of exploding gradients.
- Also they reduced or removed dropout from inception, and substitued with regularization effect of BN.
- Also, BN made it possible to reasonably train inception with sigmoid activation instead of ReLU. This is not possible without BN. It shows normalzing input to sigmoid makes it usable and not saturate the gradients.

## Summary
- Batch Normalization is applied at the input of non-linearities, to remove "covariate shift" from internal activations. It adds two extra parameters per activation.
- Applied per training mini-batch
- Typically results in faster training of deep NNs. It allows using higher training rates, and reduces need for dropout regularization.


## References
- Papers explained [Youtube video](https://www.youtube.com/watch?v=OioFONrSETc)
- Original Paper: [Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift](https://arxiv.org/abs/1502.03167)
