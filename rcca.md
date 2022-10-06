---
layout: page 
title: Regressors: Canonical Correlation Analysis
permalink: /cca/ 
--- 

# Regressors: Canonical Correlation Analysis
### xc.CCA ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/preprocessing/cca.py#L11))

The CCA regressor method uses a combination of Principal Components Analysis and Canonical Correlation Analysis to produce a regression model that can be fine-tuned by adjusting both the spatial domain and the number of PCA & CCA modes retained. It proceeds by first weighting the X Data Array by the cosine of the latitude coordinate, then stacking all latitude and longitude points along one axis and using PCA to reduce the dimensionality. It then does the same process to the Y Data Array - latitude weighting and then PCA reduction. Once time series of both X PCA scores and Y PCA scores have been found, CCA is fit between the two and used to construct a regression model. 

The prediction step proceeds by applying latitude weighting, using the fitted X PCA transformer to transform X Data into a time series of PCA scores, applying the regression model from CCA, and then using the Y PCA transformer to invert the transformation from Y PCA time series scores into a full-field Y Data Array, the predictions. This method is not implemented with BaseEstimator.

**Constructor**: 
Keyword Arguments: 
- xmodes (default:5) - the number of PCA modes to retain when transforming X
- ymodes (default:5) - the number of PCA modes to retain when transforming Y 
- ccamodes (default:5) - the number of CCA modes to retain during CCA
- x_preprocessing (default: 'stdanomaly') - preprocessing scheme for X
- y_preprocessing (default: 'stdanomaly') - preprocessing scheme for Y
- latitude_weighting (default: True) - whether or not to apply latitude weighting to X and Y. 



**.fit** - fits the CCA estimator
Arguments: 
- X: an xarray data array following the XCast dimensionality conventions, serving as predictor variables.
- Y: an xarray data array following the XCast dimensionality conventions, serving as predictand variables. Does not have to be the same shape as X along any dimension except the sample dimension.  

Keyword Arguments:
- **guess_coords kwargs
	
Returns: 
- None

Post-Fit CCA Instance Attributes: 
- CCA.ccax_loadings - xr.DataArray storing CCA Spatial Loadings for the X data 
- CCA.ccay_loadings - xr.DataArray storing CCA Spatial Loadings for the Y data 
- CCA.ccax_scores - xr.DataArray storing CCA Time Series scores for X 
- CCA.ccay_scores - xr.DataArray storing CCA Time Series scores for Y 
- CCA.eofx_loadings - xr.DataArray storing EOF Spatial Loadings for the X data 
- CCA.eofy_loadings - xr.DataArray storing EOF Spatial Loadings for the Y data 
- CCA.eofx_scores - xr.DataArray storing EOF Time Series scores for X 
- CCA.eofy_scores - xr.DataArray storing EOF Time Series scores for Y 

**.predict** - produces a prediction based on the new x input data according to the fitted underlying estimator. Can be either a category (1, 2, 3… etc) or continuous values. 
 
Arguments: 
- X: an xarray data array following the XCast dimensionality conventions, serving as predictor variables. Must be the same shape as the X used for .fit along all dimensions except the sample dimension, which can be anything

Keyword Arguments:
- **guess_coords kwargs

Returns: 
- preds: an Xarray DataArray 
