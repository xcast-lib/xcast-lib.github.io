---
layout: page
title: LeaveOneYearOut
permalink: /LeaveOneYearOut/
---

# LeaveOneYearOuet

While the `CrossValidator` class implements Leave-N-Out cross-validation with a constant window size, in some contexts, this is not desirable. For example, during subseasonal forecasting when one has multiple samples per year, you don't want to leave out each sample in turn. If every year had the same number of samples, you could use the normal `CrossValidator` and set the window size, but often there are different numbers of samples in each year. `LeaveOneYearOut` solves this problem by leaving out all of the samples in in given calendar year at a time. 

`LeaveOneYearOut` needs to make some assumptions: 
- X and Y have exactly the same coordinates along their sample dimension
- Those coordinates are convertible to `pandas.Timestamp`

If your X and Y don't match, well, you need to fix that. Here, the left-out set of samples for a given year is of variable size and is represented by `xtest` and `ytest`. The remaining data, for every other year, on which the model should be trained at each iteration, is represented by `xtrain` and `ytrain`.

```
for xtrain, ytrain, xtest, ytest in xc.LeaveOneYearOut(X, Y): 
  # do some stuff within loop
```

Generally it is important to evaluate predictions and forecasts under cross-validation to prevent data-leakage and spurious high skill. If you compare predictions made for the samples that your model was trained on with observations (which the model was also trained on), you're going to see much higher skill than you would for samples the model hasn't seen before. Since in forecasting, we train predictive models on the available hindcast/observation pairs, and make predictions for future dates which have not been observed, we need a way of measuring how well the model generalizes to new data - cross validation. 

`LeaveOneYearOut` usualy should be used in conjunction with `RollingMinMax` to account for intraseasonal variability. 

For more detailed examples of cross-validation and skill metrics with xcast, please see the the [examples](github.com/kjhall01/xcast) 







