---
layout: page
title: Classifiers: POELM
permalink: /cpoelm/ 
--- 

# Classifiers: POELM 
### xc.cPOELM ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/estimators/classifiers.py#L74))

cPOELM is an XCast original implementation. Its underlying flat estimator is the Probabilistic-Output Extreme Learning Machine (POELM). POELM is essentially a randomized, un-trained neural network, which uses the Moore-Penrose pseudoinverse to solve a sigmoid objective function on the output layer. Three output neurons are fit, generally, one for each of the Above Normal, Below Normal, and Near Normal categories. Regularization is then used to ensure that the tercile probabilities always sum to one.
