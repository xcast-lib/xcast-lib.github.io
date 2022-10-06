---
layout: page
title: Regressors: Ensemble Mean
permalink: /ensemblemean/ 
---

# Regressors: Ensemble Mean
### xc.EnsembleMean ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/estimators/regressors.py#L13))

EnsembleMean is one of the rare XCast estimators which is not implemented with BaseEstimator- it is a pure Xarray method, and all it does is take the average over the feature dimension of the X data array. This estimator is only required as a drop-in replacement for other methods, so the same workflows can be used with EnsembleMean and no unreasonable effort is needed to accommodate the comparison.
