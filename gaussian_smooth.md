---
layout: page
title: gaussian_smooth
permalink: /gaussian_smooth/
---

# gaussian_smooth

The gaussian_smooth functions applies NxN gaussian kernel smoothing to an xarray.DataArray. The size of the kernel is determined by the kernel keyword, and the mean and standard deviation of the gaussian kernel are calculated based on the desired kernel size. 

See [here](https://stackoverflow.com/questions/25216382/gaussian-filter-in-scipy) for more detail about how the kernel parameters are derived from the diameter

```
smoothed_data = xc.gaussian_smooth(
  X,                     # data array to apply gaussian kernel smoothing to across latitude/longitude gridpoints 
  kernel=3,              # desired diameter of the gaussian kernel 
  x_lat_dim=None, 
  x_lon_dim=None, 
  x_sample_dim=None, 
  x_feature_dim=None
)
```

`gaussian_smooth` will not modify the data array passed to it in-place, but rather return a copy of the original data array with the smoothing applied

```
data = xr.open_dataset('example.nc').precipitation # pretend this is a 4D XCast-style data array with daily precipitation (mm/day) values in it
smoothed_data = xc.gaussian_smooth(data, kernel=9) # apply 9x9 (approximately) gaussian kernel smoothing 
```

