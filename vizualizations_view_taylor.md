---
layout: page
title: Visualizations: Taylor Diagram
permalink: /view_taylor/
---

# Visualizations: Taylor Diagram
### xc.view_taylor ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/core/visualization.py#L190
)) 

this function plots a “Taylor Diagram” representing the contents of the provided X and Y datasets. A taylor diagram shows the level of consistency of several variables in comparison to a single baseline variable by plotting the RMSE between each variable and the baseline, the standard deviations of each, and the level of correlation between each variable and the baseline. 



The plot is defined by using two sets of concentric rings to represent the standard deviation of the data, and the Root Mean Squared Error (RMSE) between each variable and the baseline. The rings representing Std. Dev are centered at the bottom left hand corner of the plot (the origin), with progressively larger and larger rings emanating outward, the distance to the origin representing the standard deviation of each variable, including the baseline. The rings representing the RMSE between the baseline and each variable are centered at the point representing the baseline on the x-axis, with the distance between the points being proportional to the magnitude of the RMSE. 



Correlations values are then plotted along a radial axis, denoted by lines extending out from the origin at angles which represent, proportionally, the correlation between a point on that line and the baseline.


Returns: 
- None

Arguments: 
- X: an xarray data array following the XCast dimensionality conventions, serving as dependent variables to be compared to the baseline.
- Y: an xarray data array following the XCast dimensionality conventions, serving as the baseline variable for the taylor diagram.

Keyword Arguments:
- loc: location to place legend - same as pyplot.legend()’s loc argument. 
	
guess_coords kwargs:
- x_lat_dim (default: None): the name of the latitude dimension on X
- x_lon_dim (default: None): the name of the longitude dimension on X
- x_feature_dim (default: None): the name of the feature dimension on X
- x_sample_dim (default: None): the name of the sample dimension on X
- y_lat_dim (default: None): the name of the latitude dimension on Y
- y_lon_dim (default: None): the name of the longitude dimension on Y
- y_feature_dim (default: None): the name of the feature dimension on Y
- y_sample_dim (default: None): the name of the sample dimension on Y

