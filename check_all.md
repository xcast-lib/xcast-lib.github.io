---
layout: page
title: check_all
permalink: /check_all/ 
---

This function checks that an xarray.DataArray conforms to the expected format for XCast. With few exceptions, any xarray.DataArray used with XCast must be four-dimensional, with the dimensions representing latitude, longitude, samples and features respectively. Each dimension must have a corresponding coordinate of the same size as that dimension. For even more detail, look [here](https://xcast-lib.github.io/data/)

This is mostly an internal function for the sake of validating the assumptions made by XCast and throwing assertion errors if they are violated. You probably don't have to be using this unless you're contributing to XCast. 

```
check_all(X, x_lat_dim, x_lon_dim, x_sample_dim, x_feature_dim)
```
