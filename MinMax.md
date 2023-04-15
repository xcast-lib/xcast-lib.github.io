---
layout: page
title: MinMax
permalink: /MinMax/
---

# MinMax

The MinMax class is a transformer which scales an xarray.DataArray to the interval [-1, 1]. MinMax must first be fit on an xarray.DataArray, and then used to transform that or another data array.


```
minmax = xc.MinMax(
  min=-1, # minimum value to scale data to
  max=1   # maximum value to scale data to
)
```

Once instantiated, you need to fit `mm` on an xarray.DataArray, X, which should have the four dimensions expected by XCast (see [data in xcast](https://xcast-lib.github.io/data/))

``` 
mm.fit(X) 
``` 

after fitting, these objects can then be used to apply minmax scaling to data that looks like `X`: 

```
scaled = mm.transform(X) # this could be X1, a dataset from a different year of the same format as X. Scaled will have minimum of mm.min and maximum of mm.max
```

additionally, the `mm` object can be used to reverse the transformation: 

```
unscaled = mm.inverse_transform(scaled) 
```







