---
layout: page
title: Docs: Estimators
permalink: /estimators/
---

# Docs: XCast Estimators 

XCast estimators are objects which represent gridpoint-wise local statistical and machine learning models. Similar to those of Scikit-Learn, they implement ```.fit``` and ```.predict``` methods. (also ```.predict_proba```). Generally, their methods all accept dimension name keyword arguments to accomodate different data arrays.
Keyword arguments passed to the constructor of an XCast estimator are forwarded to the underlying 2D estimator object which is wrapped. So if I wanted to make an sklearn.neural_network.MLPRegressor with hidden_layer_sizes=(100,100), I would simply pass hidden_layer_sizes=(100, 100) to XCast, and it would be forwarded automatically. 

Generally, the names of regressors are preceded by the letter 'r', and the names of classifiers are preceded by the letter 'c'. For now, XCast classifiers have the ```.predict_proba``` method, but only implement tercile probabilities. See the 'citing xcast' page for a link to the full article on XCast for more detail.

### Regressors: 

```
import xcast as xc 
X, Y, T = xc.NMME_IMD_ISMR() # load test data 

em = xc.EnsembleMean()
em.fit(X, Y)
pred = em.predict(X) # gives deterministic forecast 

bcem = xc.BiasCorrectedEnsembleMean()
bcem.fit(X, Y) 
pred = bcem.predict(X) 

mlr = xc.rMultipleLinearRegression()
mlr.fit(X, Y)
pred = mlr.predict(X) 

poisson = xc.rPoissonRegression()
poisson.fit(X, Y) 
pred = poisson.predict(X) 

gamma = xc.rGammaRegression() 
gamma.fit(X, Y) 
pred = gamma.predict(X) 

mlp = xc.rMultiLayerPerceptron() 
mlp.fit(X, Y) 
pred = mlp.predict(X) 

rf = xc.rRandomForest() 
rf.fit(X, Y) 
pred = rf.predict(X) 

ridge = xc.rRidgeRegression() 
ridge.fit(X, Y) 
pred = ridge.predict(X) 

elm = xc.rExtremeLearningMachine() 
elm.fit(X, Y) 
pred = elm.predict(X) 
```


### Classifiers: 

```
import xcast as xc 
X, Y, T = xc.NMME_IMD_ISMR() # load test data 

elr = xc.cExtendedLogisticRegression()
elr.fit(X, Y) # ELR is fit on continuous Y data
pred = elr.predict_proba(X) 

mlp = xc.cMultiLayerPerceptron() 
mlp.fit(X, T) # one hot encoded Y data
pred = mlp.predict_proba(X) 

rf = xc.cRandomForest() 
rf.fit(X, T) # one-hot encoded Y data 
pred = rf.predict_proba(X) 

nb = xc.cNaiveBayes() 
nb.fit(X, T) # one-hot encoded Y data 
pred = nb.predict_proba(X) 

poelm = xc.cPOELM() 
poelm.fit(X, T) # one-hot encoded Y data 
pred = elm.predict_proba(X) 
```

## Extending XCast with a New Model Type: 
XCast makes it easy to implement new gridpoint-wise statistical models. Say for example you wanted to implement XGBoostRegressor or XGBoostClassifier: 

```
import xcast as xc 
import xgboost as xg 

# regressor! 
class rXGboost(BaseEstimator):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.model_type = xg.XGBoostRegressor

xgb = xc.rXGboost() 
xgb.fit(X, Y) 
pred = xgb.predict(X) 


# Classifier!
class cXGboost(BaseEstimator):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.model_type = xg.XGBoostClassifier

xgb = xc.cXGboost() 
xgb.fit(X, T) 
pred = xgb.predict_proba(X) 
``` 

The only trick to this is to make sure that the arguments to XGBoostRegressor/XGBoostClassifier conform to the same shape as scikit-learn regressors / classifiers- two dimensional vectors with the samples in the first dimension. So you might need to implement a simple 2D wrapper class which resahpes the arguments. But that's not so bad! 




