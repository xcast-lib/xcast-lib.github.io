---
layout: page
title: OneHotEncoder
permalink: /OneHotEncoder/
---

# OneHotEncoder

The OneHotEncoder class is a transformer which one-hot encodes an xarray.DataArray according to tercile categories defined by the 33rd and 66th percentile of the data array along its time dimension. An array with feature size 1 will be transformed to an array with feature size 3, where each coordinate along the new feature dimension is a field where the value 1 indicates that a given sample fell within that tercile category, and a value of zero indicates that it did not. OneHotEncoder must first be fit on an xarray.DataArray, and then used to transform that or another data array. 
Once instantiated, you need to fit a `OneHotEncoder` on an xarray.DataArray, X, which should have the four dimensions expected by XCast (see [data in xcast](https://xcast-lib.github.io/data/)). After fitting, these objects can then be used to one-hot encode data formatted like `X`.  

```
ohc = xc.OneHotEncoder()
ohc.fit(X) 
T = ohc.transform(X) # this could be X1, a dataset from a different year of the same format as X. Scaled will have minimum of mm.min and maximum of mm.max
```

While no XCast estimators (as of v1.0.0) require One-Hot Encoded training data, `OneHotEncoder` is still used to transform observations for the sake of comparison. Many of XCast's metrics require one-hot encoded observation data for comparison with probabilistic forecasts. 






