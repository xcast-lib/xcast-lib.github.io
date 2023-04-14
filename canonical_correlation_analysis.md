---
layout: page
title: canonical_correlation_analysis
permalink: /canonical_correlation_analysis/
---

# canonical_correlation_analysis

This class represents an estimator which performs [canonical correlation analysis](https://en.wikipedia.org/wiki/Canonical_correlation) under K-Fold cross validation in order to provide the capacity for probabilistic predictions. The cross-validated error variance is used to represent the variance of prediction residuals, which are assumed to be gaussian. Once the error variance is determined under cross validation, CCA is applied to the whole dataset provided. X and Y principal component time series and loadings, as well as CCA time series and loadings (for both X and Y) are calculated using singular value decomposition.  

This class accepts two two-dimensional NumPy arrays, X and Y, whose first dimension represents distinct samples and whose second dimension represents distinct features (gridpoints). This is used internally by `xc.CCA` to perform CCA on two xarray.DataArrays, but you can also use it separately with NumPy arrays if you want.

```
cca = canonical_correlation_analysis(xmodes=(1, 5), ymodes=(1, 5), ccamodes=(1,5), crossvalidation_splits=5, probability_method='error_variance', latitude_weights_x=None, latitude_weights_y=None, search_override=(None, None, None))
```

`canonical_correlation_analysis` by default performs a comprehensive search across the three-dimensional space defined by the `xmodes`, `ymodes`, and `ccamodes` arguments, where each represents the minimum and maximum number of X-PCA/Y-PCA/CCA modes to retain, respectively.

If you want to explicitly pass the number of X-EOFs (PCs), Y-EOFS (PCs) and CC-Modes to retain, use the `search_override` argument, representing `(X-Modes, Y-Modes, CCA-Modes)` as a tuple of integers. Note that this must satisfy the condition `CCA-Modes <= min(X-Modes, Y-Modes)` otherwise you'll get an assertion error. Read up on CCA for the mathematical justification of this condition. 

Once instantiated, you need to fit `cca` on two numpy-arrays, `x`, and `y`: 

``` 
cca.fit(x, y) 
``` 

After fitting, the principal component and CCA scores, loadings, and singular values will be available as NumPy arrays as attributes on the `cca` object, named as follows: 

```
y_eof_scores           = cca.y_eof_scores             # PC time series for y
y_eof_loadings         = cca.y_eof_loadings           # EOFs/PC loadings for y
y_eof_singular_values  = cca.y_eof_singular_values    # PCA Singular Values for y
y_pct_variances        = cca.y_pct_variances          # Percent Variance explained by each mode for y
x_eof_scores           = cca.x_eof_scores             # PC time series for x
x_eof_loadings         = cca.x_eof_loadings           # EOFs/PC loadings for x
x_eof_singular_values  = cca.x_eof_singular_values    # PCA Singular Values for x
x_pct_variances        = cca.x_pct_variances          # Percent Variance explained by each mode for x
x_cca_loadings         = cca.x_cca_loadings           # CCA coefficients for the X PC time-series projected back onto the x-eof loadings 
x_cca_scores           = cca.x_cca_scores             # Time-series of CCA scores associated with X 
y_cca_loadings         = cca.y_cca_loadings           # CCA coefficients for the Y PC time-series projected back onto the y-eof loadings
y_cca_scores           = cca.y_cca_scores             # Time-series of CCA scores associated with Y
canonical_correlations = cca.canonical_correlations   # CCA values - canonical correlation between time series for each mode
cca_u                  = cca.cca_u                    # CCA coefficients for the X PC time-series (to transform to CCA time-series) 
cca_vt                 = cca.cca_vt                   # CCA coefficients for the Y PC time-series (to transform to CCA time-series) 
```

you can then also make deterministic and probabilistic predictions for new data like `x` (`x1`, maybe) as follows: 

```
deterministic_preds = cca.predict(x1)
tercile_probabilities = cca.predict_proba(x1) 
nonexceedance_30thquantile = cca.predict_proba(x1, quantile=0.3) 
```








