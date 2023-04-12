---
layout: page 
title: 2. Installing XCast 
permalink: /installation
---

# Installing XCast

XCast is distributed as-is on [Anaconda](https://www.anaconda.com/products/distribution) on my [hallkjc01](https://anaconda.org/hallkjc01) conda channel. 

However, I recommend using this sequence of commands to set up a jupyter notebook kernel for XCast work:

```
conda create -c conda-forge -c hallkjc01 -n xcast_env xcast xarray netcdf4 matplotlib cartopy jupyter ipykernel 
conda activate xcast_env
python -m ipykernel install --user --name=xcast_env
```

You'll then be able to run jupyter notebooks under the ```xcast_env``` kernel, and have access to xcast. 

