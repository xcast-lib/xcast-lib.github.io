---
layout: page
title: Ensemble
permalink: /Ensemble/
---

# Ensemble

Ensemble is an XCast estimator which implements the basic ensemble forecasting methods, Ensemble Mean and Member Counting. It can produce both deterministic forecasts (Ensemble Mean) and tercile probabilistic forecasts (Member Counting). It is best used with the individual members of a given climate model, rather than as a multi-model ensemble method.   

Ensemble is not implemented as a subclass of BaseEstimator, but rather directly with Xarray operations. There are no hyperparameters to be tuned, as in EPO-ELM or other methods. `.fit` will fit both Member Counting and Ensemble mean (not that ensemble mean really requires 'fitting' in the normal sense, but you still need to do it here). `.predict` will return the ensemble mean, and `.predict_proba` will return the member count tercile forecast. It cannot be used for probabilty of non-exceedance predictions. 

Ensemble is mostly included in XCast for the sake of benchmark comparisons, as a drop-in replacement for EPO-ELM, QRF, and other things we want to compare it to. 
