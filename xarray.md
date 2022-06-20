---
layout: page
title: Xarray Resources
permalink: /xarray/ 
---

# Introduction To Xarray

[Xarray](https://docs.xarray.dev/en/stable/) is a powerful python library for manipulating gridded geospatial data, like NetCDF and GeoTIFF files. It is extremely flexible and powerful, as well as well-accepted by the Python climate data community. 

XCast is built to produce and consume [```Xarray.DataArray```](https://docs.xarray.dev/en/stable/generated/xarray.DataArray.html), much like [Scikit-Learn](https://scikit-learn.org/) is built to produce and consume NumPy arrays. Therefore, users of XCast need to have a solid understanding of how to use Xarray to prepare their datasets. 

XCast is designed to use four-dimensional data arrays - two spatial dimensions, across which to chunk and parallelize data, one sample dimension, and one feature dimension. Other dimensions should be flattened out or otherwise removed from datasets before they are passed to XCast. To that end, here are some example Xarray dataflows useful for XCast users: 

### Opening Files: 

```xr.open_dataset``` is an xarray function capable of opening a diverse set of gridded data files like geoTIFF, netcdf, hdf5 and more. It returns an ```xr.Dataset```, so a dataarray must be extracted before it can be used with XCast. 

```
import xarray as xr 
ds = xr.open_dataset('test_data.nc') 
predictor = ds.precipitation
```

### Slicing Data 

Sometimes it may be necessary to subset a data across time or space, for one reason or another. Xarray datasets and dataarrays have powerful subsetting functions: ```.isel``` and ```.sel```. 

```.isel``` can be thought of as short for "index select"- because it works the same way as normal python indexing (integers starting at zero). 

Since Xarray's dimensions are labelled by coordinates, you can also select based on the coordinates using the ```.sel``` method. 

```
import xarray as xr 
import datetime as dt
ds = xr.open_dataset('test_data.nc') 
predictor = ds.precipitation

# select years based on index
first_year = predictor.isel(T=0) 
first_ten_years = predictor.isel( T=slice(0, 10) )

# select years based on coordinates
# the coordinate "dt.datetime(1982, 1, 1)" must be present on predictor's T dimension
first_year = predictor.sel( T=dt.datetime(1982, 1, 1) )  

# the coordinate "dt.datetime(1982, 1, 1)" must be present on predictor's T dimension - everything between 1982 and 1992 will be returned
first_ten_years = predictor.sel( T=slice(dt.datetime(1982, 1, 1), dt.datetime(1992, 1, 1) ) )   
```

### Removing a Dimension by Aggregation

Selecting a single point along a dimension will remove that dimension, but sometimes you may also want to do that by taking the average across a dimension, or the standard deviation, or another aggregation. 

```
import xarray as xr 
ds = xr.open_dataset('test_data.nc') 
predictor = ds.precipitation

mean = predictor.mean('T')  # average 
std = predictor.std('T')    # standard deviation 
min = predictor.min('T')    # minimum 
max = predictor.max('T')    # maximum
sum = predictor.sum('T')    # summation 
``` 


You can also chain these together! 

```
import xarray as xr 
ds = xr.open_dataset('test_data.nc') 
predictor = ds.precipitation
regional_mean = predictor.sel(X=slice(10, 20), Y=slice(10, 20)).mean('X').mean('Y') 
``` 

### Renaming Dimensions

Any Xarray dimension / coordinate can be renamed by passing a dictionary mapping ```current_names``` to ```desired_names``: 

```
import xarray as xr 
ds = xr.open_dataset('test_data.nc') 
predictor = ds.precipitation
predictor_renamed = predictor.rename({'latitude1': 'new_latitude', 'longitude1': 'new_longitude'}) 
```



Xarray's full documentation is available at [https://docs.xarray.dev/en/stable](https://docs.xarray.dev/en/stable) - check it out! 




