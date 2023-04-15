---
layout: page
title: Normal
permalink: /Normal/
---

# Normal

The Normal class is a a transformer which scales an xarray.DataArray to zero-mean and unit variance. ( In a very similar way to Scikit-Learn's StandardScaler) Normal must first be fit on an xarray.DataArray, and then used to transform that or another data array. 

```
norm = xc.Normal()
```

Once instantiated, you need to fit `norm` on an xarray.DataArray, X, which should have the four dimensions expected by XCast (see [data in xcast](https://xcast-lib.github.io/data/))

``` 
norm.fit(X) 
``` 

after fitting, these objects can then be used to apply standard anomaly scaling to data that looks like `X`: 

```
scaled = norm.transform(X) # this could be X1, a dataset from a different year of the same format as X. Scaled will have mean of 0 at each point and std.dev of 1 at each point. 
```

additionally, the `norm` object can be used to reverse the transformation: 

```
unscaled = norm.inverse_transform(scaled) 
```







