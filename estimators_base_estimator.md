---
layout: page
title: Estimators: BaseEstimator
permalink: /BaseEstimator/ 
---
# Estimators: BaseEstimator 
### xc.BaseEstimator ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/estimators/base_estimator.py#L119
)) 

BaseEstimator is the driving functionality behind all of XCast’s estimators and transformers- they are all, with few exceptions, implemented as subclasses of BaseEstimator. 



BaseEstimator implements four core methods- .fit, .predict, .predict_proba, and .transform. Estimators use the .fit, .predict, and .predict_proba, while transformers make use of .fit and .transform. 


The core idea of BaseEstimator is that it is a wrapper for an underlying “flat” estimator - estimators that operate on two-dimensional numpy arrays, rather than high dimensional xarray data arrays, like those of SciKit-Learn. BaseEstimator takes the four dimensional Xarray DataArray, and splits it up into (N Latitudes) x (M Longitudes) grid points, creating NxM two-dimensional datasets, representing the data from each gridpoint. It then applies the .fit method of the underlying statistical/machine learning class, and saves a copy of that flat estimator for each gridpoint. 


During .predict/.predict_proba/.transform, BaseEstimator applies the corresponding .predict/.predict_proba/.transform method of the underlying fitted flat estimator at each grid point, and then re-assembles the results from all of the grid points into a new Xarray DataArray of the proper dimensionality, and returns it. 


This is all accomplished using Dask’s chunk-wise parallelism to dispatch wrapper functions like apply_fit_to_block, apply_predict_to_block, etc, which implement manual for-loop iteration over each grid point within the block they’ve been given. The size of the chunk can be used to control the level of parallelism with, theoretically, smaller chunks meaning more parallelism. Practically, this is limited by the number of cores on your machine. Please read the XCast paper in Frontiers in Climate for more detail. 


Note that during .fit, .predict, .transform, and .predict_proba, extraneous/unexpected keyword arguments are passed on to the underlying flat estimators .fit/.predict/.predict_proba/.transform methods and then are used normally. 


**Constructor**

Keyword Arguments: 
- ND (default: 1) - the number of times to repeat this estimator at each point (used for non-deterministic or stochastically initialized methods to leverage ensemble forecasts) 
- lat_chunks (default: 1) - the number of chunks into which to break the data along the latitude dimension.
- lon_chunks (default: 1) - the number of chunks into which to break the data along the longitude dimension.
- verbose (default: False) - whether or not to print the progress of the BaseEstimator methods.

**.fit** - fits the underlying flat estimator at each grid point 
Arguments: 
- X: an xarray data array following the XCast dimensionality conventions, serving as predictor variables.
- Y: an xarray data array following the XCast dimensionality conventions, serving as predictand variables. Must be the same shape as X along all dimensions except the feature dimension, which can be anything (consistent with the intent of the underlying flat estimator) 

Keyword Arguments:
- rechunk (default: True): whether or not to rechunk the data using align_coords according to the lat_chunks and lon_chunks arguments provided during instantiation.
- **kwargs (accepts arbitrary other keyword arguments which are forwarded to the underlying estimator) 
- **guess_coords kwargs
	
Returns: 
- None

**.predict** - produces a prediction based on the new x input data according to the fitted underlying estimator. Can be either a category (1, 2, 3… etc) or continuous values. 
 
Arguments: 
- X: an xarray data array following the XCast dimensionality conventions, serving as predictor variables. Must be the same shape as the X used for .fit along all dimensions except the sample dimension, which can be anything

Keyword Arguments:
- rechunk (default: True): whether or not to rechunk the data using align_coords according to the lat_chunks and lon_chunks arguments provided during instantiation.
- **kwargs (accepts arbitrary other keyword arguments which are forwarded to the underlying estimator) 
- **guess_coords kwargs

Returns: 
- preds: an Xarray DataArray with the stitched-together return values of the underlying estimators’ .predict method

**.predict_proba** - use a fitted estimator to make probability forecasts for each feature on the input target vector. Behaves differently (one-vs-rest, or categorical) depending on the underlying estimator type. 

Arguments: 
- X: an xarray data array following the XCast dimensionality conventions, serving as predictor variables. Must be the same shape as the X used for .fit along all dimensions except the sample dimension, which can be anything

Keyword Arguments:
- rechunk (default: True): whether or not to rechunk the data using align_coords according to the lat_chunks and lon_chunks arguments provided during instantiation.
	**kwargs (accepts arbitrary other keyword arguments which are forwarded to the underlying estimator) 
	**guess_coords kwargs

Returns: 
- preds: an Xarray DataArray with the stitched-together return values of the underlying estimators’ .predict_proba method

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

