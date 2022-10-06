---
layout: page 
title: Flat Estimators: Extended Logistic Regression (ELR) 
permalink: /elrclassifier/
---

# Flat Estimators: Extended Logistic Regression (ELR) 
### xc.ELRClassifier ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/flat_estimators/classifiers/elr.py#L7))

ELR Classifier implements the ensemble mean Extended Logistic Regression (ELR) methodology. Ensemble Mean ELR proceeds by individually fitting an Extended Logistic Regression model on each of the predictor fields, and then taking an ensemble average of their predictions to be the prediction of the estimator. Note that its performance (speed of fitting) scales poorly with increases in the number of predictors.

**Constructor**: 
Keyword Arguments: 
- preprocessing (default:’none’) - whether and how to preprocess the input x data - one of ‘none’, ‘minmax’, or ‘stdanomaly’ 
- verbose (default:False) - controls the verbosity of ELR Classifier
- **kwargs- other kwargs are forwarded to MultivariateELRClassifier

**.fit** - fits the CCA estimator
Arguments: 
- x: an nxm numpy array with n samples and m features, serving as independent predictor variables.
- y: an nx1 numpy array with n samples of one continuous random variable serving as the dependent predictand.   

Keyword Arguments:
- None
	
Returns: 
- None

**.predict** - produces a categorical prediction based on the new x input data according to the fitted ELR ensemble model. Note that this is explicitly available for the tercile case. (so you will get 0, 1, or 2) 
 
Arguments: 
- x: a numpy array serving as new predictor variables. Must be the same shape as the x used for .fit , except for the number of samples. 

Keyword Arguments:
- None 

Returns: 
- preds: a numpy array with predictions for each new sample

**.predict_proba** - produces a probabilistic prediction based on the new x input data according to the fitted ELR ensemble model. This function produces tercile probabilities for BN/NN/AN by default, but if you pass the `quantile` keyword argument (set to something between 0 and 1, indicating a quantile threshold for the nonexceedance probability, or a list of them) you will get nonexceedance probabilities for each of the quantiles you pass.  
 
Arguments: 
- x: a numpy array serving as new predictor variables. Must be the same shape as the x used for .fit , except for the number of samples. 

Keyword Arguments:
- quantile (default:None) - if None, return tercile probabilities for AN/BN/NN categories. Else return an nx1 numpy array of nonexceedance probabilities (for each of the specified quantiles, stacked together horizontally to make an nxm array, where n is number of samples in x and m is the number of quantiles specified) 

Returns: 
- preds: an nx3 array with tercile category probabilities if quantile is None, else an nxm array with nonexceedance probabilities (where each of the m columns corresponds to one of the specified quantile nonexceedance thresholds in .predict_proba) 
