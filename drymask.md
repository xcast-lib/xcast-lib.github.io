---
layout: page
title: drymask
permalink: /drymask/
---

# drymask

The drymask function is used to detect gridpoints within an xarray.DataArray which fail to satisfy certain conditions, and produce a mask which can be used to remove those gridpoints from computation. This function can detect gridpoints whose mean values fall below the user provided dry_threshold, or gridpoints whose Nth percentile falls below the user-provided dry_threshold. Only gridpoints whose mean or Nth percentile along the sample dimension are greater than or equal to the dry_threshold will be kept, and all others will be removed. For example, if you want to mask out points where seasonal precipitation is less than 5mm for no more than 30% of the available samples, you would pass dry_threshold=5 and quantile_threshold=0.3. 

```
drymask = xc.drymask(
  X, 
  dry_threshold=0.001, # definition of 'dry' - anything less than this value will count as a 'dry' sample. any numeric value is valid
  quantile_threshold=0.33,  # quantile defining the maximum number of samples allowed to be dry- if this value is 0.33, then no more than 33% of the samples can be dry. If any more are, they will be masked out. between (0,1) exclusive. 
  method='quantile',  # whether to use the quantile threshold defined above, or the mean along the data array's sample dimension as the condition for masking
  x_lat_dim=None, 
  x_lon_dim=None, 
  x_sample_dim=None, 
  x_feature_dim=None
):
```

`drymask` will not modify the data array passed to it in-place, just create a mask array with the value 1 over non-dry gridpoints and NaN over dry gridpoints. In order to apply the masking, you should multiply the original array by the mask: 

```
data = xr.open_dataset('example.nc').precipitation # pretend this is a 4D XCast-style data array with daily precipitation (mm/day) values in it
mask = xc.drymask(data, dry_threshold=5, quantile_threshold=0.1) # create a mask removing gridpoints where 10% or more of the data points have < 5 mm/day precipitation
masked_data = data * mask # apply mask to the data
```

