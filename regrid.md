---
layout: page
title: regrid
permalink: /regrid/
---

# regrid

The regrid function uses Bivariate Spline interpolation (see: SciPy) to regrid an xarray.DataArray to a new resolution along its latitude/longitude dimensions. Note that the new coordinates onto which to regrid the xarray.DataArray should be ordered the same as the original lat/long coordinates on the data array, and should cover either the same geographical extent or a subset. Also be advised that you'll need to make sure that the longitude coordinates match (if the orignal longitude coordinate is 0-360, the one to which to regrid the data should also be 0-360. If they are -180 to 180, thats fine too but make sure they match).  

```
X = xc.regrid(
  X,                     # the 4D data array to regrid 
  lons,                  # the new longitude grid coordinates to regrid to - either a numpy array, or an xarray data array with 1 dimension
  lats,                  # the new latitude grid coordinates to regrid to - either a numpy array, or an xarray data array with 1 dimension
  x_lat_dim=None, 
  x_lon_dim=None, 
  x_sample_dim=None, 
  x_feature_dim=None
):
```

`regrid` will not modify the data array passed to it in-place, but rather return a copy of the original data array with the regridding applied independently at each sample/feature. 

```
data = xr.open_dataset('example.nc').precipitation    # pretend this is a 1degree x 1degreed 4D XCast-style data array with daily precipitation (mm/day) values in it
high_res_data = xr.open_dataset('example_0p25x0p25.nc').precipitation  # pretend this is similar data, but on a higher resolution grid 
regridded_data = xc.regrid(data, high_res_data.longitude, high_res_data.latitude) # assuming the names of the dimensions are 'latitude' and 'longitude'. 
```

