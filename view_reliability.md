---
layout: page
title: view_reliability
permalink: /view_reliability/
---

# view_reliability

view_reliability calculates and plots the reliability_diagram separately for each feature on two compatible xarray.DataArrays, one of which represents a tercile forecast and one of which represents one hot encoded observations.   It will pool all the gridpoints across space to produce a reliability diagram that represents the full geographical extent covered by the data arrays. 
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
  **kwargs               # keyword arguments to be forwarded to xc.reliability_diagram
)
```

IMPORTANT: If, for example, your observations have missing values (NaN) over ocean or otherwise, but for whatever reason your predictions do not, you WILL need to mask those values out before you use them with `view_reliability`
