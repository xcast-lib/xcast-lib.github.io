---
layout: page
title: BaseEstimator
permalink: /BaseEstimator/
---

# BaseEstimator

A class called `BaseEstimator` is at the core of most of XCast's functionality. It takes two-dimensional estimator classes, as in those of scikit-learn and other python data science packages, and extends them to be able to accommodate four-dimensional gridded climate data, as in `xarray.DataArrays`. It broadcasts the methods of the underlying two dimensional estimator across latitude and longitude / gridpoints, working with a separate instance of the estimator at each gridpoint efficiently in parallel. It gives you access to a subset of their methods - namely, `.fit`, `.predict`, `.transform`, and `.predict_proba`. (or a subset thereof, if your estimator is more of a transformer than an estimator, like in those in  `sklearn.decomposition`). 

BaseEstimator and its subclasses also accomodates gridpoint-wise hyperparameter tuning, using a home-brewed stochastic depth-first search tuning algorithm. Before fitting an estimator, use the `.tune` method to generate a set of optimized parameters, then pass that to your estimator during instantiation. Hyperparameter tuning is VERY slow when you have to broadcast it across gridpoints- so don't expect results any time soon! For examples, see the XCast github repository.

XCast obviously doesn't implement every possible estimator in the world - in fact the options are limited to only a small subset of methods so we can better support them. However, it is pretty easy to implement new XCast-style estimators by subclassing BaseEstimator: 

```
import xcast as xc 
from sklearn.linear_model import ElasticNet 

class XCElasticNet(xc.BaseEstimator):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.model_type = ElasticNet

``` 
You'll then be able to use XCElasticNet.fit, and the other sklearn.linear_model.ElasticNet class methods (out of .fit, .predict, .transform, and .predict_proba) as XCast-style functions. See all of the things implemented with BaseEstimator in the table below: 

| 2D estimator | XCast-Style Estimator | Deterministic Forecasts? | Tercile Probability Forecasts? | Non-Exceedance Forecasts? | 
| ---- | --- | --- | --- | --- |
| xcast.linear_regression | xcast.MLR |  YES | YES | YES | 
| xcast.multivariate_extended_logistic_regression | xcast.MELR | NO | YES | YES | 
| xcast.extended_logistic_regression | xcast.ELR | NO | YES | YES | 
| xcast.extreme_learning_machine | xcast.ELM | YES | YES | NO | 
| xcast.epoelm | xcast.EPOELM  | YES | YES | YES |  
| xcast.quantile_regression_forest | xcast.QRF  | YES | YES | YES |  



