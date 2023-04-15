---
layout: page
title: GammaTransformer
permalink: /GammaTransformer/
---

# GammaTransformer

The `GammaTransformer` class is a transformer which attempts to make a dataset fit the Gaussian Normal distribution better through a gamma-transform. Gamma Transformer must first be fit on an xarray.DataArray, and then used to transform that or another data array. 

```
gam = xc.GammaTransformer()
gam.fit(X) 
Xg = gam.transform(X) # this could be X1, a dataset from a different year of the same format as X.
```

Gamma Transformers let you coerce your data into fitting gaussian assumptions a little better, but generally are slow, don't work perfectly, and aren't recommended. There are better ways to address non-gaussian data sets.





