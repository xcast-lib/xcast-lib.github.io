---
layout: page 
title: Preprocessing: Drymask 
permalink: /drymask/ 
---

# Preprocessing: Drymask 
### xc.drymask ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/preprocessing/onehot.py#L7))

This is a preprocessing function which creates a “dry-mask” - a 2D map data array by which the original data can be multiplied, to transform all the lat/lon points that are climatologically ‘too dry’ to NaN values. 

It proceeds by using the  `quantile` function to calculate a quantile threshold. (usually, the 10th or 30th percentile) It then takes all of the gridpoints where this threshold is less than a certain value (specified by the user - usually very small like 0.0001 or something), and transforms them to NaNs. Other grid points are set to 1. This data array can then be multiplied by the original data, to ‘mask out’ all of the ‘too-dry’ regions. 

Note that this is logically equivalent to masking “places where more than x% of the samples are zero are ‘too-dry’” 

Arguments: 
- X: the Xarray DataArray to be masked - must conform to xcast dimensionality conventions

Keyword Arguments: 
- dry_threshold (default:0.001) - the real-value threshold defining ‘too-dry’
- quantile_threshold (default:0.33) - the quantile threshold to check against the dry_threhold
- method (default:'midpoint') - this is passed to the quantile function, see np.quantile for more information.
