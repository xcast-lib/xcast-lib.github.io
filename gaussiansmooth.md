---
layout: page
title: Postprocessing: Gaussian Kernel Smoothing
permalink: /gaussiansmooth/
---

# Postprocessing: Gaussian Kernel Smoothing

### xc.gaussian_smooth ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/preprocessing/spatial.py#L176)) 

gaussian_smooth implements gaussian kernel smoothing. Since most of XCast’s methods are completely independent at each gridpoint, it can be desirable to apply gaussian kernel smoothing with kernels of different sizes, to reduce the perceived spatial noise, and draw the eye to larger-scale spatial signals. Gaussian_smooth is implemented with SciPy’s gaussian kernel functionality, and applied independently at each sample / feature across a dataset. 

**Arguments**
- X: an Xarray DataArray following the xcast dimensionality conventions

**Keyword Arguments**
- kernel (default: 3) - argument to be passed to SciPy, specifying the width/height of the kernel to be applied for gaussian smoothing. This should be an odd integer greater than 1. (for now, the kernel must be square- hence only one number passed) 
- **guess coords kwargs 

**Returns**
- X2: smoothed dataarray 
