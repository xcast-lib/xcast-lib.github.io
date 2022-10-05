---
layout: page
title: Utilities: align_chunks
permalink: /align_chunks/
---

this function modifies the latitude/longitude chunking scheme of two xarray dataarrays, such that the geographical regions represented  by each chunk in either array are consistent between them. The geographical boundaries of each data array should be consistent to start with, since xcast operates based on indices, not on coordinates. (I.e., XCast does not look at the latitude / longitude coordinates of the data it’s been given - it just checks that there are the same number of points in each one) This will, however, enable you to do tricky teleconnection-based forecasting if you can set up the data arrays correctly. 


This function is necessary only to enable high-performance during XCast cross-validation. By default, XCast estimators already do rechunking every time- but rechunking is an expensive operation, and performance can be increased by moving the rechunking outside of cross-validation (and thereby not repeating work unnecessarily) 


In that case, this function should be applied to the X and Y datasets before the cross validation loop begins, and then the rechunk keyword arguments within the instantiation/fit/predict code should be set to False. 

Returns: 
- X1: rechunked version of X 
- Y1: rechunked version of Y

Arguments: 
- X: an xarray data array following the XCast dimensionality conventions
- Y: an xarray data array following the XCast dimensionality conventions

Keyword Arguments:
- lat_chunks (default: 5): integer number of chunks into which to split these datasets across the latitude dimension
-	lon_chunks (default: 5): integer number of chunks into which to split these datasets across the longitude dimension
	
guess_coords kwargs:
- x_lat_dim (default: None): the name of the latitude dimension on X
- x_lon_dim (default: None): the name of the longitude dimension on X
-	x_feature_dim (default: None): the name of the feature dimension on X
-	x_sample_dim (default: None): the name of the sample dimension on X
-	y_lat_dim (default: None): the name of the latitude dimension on Y
-	y_lon_dim (default: None): the name of the longitude dimension on Y
-	y_feature_dim (default: None): the name of the feature dimension on Y
-	y_sample_dim (default: None): the name of the sample dimension on Y

[source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/core/chunking.py#L4)
