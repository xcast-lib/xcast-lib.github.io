---
layout: page
title: Preprocessing: Spatial Principal Components Analysis (Empirical Orthogonal Functions) 
permalink: /spatialpca/
---

# Preprocessing: Spatial Principal Components Analysis (Empirical Orthogonal Functions) 
### xc.SpatialPCA ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/preprocessing/spatial.py#L91))

SpatialPCA uses Scikit-Learn’s PCA class to calculate PCA modes across the spatial dimensions of an Xarray DataArray  - generally this is referred to as calculating ‘EOFs’ - Empirical Orthogonal Functions - in the climate world. 

It proceeds by stacking all of the latitude/longitude/feature grid points along a single dimension, dropping the points where any missing values (NaNs) are present, and then feeding the (N Samples) x (lat x lon x feature) into scikit learn’s PCA.fit method. 

Optionally, you can specify the use of preprocessing (‘none’, ‘minmax’, or ‘stdanomaly’) and whether or not you want to apply cosine-latitude weighting to the data before fitting PCA. 

The fit method fits the PCA model and saves the spatial loadings of the dataset in PCA.loadings.  the transform method uses that PCA model to return a data array storing PCA time series scores.  

**Constructor** 
Arguments: 
- None

Keyword Arguments: 
- latitude_weighting (default: True) - whether or not to apply cosine-latitude weighting to the data pre-fit 
- preprocessing (default: ‘std’) - whether or not to apply pre-scaling ( std, or none) to the data pre-fit. 
- **kwargs - other keyword arguments to be passed to scikit-learn.decomposition.PCA

**.fit**
Arguments: 
- X: an xr.DataArray conforming to the xcast dimensionality standards

Keyword Arguments: 
- **guess coords keyword args 

Returns: 
- None 

Post-Fit Attributes 
- loadings - an xarray data array storing the spatial loadings for this dataset. 

**.transform** 
Arguments: 
- X: an xr.DataArray conforming to the xcast dimensionality standards

Keyword Arguments: 
- **guess coords keyword args 

Returns: 
- ret- an xr. DataArray storing the temporal scores for each mode/ sample. 
