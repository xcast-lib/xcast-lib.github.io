---
layout: page
title: CrossValidator
permalink: /CrossValidator/
---

# CrossValidator

The CrossValidator class implements Leave-N-Out cross-validation. It is an iterator which, at each iteration, yields xtrain - the X data array without the period to be left out at that step, ytrain - the Y data array without the period to be left out at that step, xtest- the X data that is left out at that step, and ytest- the Y data that is left out at that step. The size of the window to be left out is determined by the window keyword. 
This is not exactly the same as K-Fold cross validation - there is no shuffling, and the left-out periods are sequential, and are allowed to overlap. 

Here, the left-out period is of size `window` and is represented by `xtest` and `ytest`. The remaining data, on which the model should be trained at each iteration, is represented by `xtrain` and `ytrain`.

```
for xtrain, ytrain, xtest, ytest in xc.CrossValidator(X, Y, window=1): 
  # do some stuff within loop
```

Generally it is important to evaluate predictions and forecasts under cross-validation to prevent data-leakage and spurious high skill. If you compare predictions made for the samples that your model was trained on with observations (which the model was also trained on), you're going to see much higher skill than you would for samples the model hasn't seen before. Since in forecasting, we train predictive models on the available hindcast/observation pairs, and make predictions for future dates which have not been observed, we need a way of measuring how well the model generalizes to new data - cross validation. 

For more detailed examples of cross-validation and skill metrics with xcast, please see the the [examples](https://github.com/kjhall01/xcast)







