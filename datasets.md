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




