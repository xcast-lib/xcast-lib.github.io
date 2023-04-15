---
layout: page
title: percentile
permalink: /percentile/
---

# percentile

The percentile function transforms an xarray.DataArray from real-values to the corresponding percentiles along the sample dimension, by ranking them, dividing by the number of samples, and then removing/adding epsilon to values of 1/0. 

```
percentiles = xc.percentile(
  X,                     # data array to apply gaussian kernel smoothing to across latitude/longitude gridpoints 
  x_lat_dim=None, 
  x_lon_dim=None, 
  x_sample_dim=None, 
  x_feature_dim=None
)
```

`percentile` will not modify the data array passed to it in-place, but rather return a copy of the original data array with the ranking applied. 

```
data = xr.open_dataset('example.nc').precipitation # pretend this is a 4D XCast-style data array with daily precipitation (mm/day) values in it
percentile_data = xc.percentile(data) 
```

