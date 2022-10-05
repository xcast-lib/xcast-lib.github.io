---
layout: page 
title: Installing XCast 
permalink: /installation
---

# Installing XCast

XCast is distributed on [Anaconda](https://www.anaconda.com/products/distribution) and through the [```conda```](https://docs.conda.io/en/latest/) package manager. It is distributed as-is on the [hallkjc01](https://anaconda.org/hallkjc01) conda channel. 

However, we recommend using this sequence of commands to set up a jupyter notebook kernel for XCast work:

```
conda create -c conda-forge -c hallkjc01 -n xcast_env xcast xarray netcdf4 matplotlib cartopy jupyter ipykernel 
conda activate xcast_env
python -m ipykernel install --user --name=xcast_env
```

You'll then be able to run jupyter notebooks under the ```xcast_env``` kernel, and have access to xcast. 

You can also do whatever you want! It's an Anaconda library- so you can install it , remove it, whatever! Have a blast!

[contributors-shield]: https://img.shields.io/github/contributors/kjhall01/xcast.svg?style=for-the-badge
[contributors-url]: https://github.com/kjhall01/xcast/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/kjhall01/xcast.svg?style=for-the-badge
[forks-url]: https://github.com/kjhall01/xcast/network/members
[stars-shield]: https://img.shields.io/github/stars/kjhall01/xcast.svg?style=for-the-badge
[stars-url]: https://github.com/kjhall01/xcast/stargazers
[issues-shield]: https://img.shields.io/github/issues/kjhall01/xcast.svg?style=for-the-badge
[issues-url]: https://github.com/kjhall01/xcast/issues
[license-shield]: https://img.shields.io/github/license/kjhall01/xcast.svg?style=for-the-badge
[license-url]: https://github.com/kjhall01/xcast/blob/main/LICENSE
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/kjhall01
