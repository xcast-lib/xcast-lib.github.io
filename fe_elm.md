---
layout: page
title: Flat Estimators: Extreme Learning Machine
permalink: /elmregressor/ 
---

# Flat Estimators: Extreme Learning Machine
### xc.ELMRegressor ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/flat_estimators/regressors/elm.py#L12)) 

ELMRegressor is an XCast original implementation of the Extreme Learning Machine regression model. It’s basically a randomly initialized, un-trained neural network which uses the Moore-Penrose Generalized Inverse (which is very similar to if not the same as OLS) to fit a linear relationship between its hidden nodes and target vector.

**Constructor**: 
Keyword Arguments: 
- preprocessing (default:’none’) - whether and how to preprocess the input x data - one of ‘none’, ‘minmax’, or ‘stdanomaly’ 
- verbose (default:False) - controls the verbosity of ELR Classifier
- **kwargs- other kwargs are forwarded to MultivariateELRClassifier
- activation (default:'sigm') - activation function to use on hidden nodes
- hidden_layer_size (default:5) - number of neurons to use in hidden layer

**.fit** - fits the ELM estimator
Arguments: 
- x: an nxm numpy array with n samples and m features, serving as independent predictor variables.
- y: an nx1 numpy array with n samples of one continuous random variable serving as the dependent predictand.   

Keyword Arguments:
- None
	
Returns: 
- None

**.predict** - produces a continuous prediction based on the new x input data according to the fitted ELM model. 
 
Arguments: 
- x: a numpy array serving as new predictor variables. Must be the same shape as the x used for .fit , except for the number of samples. 

Keyword Arguments:
 - None 

Returns: 
- preds: a numpy array with predictions for each new sample
