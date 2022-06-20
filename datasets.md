---
layout: page
title: Datasets in XCast
permalink: /datasets/
---

# Datasets in XCast 

XCast is designed to use four-dimensional datasets - latitude, longitude, samples, and features. While these are the terms we use to discuss each of these dimensions, and differentiate them, their meanings are flexible. 

Latitude and longitude are the dimensions across which data will be chunked and parallelized - usually this represents lat/lon or space otherwise, but it can also be used to represent any other dimension across which 'pointwise' operations should be mapped. You could do, for examples, latitude x altitude, longitude x geopotential height, etc. 

The sample dimension is used to represent the distinct training samples used to fit each model. Usually, at least in seasonal forecasting, this is one sample per year. It can represent other things, like weeks or other units of time, but the user should think about what makes sense to do. 

The feature dimension is the dimension which represents the distinct predictors passed to the model during fitting. 

Every training dataarray needs to have 4 dimensions - even continuous predictand dataarrays, which intuitively would have 3 dimensions, needs to have a fourth dimension, of size one. 


Additionally, predictors and predictands should be the same size in latitude/longitude dimensions. Otherwise 'gridpoint-wise' operations don't make sense. XCast's regridding functionality will help with this. They should also have the same chunking scheme, which can be managed with xcast's "align_chunks" function. 

```
import xcast as xc 
import xarray as xr 

x = xr.open_dataset('test_data_x.nc').prec 
y = xr.open_dataset('test_data_y.nc').prec 

x = xc.regrid(y.coords['X'].values, y.coords['Y'].values, x) 
x, y = xc.align_chunks(x, y, 10, 10) # number of chunks across lat/lon 
```

## Dimension & Coordinate Naming

One drawback of Xarray's flexibility is that netcdf files, geotiff files, and other datasets are allowed to have different names for the same dimension. a Time dimension can be 'Time', 'T', 'Initialization', 'Target', 'Year', or anything else really - so its not possible to automatically detect which dimensions are meant to be which in every case. 

XCast accomodates this by implementing smart name-guessing heuristics based on the most common sets of coordinate and dimension names in climate data. 
In XCast, the following common dimension names (and their mixed-case versions like Lat and Lon) will be auto-detected.  

```
common_x = ['LONGITUDE', 'LONG', 'X', 'LON']
common_y = ['LATITUDE', 'LAT', 'LATI', 'Y']
common_t = ['T', 'S', 'TIME', 'SAMPLES', 'SAMPLE', 'INITIALIZATION', 'INIT', "TARGET"]
common_m = ['M', 'FEATURES', 'F', 'REALIZATION', 'MEMBER', 'Z', 'C', 'CAT']
```

XCast operations will fail if the names of the four XCast dimensions (lat/lon/sample/feature) cannot be auto-detected. Luckily, rather than requiring you to rename your dimensions and coordinates, XCast allows you to pass them as keyword arguments to any function or estimator. For functions and estimator methods that accept just an 'x' dataarray, you should pass ```x_lat_dim='your_latitude_coordname', x_lon_dim='your_longitude_coordname', x_sample_dim='your_sample_coordname', x_feature_dim='your_feature_coordname'```. For things that accept two data arrays, those are available, as well as ```y_lat_dim='your_latitude_coordname', y_lon_dim='your_longitude_coordname', y_sample_dim='your_sample_coordname', y_feature_dim='your_feature_coordname'``` 

For example: 

```
import xcast as xc 
import xarray as xr 

x = xr.open_dataset('test_data_x.nc').prec 
y = xr.open_dataset('test_data_y.nc').prec 

x = xc.regrid(y.coords['X'].values, y.coords['Y'].values, x, x_lat_dim='lat1', x_lon_dim='lon1', x_sample_dim='samples', x_feature_dim='features') 
x, y = xc.align_chunks(x, y, 10, 10) # number of chunks across lat/lon 
```



