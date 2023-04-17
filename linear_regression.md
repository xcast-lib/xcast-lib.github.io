---
layout: page
title: linear_regression
permalink: /linear_regression/
---

# linear_regression

This class represents an estimator which performs multiple linear regression under K-Fold cross validation in order to provide the capacity for probabilistic predictions. The cross-validated error variance is used to represent the variance of prediction residuals, which are assumed to be gaussian. Once the error variance is determined under cross validation, MLR is applied to the whole dataset provided. 

This class accepts two two-dimensional NumPy arrays, X and Y, whose first dimension represents distinct samples and whose second dimension represents distinct features (gridpoints). This is used internally by `xc.MLR` to perform linear_regression on two xarray.DataArrays, but you can also use it separately with NumPy arrays if you want.

```
mlr = xc.linear_regression(
  fit_intercept=True,  # whether or not to fit an intercept 
  crossvalsplits=5,    # how many splits to use for cross validation
  probability_method='error_variance'  # one of 'error_variance' or 'adjusted_error_variance' 
)
```

Once instantiated, you need to fit `mlr` on two numpy-arrays, `x`, and `y`: 

``` 
mlr.fit(x, y) 
``` 

you can then make deterministic and probabilistic predictions for new data like `x` (`x1`, maybe) as follows: 

```
deterministic_preds = mlr.predict(x1)
tercile_probabilities = mlr.predict_proba(x1) 
nonexceedance_30thquantile = mlr.predict_proba(x1, quantile=0.3) 
```








