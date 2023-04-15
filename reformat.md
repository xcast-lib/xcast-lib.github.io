---
layout: page
title: reformat
permalink: /reformat/
---

# reformat

reformat standardizes the format of climate model data by converting longitude coordinates to the domain [-180,180] and sorting by latitude and longitude. You'd be surprised how useful this can be.

```
reformated = xc.reformat(
  X, 
  x_lat_dim=None, 
  x_lon_dim=None, 
  x_sample_dim=None, 
  x_feature_dim=None
):
```

`reformat` will not modify the data array passed to it in-place, rather just return a copy of the original data the changes applied.

```
data = xr.open_dataset('example.nc').precipitation # pretend this is a 4D XCast-style data array with longitude values 0-360
reformatted = xc.reformat(data)  #  converted longitude values to [-180, 180]
```

