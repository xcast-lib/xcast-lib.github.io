---
layout: page
title: Visualizations: Dominant Tercile
permalink: /view_probabilistic/ 
---

# Visualizations: Dominant Tercile 
### xc.view_probabilistic ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/core/visualization.py#L273) )


This function can be used to plot tercile forecasts across a map in the standard way. At each point, only the dominant tercile (the tercile with the largest probability) is plotted, and each tercile (BN, NN, or AN) is plotted with a separate colorbar. This function is necessary to replace standard xarray plotting functionality for dominant-tercile plots, and accepts only xarray dataarrays with 3 features along the feature dimension and 1 coordinate along the sample dimension.

Returns: 
- None 

Arguments: 
- X: an xarray data array following the XCast dimensionality conventions, with only 3 features along the feature dimension and 1 sample along the sample dimension (i.e., pick a given year to plot the forecast from, one at a time) 

Keyword Arguments:
- loc: location to place legend - same as pyplot.legend()’s loc argument. 
	
guess_coords kwargs:
- x_lat_dim (default: None): the name of the latitude dimension on X
- x_lon_dim (default: None): the name of the longitude dimension on X
- x_feature_dim (default: None): the name of the feature dimension on X
- x_sample_dim (default: None): the name of the sample dimension on X

