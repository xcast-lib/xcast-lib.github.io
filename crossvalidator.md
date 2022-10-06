---
layout: page
title: Validation: Cross Validator
permalink: /crossvalidator/
---

# Validation: Cross Validator
### xc.CrossValidator ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/validation/base_validation.py#L9) )

CrossValidator efficiently implements leave-N-out crossvalidation for XCast workflows. Generally, it is unreliable to trust skill scores derived from forecasts made for data on which the models were trained- so one should generally do things under some sort of cross-validation.

This means, in pseudocode: 

```
Out-of-sample predictions = []
For each sample in the dataset: 
	Train model on all samples that arent the current sample
	Make predictions for the current sample 
	Append prediction to out-of-sample predictions 

Re-assemble a dataset from all of the out of sample predictions
Compare that dataset to the original observations
```

However, XCast’s Crossvalidator class lets you control the size of the window, and the stepsize between iterations - so you can effectively make it ‘leave-whatever-you-want-out’ cross validation if you get the indices right. 

Here is a usage example, because its a little tricky compared to other things in XCast: 

```
import xcast as xc 
X, Y, T = xc.load_sample_data() 

poelm_xval = []
for x_train, y_train, x_test, y_test in xc.CrossValidator(X, Y, window=3, step=3):
    ohc = xc.RankedTerciles()
    ohc.fit(y_train)
    ohc_y_train = ohc.transform(y_train)
    
    poelm = xc.cPOELM()
    poelm.fit(x_train, ohc_y_train)
    poelm_preds = poelm.predict_proba(x_test)
    poelm_xval.append(poelm_preds.isel(S=cross_validation_window // 2))
    
poelm_hindcasts = xr.concat(poelm_xval, 'S').mean('ND')
```

As you can see, CrossValidator is an iterator - you loop over it in order to access each of the train-test splits in succession. 

**Constructor**
Arguments:
- X: An Xarray DataArray conforming to the XCast Dimensionality Conventions
- Y: An Xarray DataArray, conforming to the XCast Dimensionality Conventions (and matching X in its size along the samples, latitude, and longitude dimensions) 

Keyword Arguments: 
- window (default:3) - the size of the crossvalidation window (meaning, leave this many out - those n will be in the x_test/y_test variables)  (must be odd) 
- step (default: 1) - the size of the step to move the center of the cross validation window by each time- if step == window, you should leave out each of the samples exactly one time.)
- ** guess coords kwargs for x and y  

