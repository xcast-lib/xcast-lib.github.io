---
layout: page
title: Utilities: guess_coords
permalink: /guess_coords/
---

# Utilities: guess_coords

### xc.guess_coords( ... )  ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/core/utilities.py#L11))

This function is used internally to automatically determine which dimension on an xarray data array corresponds to which dimension within the xcast dimensionality convention. It allows xcast to accommodate data from any source, and gives the user the option to provide a mapping from xcast’s naming conventions to their data array’s.



Within the call to any XCast function or method, you can specify the ‘x_lat_dim’, ‘x_lon_dim’, ‘x_sample_dim’, ‘x_feature_dim’ keyword arguments, (or any subset of them, and xcast will try to guess the rest), to tell xcast what the name of the corresponding dimension on your data is. ‘x_...’ keyword arguments refer to the first positional argument of a given function, and ‘y_...’ keyword arguments refer to the second, if there. 



Please see ‘XCast Dimensionality Conventions’ for more detail on what each dimension of the data is intended to represent. guess_coords will search for dimensions on the data with names like the following: 

```
common_x = ['LONGITUDE', 'LONG', 'X', 'LON']
common_y = ['LATITUDE', 'LAT', 'LATI', 'Y']
common_t = ['T', 'S', 'TIME', 'SAMPLES', 'SAMPLE', 'INITIALIZATION', 'INIT', "TARGET"]
common_m = ['M', 'FEATURES', 'F', 'REALIZATION', 'MEMBER', 'Z', 'C', 'CAT']
```

So if your dataset’s naming conventions fall outside of that, please be aware that you’ll need to specify the names, or rename them. 

Returns: 
-	Lat: string name of latitude dimension on X
-	Lon: string name of longitude dimension on X
-	Sample: string name of sample dimension on X
-	Feature: string name of feature dimension on X

Arguments: 
- X: an xarray data array following the XCast dimensionality conventions

Keyword Arguments:
- x_lat_dim (default: None): the name of the latitude dimension on X
-	x_lon_dim (default: None): the name of the longitude dimension on X
-	x_feature_dim (default: None): the name of the feature dimension on X
-	x_sample_dim (default: None): the name of the sample dimension on X

