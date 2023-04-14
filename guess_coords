---
layout: page
title: guess_coords
permalink: /guess_coords/
---

# guess_coords

This function attempts to determine which dimensions/coordinates on an xarray.DataArray correspond to latitude/longitude/sample/feature by detecting commonly used names. This cannot be guaranteed to work perfectly in every case, so to be certain the correct dimensions are being assigned, pass the x_lat_dim, x_lon_dim, x_sample_dim, and x_feature_dim arguments to any XCast function or class method explicitly.

```
x_lat_dim, x_lon_dim, x_sample_dim, x_feature_dim = guess_coords(X, x_lat_dim=None, x_lon_dim=None, x_sample_dim=None, x_feature_dim=None)
```

If the xarray.DataArray passed to `guess_coords` as `X` is not four-dimensional, this function will print warning messages about being unable to find the dimensions it deems to be missing. Additionally, if the names of any of the dimensions on the DataArray cannot be assigned to a dimension XCast is looking for, it will print a warning message about being unable to assign those labels to a dimension. See [here](https://xcast-lib.github.io/data/) for more detail on the dimensionality XCast expects. 

If you find that XCast cannot automatically assign the labels of the dimensions on your xarray.DataArrays, you can manually pass the `x_lat_dim=None, x_lon_dim=None, x_sample_dim=None, x_feature_dim=None` arguments on any XCast function/class method.  However if you pass one of these arguments, and whatever you pass is not the name of a dimension on the Data Array passed, you'll get an assertion error.

The names that can be automatically detected by XCast include: 

```
often_used = { 
	'longitude': ['LONGITUDE', 'LONG', 'X', 'LON'],
	'latitude': ['LATITUDE', 'LAT', 'LATI', 'Y'],
	'sample': ['T', 'S', 'TIME', 'SAMPLES', 'SAMPLE', 'INITIALIZATION', 'INIT','D', 'DATE', "TARGET", 'YEAR', 'I', 'N'],
	'feature': ['M', 'MODE', 'FEATURES', 'F', 'REALIZATION', 'MEMBER', 'Z', 'C', 'CAT', 'NUMBER', 'V', 'VARIABLE', 'VAR', 'P', 'LEVEL'],
}
```
