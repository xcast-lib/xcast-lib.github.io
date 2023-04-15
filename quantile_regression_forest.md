---
layout: page
title: quantile_regression_forest
permalink: /quantile_regression_forest/
---

# quantile_regression_forest

This class is a 2D estimator representing Quantile Regression Forest and is heavily based on the [PyQuantRF](https://github.com/jnelson18/pyquantrf/) library. This implementation implements small but important changes to improve training speed and decrease memory usage.

For more detail on the QRF method, please refer to [Meinshausen, 2006](https://www.jmlr.org/papers/volume7/meinshausen06a/meinshausen06a.pdf].

```
qrf = quantile_regression_forest(**rf_kwargs)
```

This implementation heavily uses [sklearn.ensemble.RandomForestRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html)
Please refer to the Scikit-Learn docs for more details about QRF hyper-parameter options. 

Once instantiated, you need to fit `qrf` on two numpy-arrays, `x`, and `y`. 

``` 
qrf.fit(x, y) 
``` 

you can then make deterministic and probabilistic predictions for new data like `x` (`x1`, maybe) as follows: 

```
deterministic_preds = qrf.predict(x1)
tercile_probabilities = qrf.predict_proba(x1) 
nonexceedance_30thpercentile = qrf.predict_proba(x1, quantile=0.3) 

```









