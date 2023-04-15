---
layout: page
title: remove_climatology
permalink: /remove_climatology/
---

# remove_climatology

This function removes the **monthly** climatology from the provided four-dimensional xarray.DataArray. The data array must have sample coordinates convertible to pandas.Timestamp.
```
anomaly = xc.remove_climatology(
  X, 
  x_lat_dim=None, 
  x_lon_dim=None, 
  x_sample_dim=None, 
  x_feature_dim=None
):
```

`remove_climatology` will not modify the data array passed to it in-place, rather just return a copy of the original data with the **monthly** average removed. 

```
data = xr.open_dataset('example.nc').precipitation # pretend this is a 4D XCast-style data array with daily precipitation (mm/day) values in it
anom = xc.remove_climatology(data)  # remove monthly climatology
```

