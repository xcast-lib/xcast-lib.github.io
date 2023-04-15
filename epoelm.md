---
layout: page
title: epoelm
permalink: /epoelm/
---

# epoelm

This class represents an estimator which fits Extended Probabilistic Output Extreme Learning Machine (EPOELM) between two two-dimensional NumPy arrays, X and Y, whose first dimensions represent distinct samples and whose second dimensions represent distinct features. EPO-ELM proceeds by creating a single-hidden-layer feed-forward neural network with random weights and biases, which foregoes traing through backpropagation and fits a generalized Moore-Penrose inverse between a target vector and hidden-layer-output vector which have both been extended according to the Extended Logistic Regression procedure. This allows EPO-ELM to directly produce full conditional probability distributions with the logistic sigmoid function. A single EPO-ELM can be considered to be fitting conditional logistic distributions, but since EPO-ELM is an ensemble method, the predictive distributions are usually quite non-parametric looking. 
```
epoelm = epoelm(
    activation='relu', # the activation function of the hidden layer - one of 'sigm' (sigmoid), 'tanh' (hyperbolic tangent), 'relu' (rectified linear unit), 'lin' (linear/identity function)
    hidden_layer_size=5, # integer number of nodes in the hidden layer 
    regularization=-10, # level of regularization to use - the actual value will be 2**regularization. If you want zero regularization, use None
    preprocessing='minmax', # one of 'minmax' (minmax scaling), 'std' (standard anomaly scaling) or None
    n_estimators=30,  # ensemble size
    eps=np.finfo('float').eps # epsilon for representation of one-hot encoding. since logit(1) and logit(0) are undefined, we use logit(1-eps) and logit(eps) to represent one and zero
    encoding='nonexceedance', # method of encoding target vector - one of 'binary' (standard one-hot encoding) or 'nonexceedance' (anomaly regression) 
    initialization='normal', # weight initialization scheme - one of 'normal' (gaussian normal dist), 'uniform' (uniform dist) or 'xavier'
    quantiles=[0.2, 0.4, 0.6, 0.8], # quantiles to use for extension scheme
    standardize_y=False # whether or not to apply standard anomaly scaling to Y
)
```

Once instantiated, you need to fit `epoelm` on two numpy-arrays, `x`, and `y`. Normal ELM will be used for deterministic predictions, and Probabilistic-Output ELM will be used for probabilistic predictions.

``` 
epoelm.fit(x, y) 
``` 

you can then make deterministic and probabilistic predictions for new data like `x` (`x1`, maybe) as follows: 

```
deterministic_preds = epoelm.predict(x1)
tercile_probabilities = epoelm.predict_proba(x1) 
nonexceedance_30thpercentile = epoelm.predict_proba(x1, quantile=0.3) 

```









