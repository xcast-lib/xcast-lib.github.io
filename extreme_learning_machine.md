---
layout: page
title: extreme_learning_machine
permalink: /extreme_learning_machine/
---

# extreme_learning_machine

This class represents a 2D estimator which fits Extreme Learning Machine (ELM) and Probabilistic Output Extreme Learning Machine (POELM) on two two-dimensional NumPy arrays, X and Y, whose first dimensions represent distinct samples and whose second dimensions represent distinct features. Both ELM and POELM proceed by instantiating a single-hidden-layer feed-forward neural network with random weights and biases, then foregoing backpropagation and fitting a Moore-Penrose Generalized Inverse between the output of the frozen hidden layer and the target vector. In order to produce tercile probabilities, the real-value target vector Y is one-hot encoded according to tercile categories delineated by its 33rd and 66th percentiles, and then transformed to log-space with the logit function. The generalized inverse is fit in log-space. Predictions are produced by applying the logistic sigmoid function to log-space generalized inverse predictions. In this implementation, both probabilistic and deterministic output layers are fit on a single shared hidden layer. This is an ensemble method, where the mean of the output of N estimators is taken. 

```
elm = extreme_learning_machine(
    activation='relu', # the activation function of the hidden layer - one of 'sigm' (sigmoid), 'tanh' (hyperbolic tangent), 'relu' (rectified linear unit), 'lin' (linear/identity function)
    hidden_layer_size=5, # integer number of nodes in the hidden layer 
    regularization=-10, # level of regularization to use - the actual value will be 2**regularization. If you want zero regularization, use None
    preprocessing='minmax', # one of 'minmax' (minmax scaling), 'std' (standard anomaly scaling) or None
    n_estimators=30,  # ensemble size
    eps=np.finfo('float').eps # epsilon for representation of one-hot encoding. since logit(1) and logit(0) are undefined, we use logit(1-eps) and logit(eps) to represent one and zero
)
```

Once instantiated, you need to fit `elm` on two numpy-arrays, `x`, and `y`. Normal ELM will be used for deterministic predictions, and Probabilistic-Output ELM will be used for probabilistic predictions.

``` 
elm.fit(x, y) 
``` 

you can then make deterministic and probabilistic predictions for new data like `x` (`x1`, maybe) as follows: 

```
deterministic_preds = elm.predict(x1)
tercile_probabilities = elm.predict_proba(x1) 
```

Note that elm cannot be used to make probability-of-nonexceedance predictions.








