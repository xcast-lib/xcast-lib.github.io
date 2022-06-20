---
layout: page
title: Documentation: Cross-Validation
permalink: /crossvalidation/ 
---

# Documentation: Cross-Validation
K-Fold crossvalidation is a common way of validating data science methodologies. In XCast, we have implemented a Leave-N-Samples-Out crossvalidator which allows you to split your training data into ```xtrain```, ```ytrain```, ```xtest```, and ```ytest``` by simply passing your full datasets to the ```xc.CrossValidator``` iterator class. the Crossvalidator accepts dimension name keywords. 

```
import xarray as xr 
import xcast as xc 

nmme, india, T = xc.NMME_IMD_ISMR() # load test data 

poelm_xval = [] # place to put cross-validated predictions, to reassemble hindcast dataset 
crossvalidation_window = 5 # number of samples to leave out 

# initiate cross validation loop with CrossValidator class
for x_train, y_train, x_test, y_test in xc.CrossValidator(nmme, india, window=cross_validation_window):

    # Do all your preprocessing, training, and predicting within cross-validation 
    ohc = xc.RankedTerciles()
    ohc.fit(y_train)
    ohc_y_train = ohc.transform(y_train)
    
    poelm = xc.cPOELM()
    poelm.fit(x_train, ohc_y_train)
    poelm_preds = poelm.predict_proba(x_test)
    # put cross-validated prediction into poelm_xval
    poelm_xval.append(poelm_preds.isel(S=cross_validation_window // 2))
    
poelm_hindcasts = xr.concat(poelm_xval, 'S').mean('ND')
```
