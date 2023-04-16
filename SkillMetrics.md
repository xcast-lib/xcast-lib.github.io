---
layout: page
title: SkillMetrics
permalink: /SkillMetrics/
---

# SkillMetrics

It is important to evaluate the skill of a predictive model (otherwise, what's the point?) Luckily, XCast lets you compute skill scores of all kinds efficiently across the lat/long gridpoints of an `xarray.DataArray`. The skill metrics that come pre-made with Xcast are detailed below but are by no means exhaustive- there are far more metrics out there than we could hope to support. 

However, you can easily implement an XCast metric yourself using the `@metric` function decorator! This takes an existing function, and modifies it to accept two 4-dimensional `xarray.DataArrays`, to do all the XCast safety checks, to detect coordinates, and to finish the rest of the logistics, then broadcast the skill function across the latitude/longitude points of the data arrays.

Functions you extend with the `@metric` decorator should accept two numpy arrays of shape `N x M`, where N is the number of samples and M is the number of features. This condition holds if M is one- the arrays should be column vectors in that case. The samples and features will correspond to the sample and feature dimensions on your xarray.DataArrays - the function will not be broadcast along the feature dimension. 

Here is an example of how one could implement the Root-Mean-Squared-Error in XCast: 

```
from xcast import metric 

# this is the 2-dimensional function which calculates the RMSE between two NumPy Column Vectors.
def rmse(x, y):
  # x is Nx1, y is Nx1
  squared_error = (x - y)**2 
  mean_squared_error = squared_error.mean() 
  return np.sqrt(mean_squared_error) 
  
  
# now we extend this using the @metric decorator 
@metric
def XCastRMSE(x, y): 
  return rmse(x, y) 
```

and an alternate way to do it in one step would be: 

```
from xcast import metric 

# this is the 2-dimensional function which calculates the RMSE between two NumPy Column Vectors.
# we also just extend this using the @metric decorator from the start

@metric
def XCastRMSE(x, y): 
  # x is Nx1, y is Nx1
  squared_error = (x - y)**2 
  mean_squared_error = squared_error.mean() 
  return np.sqrt(mean_squared_error) 
```

You could then use `XCastRMSE` on your `xarray.DataArray`s. 

There are a set of commonly-used skill metrics already implemented in XCast- some of them for deterministic forecasts, some for probabilistic. They are detailed in the table below (scroll to the right for links to more information) 

| 2D Function Name    | XCast Function Name    |     Intended Purpose     |    More information   |
| ------------------- | ---------------------- | ------------------------ | --------------------- |
| xcast.index_of_agreement  | xcast.IndexOfAgreement       |   Deterministic Forecasts (Nx1)  |     [link](https://agrimetsoft.com/calculators/Index%20of%20Agreement) [paper](https://www.researchgate.net/publication/235961403_A_refined_index_of_model_performance)        |
| xcast.kling_gupta_efficiency  | xcast.KlingGuptaEfficiency | Deterministic Forecasts (Nx1) |  [link](https://agrimetsoft.com/calculators/Kling-Gupta%20efficiency#) |
| xcast.rank_probability_score  | xcast.RankProbabilityScore | Probabilistic Forecasts (NxM) |  [link](https://stats.stackexchange.com/questions/112250/understanding-the-rank-probability-score#) |
| xcast.brier_score  | xcast.BrierScore | Probabilistic Forecasts (NxM) |  [link](https://en.wikipedia.org/wiki/Brier_score) |
| xcast.generalized_receiver_operating_characteristics_score | xcast.GROCS | Probabilistic Forecasts (NxM) | [link](https://iri.columbia.edu/wp-content/uploads/2013/07/scoredescriptions.pdf) | 
| xcast.logarithm_skill_score | xcast.LSS | Probabilistic Forecasts (NxM) | [link](https://www.researchgate.net/publication/317174540_Assessing_probabilistic_predictions_of_ENSO_phase_and_intensity_from_the_North_American_Multimodel_Ensemble/figures?lo=1) | 
| scipy.stats.pearsonr | xcast.Pearson | Deterministic Forecasts (Nx1) | [link](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.pearsonr.html) | 
| scipy.stats.spearmanr | xcast.Spearman | Deterministic Forecasts (Nx1) | [link](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.spearmanr.html) | 




