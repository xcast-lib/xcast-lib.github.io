---
layout: page
title: extended_logistic_regression
permalink: /extended_logistic_regression/
---

# extended_logistic_regression

The extended_logistic_regression class is a 2D estimator which fits a univariate extended logistic regression separately between each of the predictor variables and the target variable, and then takes the average of the resulting predictions. This method is often used bias-correct individual climate models before taking their ensemble mean.
```
elr = extended_logistic_regression(
    preprocessing='minmax', # one of 'minmax' (minmax scaling), 'std' (standard anomaly scaling) or None
    thresholds=[0.2, 0.4, 0.6, 0.8], # quantiles to use for extension scheme
)
```

Once instantiated, you need to fit `elr` on two numpy-arrays, `x`, and `y` with continuous values. This implementation of ELR is currently only capable of makeing tercile probabilistic predictions and probability-of-nonexceedance predictions.

``` 
elr.fit(x, y) 
``` 

you can then make probabilistic predictions for new data like `x` (`x1`, maybe) as follows: 

```
tercile_probabilities = elr.predict_proba(x1) 
nonexceedance_30thpercentile = elr.predict_proba(x1, quantile=0.3) 
```

For more detail on the Extended Logistic Regression method, please read [Wilks, 2009.](https://rmets.onlinelibrary.wiley.com/doi/10.1002/met.134)










