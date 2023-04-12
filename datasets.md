---
layout: page
title: Data in XCast
permalink: /data/
---

# Data Objects

XCast class methods and functions largely only accepts four-dimensional xarray.DataArrays. These four dimensions generally should correspond to
1. latitude, or another spatial dimensions across which gridpoint-wise operations will be mapped
2. longitude, or a second spatial dimensions across which gridpoint-wise operations will be mapped
3. samples - whether distinct years, initializations, or another delineation of the separate samples seen by statistical techniques
4. features - distinct independent variables, as understood by statistical techniques. 

Please note the distinction between xarray.DataArray and xarray.DataSet - the two classes have significantly different data models and APIs, and XCast will not accept xarray.DataSets. This means you'll need to extract the data variable you want to work with from an xarray.DataSet before passing it to XCast. 

# Dimension & Coordinate Naming

Since netcdf files, geotiff files, and other data formats can have arbitrary dimensionality, it's not really possible to automatically detect which dimensions are meant to represent each of the four dimensions we intend for XCast to see, in every case. To make life easier for everyone, we have implemented a name-guessing heuristic based on the most common sets of coordinate and dimension names in climate science. 

```
often_used = { 
	'longitude': ['LONGITUDE', 'LONG', 'X', 'LON'],
	'latitude': ['LATITUDE', 'LAT', 'LATI', 'Y'],
	'sample': ['T', 'S', 'TIME', 'SAMPLES', 'SAMPLE', 'INITIALIZATION', 'INIT','D', 'DATE', "TARGET", 'YEAR', 'I', 'N'],
	'feature': ['M', 'MODE', 'FEATURES', 'F', 'REALIZATION', 'MEMBER', 'Z', 'C', 'CAT', 'NUMBER', 'V', 'VARIABLE', 'VAR', 'P', 'LEVEL'],
}
```

XCast operations will print warnings if the names of the four XCast dimensions cannot be uniquely determined. In this case, you can either rename your dimensions and coordinates appropriately, or pass them as keyword arguments to any function or class method. The keyword arguments are named as follows. 

```x_lat_dim='your_latitude_coordname', x_lon_dim='your_longitude_coordname', x_sample_dim='your_sample_coordname', x_feature_dim='your_feature_coordname'```

If you need to specify the dimension labels on a second xarray.DataArray argument, use:

```y_lat_dim='your_latitude_coordname', y_lon_dim='your_longitude_coordname', y_sample_dim='your_sample_coordname', y_feature_dim='your_feature_coordname'``` 

For example: 

```
import xcast as xc 
import xarray as xr 

x = xr.open_dataset('test_data_x.nc').prec 
y = xr.open_dataset('test_data_y.nc').prec 

x = xc.regrid(y.coords['X'].values, y.coords['Y'].values, x, x_lat_dim='lat1', x_lon_dim='lon1', x_sample_dim='samples', x_feature_dim='features') 
```



