---
layout: page 
title: 1. About 
permalink: /
---

<!-- PROJECT SHIELDS -->
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
![installs](https://img.shields.io/conda/dn/hallkjc01/xcast?color=light-green&label=Installations&style=for-the-badge)
[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.6472890-blue?style=for-the-badge)](https://zenodo.org/badge/latestdoi/386326352)




<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/kjhall01/xcast/">
    <h1 align="center"><img src="https://raw.githubusercontent.com/kjhall01/xcast/gh-pages/XCastLogo.png" align="center" alt="Logo" width="60" height="60">  XCast</h1>
  </a>
</p>

                                                               Kyle Hall and Nachiketa Acharya

## Welcome

XCast is a Python Climate Forecasting toolkit - a set of flexible functions and classes that let you implement any forecasting workflow you can think of. It uses [Xarray](https://xarray.dev/) and [Dask Parallelism](https://dask.org/) to apply statistical and machine learning methods to any kind of gridded climate data quickly and efficiently.

Our goal is to lower the barriers to entry to innovation in climate and weather forecasting by bridging the gap between Python's gridded data utilities (Xarray, NetCDF4, etc) and its data science utilities (Scikit-Learn, Scipy, OpenCV). While XCast focuses on newer experimental techniques like quantile regression forest and extreme learning machine, it also implements many industry standard preprocessing methods and forecasting techniques from ensemble averaging to extended logistic regression. If there's something you feel is missing from XCast, have no fear- XCast is designed to be easily extensible (see BaseEstimator and @metric).

Through dask, XCast is fully compatible with many job schedulers and workload management systems. It lets you scale your machine learning-based forecasting methods to servers and institutional supercomputer clusters with ease.

*XCast v0.6.9 is now live - report issues [here](https://github.com/kjhall01/xcast/issues)*

*For more information, please check out the [xcast whitepaper](https://www.frontiersin.org/articles/10.3389/fclim.2022.953262/full)*


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
