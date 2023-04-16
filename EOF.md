---
layout: page
title: EOF
permalink: /EOF/
---

# EOF

This is a transformer which applies empirical orthogonal function (principal components) analysis to a four-dimensional xarray.DataArray. It calculates spatial loadings, which remain stored in the eof_loadings attribute of the EOF transformer object, as well as time series scores (stored as eof_scores on the EOF transformer object) and the portion of variance explained by each of the modes (explained_variance). After fitting, it can be used to transform X-like data arrays using the calculated EOF loadings. 

```
eof = xc.EOF(
  modes=None, # number of modes to retain - default is min(samples, gridpoints) 
  latitude_weighting=False, # whether or not to applie cosine latitude weighting to X before calculating EOFs
  separate_members=True,  # if the provided data array has more than one coordinate in the feature dimension, whether to stack these or apply EOF separately to each
)
```

Once instantiated, you need to fit `eof` on an xarray.DataArray, "X" 

``` 
eof.fit(x, y) 
``` 

After fitting, the principal component time-series scores, loadings, and singular values will be available as NumPy arrays as attributes on the `eof` object, named as follows: 

```
eof_percent_variance_expained         = eof.eof_variance_explained             # Percent Variance explained by each mode
eof_scores                            = eof.eof_scores                         # PC time series for y# EOFs/PC loadings 
eof_loadings                          = eof.eof_loadings                       # EOFs/PC loadings for x
```

you can then also calculate the PC scores for new data like `x` (`x1`, maybe) as follows: 

```
new_scores = eof.transform(x1)
```








