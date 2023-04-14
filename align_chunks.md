---
layout: page
title: align_chunks
permalink: /align_chunks/
---

# align_chunks

align_chunks takes two compatible four-dimensional xarray.DataArray, and rechunks each of them along their latitude and longitude dimensions such that they match and can be parallelized. 

```
X, Y = xc.align_chunks(X, Y, lat_chunks=5, lon_chunks=5, x_lat_dim=None, x_lon_dim=None, y_lat_dim=None, y_lon_dim=None, x_feature_dim=None, y_feature_dim=None, x_sample_dim=None, y_sample_dim=None):
```

Where `X` and `Y` are the data arrays of interest and `lat_chunks` and `lon_chunks` specify the number of chunks along the latitude and longitude dimensions respectively.

This function will convert in-memory data arrays to dask arrays. This not required, but allows you to use `dask.distributed.Client` to distributed XCast computations to multiple subprocesses or a task scheduler like slurm. 
If the data arrays you're working with are in-memory (i.e., the da.values returns a NumPy array, rather than a Dask array) then using a dask client will not yield any parallelism or benefit. 

Instead of using `align_chunks`, you could re-chunk manually with `xarray.DataArray.chunk`, or open your netcdf files as out-of-memory dask arrays by passing the `chunks` argument to  `xarray.open_dataset`. The size and shape of the chunks must match exactly between X and Y in order to be compatible- you'll get a Dask error message if they do not. 

If you are using a dask client to parallelize your workflow as below, remember to pass the `rechunk=False` keyword argument to your XCast functions and class methods, otherwise XCast will by default convert whatever you pass into a single-chunk dask array and you'll get slower performance.

```
import xcast as xc 
from dask.distributed import Client 

X, Y = xc.align_chunks(X, Y, lat_chunks=5, lon_chunks=5, x_lat_dim=None, x_lon_dim=None, y_lat_dim=None, y_lon_dim=None, x_feature_dim=None, y_feature_dim=None, x_sample_dim=None, y_sample_dim=None):
with Client(): 
  ( ... some XCast functions here ... )
```

