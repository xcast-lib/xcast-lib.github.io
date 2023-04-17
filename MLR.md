---
layout: page
title: MLR
permalink: /MLR/
---

# MLR

This class represents an estimator which performs [Multiple Linear Regression]([https://en.wikipedia.org/wiki/Principal_component_regression](https://en.wikipedia.org/wiki/Linear_regression)) using `xcast.linear_regression`. 

As in `linear_regression`, the cross-validated error variance is used to produce predictive probability distributions under gaussian assumptions.

Once instantiated, you need to fit `mlr` on two numpy-arrays, `x`, and `y`: 

``` 
mlr.fit(x, y) 
``` 

you can then also make deterministic and probabilistic predictions for new data like `X` (`X1`, maybe) as follows: 

```
deterministic_preds = mlr.predict(X1)
tercile_probabilities = mlr.predict_proba(X1) 
nonexceedance_30thquantile = mlr.predict_proba(X1, quantile=0.3) 
```

Pro Tip: if the standard deviation of any gridpoint in any cross validation window in X is too close to zero, an assertionerror will be thrown. to prevent this, first apply a drymask to your data. 







