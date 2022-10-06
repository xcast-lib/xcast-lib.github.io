---
layout: page 
title: Flat Estimators: Multivariate Extended Logistic Regression (MELR)
permalink: /multivariateelrclassifier/
---

# Flat Estimators: Multivariate Extended Logistic Regression (MELR)
### xc.MultivariateELRClassifier ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/flat_estimators/classifiers/elr.py#L41))

Multivariate ELR Classifier implements the a multivariate extended logistic regression model. Rather than fitting multiple Extended Logistic Regressions, then taking the mean, MELR fits a single Extended Logistic Regression, but uses all of the predictors at once. 

The standard Extended Logistic Regression proceeds by taking the X vector, making a copy, and stacking the two vertically, to double the number of samples. Then, an additional predictor field is constructed and stacked onto that horizontally, where the first half of the samples in the new field are the 33rd percentile value of the target vector, and the second half are the 66th percentile value of the target vector. The target vector, which started as continuous values, is then doubled, and stacked vertically so as to double the number of samples. The first half is then one-hot encoded, where a “1” indicates that a given sample did not exceed the 33rd percentile, and a “0” indicates that it did. The second half of the new target vector is then one-hot encoded similarly, but substituting the 66th percentile of the original target for the 33rd. A logistic regression is then fit with iteratively reweighted least squares. 

This method allows you to solve for a coefficient which determines the relationship between the forecasted probability, and a post-fit user-specified percentile value, which in turn lets the user make predictions of the full forecast PDF, given a new value of X. 

**Constructor**: 
Keyword Arguments: 
- preprocessing (default:’none’) - whether and how to preprocess the input x data - one of ‘none’, ‘minmax’, or ‘stdanomaly’ 
- verbose (default:False) - controls the verbosity of MELR Classifier
- thresholds (default: [0.33, 0.67]) - the thresholds on which to train the MELR instance (each represents a quantile threshold between 0-1. Each additional threshold you add increases the number of training samples in the regression by N, where N is the number of samples in X - they get stacked vertically as described above) 

**.fit** - fits the CCA estimator
Arguments: 
- x: an nxm numpy array with n samples and m features, serving as independent predictor variables.
- y: an nx1 numpy array with n samples of one continuous random variable serving as the dependent predictand.   

Keyword Arguments:
- None
	
Returns: 
- None

**.predict** - produces a categorical prediction based on the new x input data according to the fitted MELR model. Note that this is explicitly available for the tercile case. (so you will get 0, 1, or 2) 
 
Arguments: 
- x: a numpy array serving as new predictor variables. Must be the same shape as the x used for .fit , except for the number of samples. 

Keyword Arguments:
- None 

Returns: 
- preds: a numpy array with predictions for each new sample

**.predict_proba** - produces a probabilistic prediction based on the new x input data according to the fitted MELR model. This function produces tercile probabilities for BN/NN/AN by default, but if you pass the `quantile` keyword argument (set to something between 0 and 1, indicating a quantile threshold for the nonexceedance probability, or a list of them) you will get nonexceedance probabilities for each of the quantiles you pass.  
 
Arguments: 
- x: a numpy array serving as new predictor variables. Must be the same shape as the x used for .fit , except for the number of samples. 

Keyword Arguments:
- quantile (default:None) - if None, return tercile probabilities for AN/BN/NN categories. Else return an nx1 numpy array of nonexceedance probabilities (for each of the specified quantiles, stacked together horizontally to make an nxm array, where n is number of samples in x and m is the number of quantiles specified) 

Returns: 
- preds: an nx3 array with tercile category probabilities if quantile is None, else an nxm array with nonexceedance probabilities (where each of the m columns corresponds to one of the specified quantile nonexceedance thresholds in .predict_proba)

**.nonexceedance** - produces a nonexceedance probability prediction based on the new x input data according to the fitted MELR model.  
 
Arguments: 
- x: a numpy array serving as new predictor variables. Must be the same shape as the x used for .fit , except for the number of samples. 

Keyword Arguments:
- quantile (default:0.5) - the specified quantiles, for which to generate and stack together horizontally nonexceedance probability vectors to produce an nxm numpy array where m = len(list(quantile)) 

Returns: 
- preds: an nxm array with nonexceedance probabilities (where each of the m columns corresponds to one of the specified quantile nonexceedance thresholds in .predict_proba) 

**.exceedance** - returns 1-nonexceedance. All arguments forwarded to .nonexceedance(...)  
 
Arguments: 
- x: a numpy array serving as new predictor variables. Must be the same shape as the x used for .fit , except for the number of samples. 

Keyword Arguments:
- quantile (default:0.5) - the specified quantiles, for which to generate and stack together horizontally exceedance probability vectors to produce an nxm numpy array where m = len(list(quantile)) 

Returns: 
- preds: an nxm array with exceedance probabilities (where each of the m columns corresponds to one of the specified quantile exceedance thresholds in .predict_proba)
