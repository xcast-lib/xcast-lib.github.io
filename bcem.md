---
layout: page 
title: Regressors: Bias-Corrected Ensemble Mean
permalink: /biascorrectedensemblemean/
---

# Regressors: Bias-Corrected Ensemble Mean
### xc.BiasCorrectedEnsembleMean ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/estimators/regressors.py#L45))


BiasCorrectedEnsembleMean is one of the rare the XCast estimators which is not implemented with BaseEstimator- it is a pure Xarray method, and all it does is take the average over the feature dimension of the X data array, after each of them has separately been scaled to N(0, 1), and then scaled to the mean and standard deviation of the Y data array. This estimator is only required as a drop-in replacement for other methods, so the same workflows can be used with BiasCorrectedEnsembleMean and no unreasonable effort is needed to accommodate the comparison.
