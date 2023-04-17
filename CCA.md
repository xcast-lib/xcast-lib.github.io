---
layout: page
title: CCA
permalink: /CCA/
---

# CCA

This class represents an estimator which performs [canonical correlation analysis](https://en.wikipedia.org/wiki/Canonical_correlation) using `xcast.canonical_correlation_analysis`. 

X and Y principal component time series and loadings, as well as CCA time series and loadings (for both X and Y) are calculated using singular value decomposition and saved on the fitted CCA class as xarray.DataArrays for easy visualization / post processing.  


```
cca = xc.CCA(
  xmodes=(1, 5), 
  ymodes=(1, 5), 
  ccamodes=(1,5), 
  crossvalidation_splits='auto',
  probability_method='error_variance', 
  latitude_weighting=None,
  search_override=(None, None, None)
):
```

like `canonical_correlation_analysis`, CCA by default performs a comprehensive search across the three-dimensional space defined by the `xmodes`, `ymodes`, and `ccamodes` arguments, where each represents the minimum and maximum number of X-PCA/Y-PCA/CCA modes to retain, respectively.

If you want to explicitly pass the number of X-EOFs (PCs), Y-EOFS (PCs) and CC-Modes to retain, use the `search_override` argument, representing `(X-Modes, Y-Modes, CCA-Modes)` as a tuple of integers. Note that this must satisfy the condition `CCA-Modes <= min(X-Modes, Y-Modes)` otherwise you'll get an assertion error. Read up on CCA for the mathematical justification of this condition. 

Once instantiated, you need to fit `cca` on two numpy-arrays, `x`, and `y`: 

``` 
cca.fit(x, y) 
``` 

After fitting, the principal component and CCA scores, loadings, and singular values will be available as NumPy arrays as attributes on the `cca` object, named as follows: 

```
y_eof_scores           = cca.y_eof_scores             # PC time series for y
y_eof_loadings         = cca.y_eof_loadings           # EOFs/PC loadings for y
y_pct_variances        = cca.y_variance_explained     # Percent Variance explained by each CCA mode for y
y_pct_variances        = cca.y_variance_explained     # Percent Variance explained by each CCA mode for X
x_eof_scores           = cca.x_eof_scores             # PC time series for x
x_eof_loadings         = cca.x_eof_loadings           # EOFs/PC loadings for x
x_cca_loadings         = cca.x_cca_loadings           # CCA coefficients for the X PC time-series projected back onto the x-eof loadings 
x_cca_scores           = cca.x_cca_scores             # Time-series of CCA scores associated with X 
y_cca_loadings         = cca.y_cca_loadings           # CCA coefficients for the Y PC time-series projected back onto the y-eof loadings
y_cca_scores           = cca.y_cca_scores             # Time-series of CCA scores associated with Y
canonical_correlations = cca.canonical_correlations   # CCA values - canonical correlation between time series for each mode
```

you can then also make deterministic and probabilistic predictions for new data like `X` (`X1`, maybe) as follows: 

```
deterministic_preds = cca.predict(X1)
tercile_probabilities = cca.predict_proba(X1) 
nonexceedance_30thquantile = cca.predict_proba(X1, quantile=0.3) 
```

Pro Tip: if the standard deviation of any gridpoint in any cross validation window in Y is too close to zero, an assertionerror will be thrown. to prevent this, first apply a drymask to your data. 







