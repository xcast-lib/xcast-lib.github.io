---
layout: page 
title: Preprocessing: Dictionary Learning 
permalink: /dictionarylearning/
---

# Preprocessing: Dictionary Learning 
### xc.DictionaryLearning ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/preprocessing/decomposition.py#L28)) 

This applies Scikit-Learn’s Dictionary Learning across the feature dimension of the provided xr.DataArray.

See scikit-learn’s documentation for more information about constructor arguments and settings. 
 
**Constructor**

Keyword Arguments: 
- ND (default: 1) - the number of times to repeat this estimator at each point (used for non-deterministic or stochastically initialized methods to leverage ensemble forecasts) 
- lat_chunks (default: 1) - the number of chunks into which to break the data along the latitude dimension.
- lon_chunks (default: 1) - the number of chunks into which to break the data along the longitude dimension.
- verbose (default: False) - whether or not to print the progress of the BaseEstimator methods.

**.fit** - fits the underlying PCA object at each grid point 
Arguments: 
- X: an xarray data array following the XCast dimensionality conventions, serving as predictor variables.
- Y: an xarray data array following the XCast dimensionality conventions, serving as predictand variables. Must be the same shape as X along all dimensions except the feature dimension, which can be anything (consistent with the intent of the underlying flat estimator) 

Keyword Arguments:
- rechunk (default: True): whether or not to rechunk the data using align_coords according to the lat_chunks and lon_chunks arguments provided during instantiation.
- **kwargs (accepts arbitrary other keyword arguments which are forwarded to the underlying estimator) 
- **guess_coords kwargs

Returns: 
- None

**.transform** - use a fitted transformer to produce the transformed version of an input data array
 
Arguments: 
- X: an xarray data array following the XCast dimensionality conventions, serving as predictor variables. Must be the same shape as the X used for .fit along all dimensions except the sample dimension, which can be anything

Keyword Arguments:
- rechunk (default: True): whether or not to rechunk the data using align_coords according to the lat_chunks and lon_chunks arguments provided during instantiation.
- **kwargs (accepts arbitrary other keyword arguments which are forwarded to the underlying estimator) 
- **guess_coords kwargs

Returns: 
- transformed: an Xarray DataArray with the stitched-together return values of the underlying estimators’ .transform method

guess_coords kwargs:
- x_lat_dim (default: None): the name of the latitude dimension on X
- x_lon_dim (default: None): the name of the longitude dimension on X
- x_feature_dim (default: None): the name of the feature dimension on X
- x_sample_dim (default: None): the name of the sample dimension on X
- y_lat_dim (default: None): the name of the latitude dimension on Y
- y_lon_dim (default: None): the name of the longitude dimension on Y
- y_feature_dim (default: None): the name of the feature dimension on Y
- y_sample_dim (default: None): the name of the sample dimension on Y
