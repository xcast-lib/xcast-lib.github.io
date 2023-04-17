---
layout: page
title: PCR
permalink: /PCR/
---

# PCR

This class represents an estimator which performs [Principal Components Regression](https://en.wikipedia.org/wiki/Principal_component_regression) using `xcast.linear_regression` and `xcast.EOF` in concert.

X  principal component time series and loadings are calculated using singular value decomposition and saved on the fitted PCR class as xarray.DataArrays for easy visualization / post processing. `linear_regression` is then fit between the PC time-series and each of the individual gridpoints on Y.   


```
pcr = xc.PCR(
  eof_modes=None,  # integer number of EOF modes to use - if none, use min(n_samples, m_features) 
  latitude_weighting=False,  # latitude weighting? yes or no
  separate_members=True,  # whether or not to calculate principal components of X features jointly (stacking them all as equally weighted features) or separately.
  crossvalidation_splits=5, # number of splits to use for K-Fold cross validation
):
```

Once instantiated, you need to fit `pcr` on two numpy-arrays, `x`, and `y`: 

``` 
pcr.fit(x, y) 
``` 

After fitting, the principal component scores, loadings, and singular values will be available as xarray.DataArrays as attributes on the `pcr` object, named as follows: 

```
x_eof_scores           = pcr.eof_scores             # PC time series for x
x_eof_loadings         = pcr.eof_loadings           # EOFs/PC loadings for x
x_eof_variance_explained = pcr.eof_variance_explained # percent of variance explained by each X EOF mode
```
you can then also make deterministic and probabilistic predictions for new data like `X` (`X1`, maybe) as follows: 

```
deterministic_preds = pcr.predict(X1)
tercile_probabilities = pcr.predict_proba(X1) 
nonexceedance_30thquantile = pcr.predict_proba(X1, quantile=0.3) 
```

Pro Tip: if the standard deviation of any gridpoint in any cross validation window in X is too close to zero, an assertionerror will be thrown. to prevent this, first apply a drymask to your data. 







