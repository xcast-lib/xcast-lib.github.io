---
layout: page
title: view_roc
permalink: /view_roc/
---

# view_roc

view_roc plots the receiver operating characteristics curve for each feature on two xarray.DataArrays (X and Y) where Y is one-hot encoded observations and X is tercile probabilty forecasts. 

```
view_reliability(
  X,                     # probabilistic predictions
  Y,                     # one-hot encoded observations
  x_lat_dim=None,        
  x_lon_dim=None, 
  x_feature_dim=None, 
  x_sample_dim=None, 
  y_lat_dim=None, 
  y_lon_dim=None, 
  y_feature_dim=None, 
  y_sample_dim=None, 
)
```

IMPORTANT: If, for example, your observations have missing values (NaN) over ocean or otherwise, but for whatever reason your predictions do not, you WILL need to mask those values out before you use them with `view_roc`
