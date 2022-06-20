---
layout: page
title: Docs: Preprocessing
permalink: /preprocessing/
---

# Docs: Preprocessing

XCast implements a diverse array of data preprocessing methodologies including regridding, smoothing, rescaling, one-hot encoding, and dimensionality reduction. 

### regridding 
XCast is capable of interpolating/extrapolating your dataset in order to change its resolution, in a process commonly called 'regridding'. This functionality is contained with ```xc.regrid```, a function which wraps SciPy's ```interp2d``` utility. In addition to the standard dimension naming keyword arguments, ```xc.regrid``` accepts three positional arguments, and a set of keyword arguments to be passed on to [SciPy.interp2d](https://docs.scipy.org/doc/scipy/reference/generated/scipy.interpolate.interp2d.html). The first and second positional arguments should be arrays (NumPy Arrays) representing the target longitude and latitude (x and y) coordinates, onto which you want your data regridded. The third argument should be the dataset itself. Keep in mind that the order of the positional arguments matters, and that the order of the coordinates on your DataArray matter. If the spatial coordinates on the dataarray are inconsistent with the ones you ask to regrid onto, you may get nonsense results. You can set the type of interpolation by passing the "kind" argument equal to one of 'linear' (default), 'cubic', or 'quintic'. 

```
import xarray as xr 
import xcast as xc 
test_data = xr.open_dataset('test_data.nc').prec
test_data2 = xr.open_dataset('test_data2.nc').prec

# regrids test_data onto resolution of test_data2
regridded = xc.regrid(test_data2.coords['X'].values, test_data2.coords['Y'].values, test_data) 
```

### smoothing 
XCast uses OpenCV to implement 2D Gaussian Kernel smoothing across spatial dimensions, in the ```xc.gaussian_smooth``` function. In addition to dimension name keywords, this function accepts a target data array, and a 'kernel' keyword argument (a tuple of integers, of length 2)  which specifies the size of the smoothing kernel (it must be odd in both dimensions).

```
import xarray as xr 
import xcast as xc 
test_data = xr.open_dataset('test_data.nc').prec

# 3x3 Gaussian Kernel Smoothing
smoothed = xc.gaussian_smooth(test_data, kernel=(3, 3) ) 
```

### rescaling
XCast implements both MinMax and Standard Anomaly rescaling (normalization). MinMax maintains the relative distances between data points, and Standard Anomaly centers the data to mean-zero and unit-standard-deviation. The user should make an informed choice about which to use, if any. 

Both methods are implemented as Transformers in XCast - objects that are 'fit' on one dataset, and remember the transformation learned from it to be used many times in the future. They accept dimension name arguments. MinMaxScaler accepts 'min' and 'max' arguments which specify the desired target range for transformation (default (-1, 1) ) .

```
import xarray as xr 
import xcast as xc 
test_data = xr.open_dataset('test_data.nc').prec

mm = xc.MinMaxScaler(min=-2, max=2)
mm.fit(test_data) 
test_data_transformed = mm.transform(test_data) 
test_data_detransformed = mm.inverse_transform(test_data_transformed) 

std_anom = xc.NormalScaler() 
std_anom.fit(test_data) 
test_data_transformed = std_anom.transform(test_data) 
test_data_detransformed = std_anom.inverse_transform(test_data_transformed)
``` 

### Tercile One-Hot Encoding
Since certain classifiers in XCast must be trained on 'One-Hot Encoded' categorical target vectors, XCast implements a One-Hot Encoder class which will transform continuous data into tercile-category data based on given percentile thresholds. 

One-Hot Encoding proceeds by identifying the 33rd and 66th percentiles of the data. Data points below the threshold identified at the 33rd percentile are sorted into the 'Below Normal' class. Data Points above the 66th percentile threshold are sorted into 'above normal', and all others are sorted into 'Normal'. These categories are then associated with binary target vectors of length three, where the first index corresponds to the Below Normal class, the second to the 'Normal' class, and the third to the 'Above Normal' class. For example, Below Normal would be [1,0,0] and above normal would be [0,0,1]. 

```
import xarray as xr 
import xcast as xc 
test_data = xr.open_dataset('test_data.nc').prec

ohc = xc.RankedTerciles(low_thresh=0.33, high_thresh=0.67) # must be between (0,1)
ohc.fit(test_data) 
test_data_transformed = ohc.transform(test_data) 
``` 

### Dimensionality Reduction
XCast implements two approaches to dimensionality reduction - dimensionality reduction across the feature dimension, and dimensionality reduction across the spatial dimensions. 

**feature*** feature-dimensionality reduction just changes the number of features along the feature dimension - it is up to the user to decide if this makes sense. 
```
import xarray as xr 
import xcast as xc 
test_data = xr.open_dataset('test_data.nc').prec

# Principal Components Analysis
pca = xc.PrincipalComponentsAnalysis(n_components=3) # save three PCA modes
pca.fit(test_data) 
test_data_transformed = pca.transform(test_data) 
test_data_detransformed = pca.inverse_transform(test_data_transformed) 

# Non-Negative Matrix Factorization
nmf = xc.NMF(n_components=3) 
nmf.fit(test_data) 
test_data_transformed = nmf.transform(test_data) 
test_data_detransformed = nmf.inverse_transform(test_data_transformed) 

# Factor Analysis 
fa = xc.FactorAnalysis(n_components=3) 
fa.fit(test_data) 
test_data_transformed = fa.transform(test_data) 
test_data_detransformed = fa.inverse_transform(test_data_transformed)

# Dictionary Learning
dl = xc.DictionaryLearning(n_components=3) 
dl.fit(test_data) 
test_data_transformed = dl.transform(test_data) 
test_data_detransformed = dl.inverse_transform(test_data_transformed) 
``` 

**spatial** XCast implements Principal Components Analysis across the spatial dimensions of a data array as ```xc.SpatialPCA```. This method is also commonly known as "EOF analysis" and XCast is not the only python library to implement it. It shrinks the spatial dimensions into one dimension called 'mode', and expands a 'fake-latitude' dimension so you can still use the dataarray with XCast estimators.  Mode then becomes a 'fake-longitude' dimension.

```
import xarray as xr 
import xcast as xc 
test_data = xr.open_dataset('test_data.nc').prec

# Spatial Principal Components Analysis / EOFS
pca = xc.SpatialPCA(n_components=3) # save three PCA modes
pca.fit(test_data) 
test_data_transformed = pca.transform(test_data) 
eofs = pca.eofs() # data array storing spatial loadings
``` 






