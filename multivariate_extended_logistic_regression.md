---
layout: page
title: multivariate_extended_logistic_regression
permalink: /extended_logistic_regression/
---

# multivariate_extended_logistic_regression

This class is an estimator which implements Multivariate Extended Logistic Regression. Multivariate Extended Logistic regression fits a standard multivariate logistic regression on an augmented dataset.  For full detail on the Extended Logistic Regression method, please read [Wilks, 2009.](https://rmets.onlinelibrary.wiley.com/doi/10.1002/met.134)

In a nutshell, however, MELR will take your X and Y arrays, double them, encode the output according to each samples membership in a distinct category defined by their nonexceedance of the 33rd and 67th percentiles of Y, and add an additional independent variable indicating the threshold by which the target variable is defined. Please read the paper for a full explanation.
The difference between MELR and ELR is that ELR will fit a multivariate logistic regression (note: not extended) for each of the independent variables, **separately**, whereas MELR will fit one multivariate logistic regression for all of them at once. 

```
melr = multivariate_extended_logistic_regression(
    preprocessing='minmax', # one of 'minmax' (minmax scaling), 'std' (standard anomaly scaling) or None
    thresholds=[0.2, 0.4, 0.6, 0.8], # quantiles to use for extension scheme
)
```

Once instantiated, you need to fit `melr` on two numpy-arrays, `x`, and `y` with continuous values. This implementation of MELR is currently only capable of making tercile probabilistic predictions and probability-of-nonexceedance predictions.

``` 
melr.fit(x, y) 
``` 

you can then make probabilistic predictions for new data like `x` (`x1`, maybe) as follows: 

```
tercile_probabilities = elr.predict_proba(x1) 
nonexceedance_30thpercentile = elr.predict_proba(x1, quantile=0.3) 
```











