---
layout: page
title: Flat Estimators: Probabilistic Output Extreme Learning Machine (POELM) 
permalink: /poelmclassifier/
---

# Flat Estimators: Probabilistic Output Extreme Learning Machine (POELM) 
### xc.POELMClassifer ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/flat_estimators/classifiers/poelm.py#L12))

cPOELM is an XCast original implementation. POELM is essentially a randomized, un-trained neural network, which uses the Moore-Penrose pseudoinverse to solve a sigmoid objective function in the output layer. Three output neurons are fit, generally, one for each of the Above Normal, Below Normal, and Near Normal categories. Regularization is then used to ensure that the tercile probabilities always sum to one.

**Constructor**: 
Keyword Arguments: 
- preprocessing (default:’none’) - whether and how to preprocess the input x data - one of ‘none’, ‘minmax’, or ‘stdanomaly’ 
- verbose (default:False) - controls the verbosity of ELR Classifier
- **kwargs- other kwargs are forwarded to MultivariateELRClassifier
- activation (default:'sigm') - activation function to use on hidden nodes
- hidden_layer_size (default:5) - number of neurons to use in hidden layer

**.fit** - fits the POELM estimator
Arguments: 
- x: an nxm numpy array with n samples and m features, serving as independent predictor variables.
- y: an nx3 numpy array with n samples of tercile-category one-hot encoded versions of one continuous random variable serving as the dependent predictand.   

Keyword Arguments:
- None
	
Returns: 
- None

**.predict** - produces a categorical prediction based on the new x input data according to the fitted POELM model. Note that this is explicitly available for the tercile case. (so you will get 0, 1, or 2) 
 
Arguments: 
- x: a numpy array serving as new predictor variables. Must be the same shape as the x used for .fit , except for the number of samples. 

Keyword Arguments:
- None 

Returns: 
- preds: a numpy array with predictions for each new sample

**.predict_proba** - produces a probabilistic prediction based on the new x input data according to the fitted POELM model. This function produces tercile probabilities for BN/NN/AN.  
 
Arguments: 
- x: a numpy array serving as new predictor variables. Must be the same shape as the x used for .fit , except for the number of samples. 

Keyword Arguments:
- None

Returns: 
- preds: an nx3 array with tercile category probabilities
