--- 
layout: page 
title: Preprocessing: Quantile
permalink: /quantile/ 
---

# Preprocessing: Quantile
### xc.quantile ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/preprocessing/onehot.py#L19)) 

This is a preprocessing function which calculates a given quantile of the data. It’s basically xr.quantile, but a little more robust 

Arguments: 
- X: the Xarray DataArray to be masked - must conform to xcast dimensionality conventions
- threshold: the quantile to be calculated (between 0 and 1) 

Keyword Arguments: 
- method (default:'midpoint') - this is passed to the quantile function, see np.quantile for more information.
