---
layout: page
title: Preprocessing: Regridding
permalink: /regrid/ 
---

# Preprocessing: Regridding
### xc.regrid ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/preprocessing/spatial.py#L14)) 

`regrid` implements two-dimensional interpolation, commonly known as ‘regridding’ in the geosciences community. This implementation uses SciPy’s Interp2D as a framework. Essentially, a separate interpolation function is fit at each step across the sample and feature dimensions of a data array, and used to produce a ‘regridded’ dataset having a new user-specified spatial resolution. 

**Arguments**
- X: an Xarray DataArray following the xcast dimensionality conventions
- lons: a 1D numpy array specifying the new longitude coordinates desired.
- lats: a 1D numpy array specifying the new latitude coordinates desired. 

*Note that lons, and lats, should probably be within the spatial subregion spanned by X’s original coordinates. Regrid will do extrapolation, but you almost definitely don’t want that. 

**Keyword Arguments**
- kind (default: ‘linear’) - argument to be passed to SciPy’s Interp2D specifying the kind of interpolation. Can be ‘linear’, ‘quadratic’, ‘cubic’, etc. 
- **guess coords kwargs 

**Returns**
- X2: regridded dataarray on new lat/lon grids. 
