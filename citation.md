---
layout: page
title: 4. Citing XCast
permalink: /xcast_citing/
---

# Citing XCast 
Please cite the xcast whitepaper if you have used XCast in your work 

#### Bibtex
```
@article{10.3389/fclim.2022.953262,
	title        = {XCast: A python climate forecasting toolkit},
	author       = {Hall, Kyle Joseph Chen and Acharya, Nachiketa},
	year         = 2022,
	journal      = {Frontiers in Climate},
	volume       = 4,
	doi          = {10.3389/fclim.2022.953262},
	issn         = {2624-9553},
	url          = {https://www.frontiersin.org/articles/10.3389/fclim.2022.953262},
	abstract     = {Climate forecasts, both experimental and operational, are often made by calibrating Global Climate Model (GCM) outputs with observed climate variables using statistical and machine learning models. Often, machine learning techniques are applied to gridded data independently at each gridpoint. However, the implementation of these gridpoint-wise operations is a significant barrier to entry to climate data science. Unfortunately, there is a significant disconnect between the Python data science ecosystem and the gridded earth data ecosystem. Traditional Python data science tools are not designed to be used with gridded datasets, like those commonly used in climate forecasting. Heavy data preprocessing is needed: gridded data must be aggregated, reshaped, or reduced in dimensionality in order to fit the strict formatting requirements of Python's data science tools. Efficiently implementing this gridpoint-wise workflow is a time-consuming logistical burden which presents a high barrier to entry to earth data science. A set of high-performance, easy-to-use Python climate forecasting tools is needed to bridge the gap between Python's data science ecosystem and its gridded earth data ecosystem. XCast, an Xarray-based climate forecasting Python library developed by the authors, bridges this gap. XCast wraps underlying two-dimensional data science methods, like those of Scikit-Learn, with data structures that allow them to be applied to each gridpoint independently. XCast uses high-performance computing libraries to efficiently parallelize the gridpoint-wise application of data science utilities and make Python's traditional data science toolkits compatible with multidimensional gridded data. XCast also implements a diverse set of climate forecasting tools including traditional statistical methods, state-of-the-art machine learning approaches, preprocessing functionality (regridding, rescaling, smoothing), and postprocessing modules (cross validation, forecast verification, visualization). These tools are useful for producing and analyzing both experimental and operational climate forecasts. In this study, we describe the development of XCast, and present in-depth technical details on how XCast brings highly parallelized gridpoint-wise versions of traditional Python data science tools into Python's gridded earth data ecosystem. We also demonstrate a case study where XCast was used to generate experimental real-time deterministic and probabilistic forecasts for South Asian Summer Monsoon Rainfall in 2022 using different machine learning-based multi-model ensembles.}
}
```

#### IEEE Format
```
K. J. C. Hall and N. Acharya, ‘XCast: A python climate forecasting toolkit’, Frontiers in Climate, vol. 4, 2022.
```




