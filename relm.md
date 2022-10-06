---
layout: page
title: Regressors: Extreme Learning Machine 
permalink: /rextremelearningmachine/ 
---

# Regressors: Extreme Learning Machine 
### xc.rExtremeLearningMachine ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/estimators/regressors.py#L125)) 

rExtremeLearningMachine is an XCast original implementation of the Extreme Learning Machine regression model. It’s basically a randomly initialized, un-trained neural network which uses the Moore-Penrose Generalized Inverse (which is very similar to if not the same as OLS) to fit a linear relationship between its hidden nodes and target vector. 
