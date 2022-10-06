---
layout: page
title: Classifiers: cMemberCount
permalink: /cmembercount/
---

# Classifiers: Member Count
### xc.cMemberCount  ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/estimators/classifiers.py#L11))

cMemberCount is one of the few XCast estimators that isn’t implemented by BaseEstimator - it is an xcast original - but that doesn’t change any of the signatures of its .fit, .predict, or .predict_proba methods. 

cMemberCount is designed to analyze a dataset representing all of the members of a given climate model - it stacks all of the members (represented on the feature dimension) along one axis, then finds the 33rd and 66th percentile across the sample and feature dimensions, and uses those to ‘one-hot encode’ the forecasts of each of the ensemble members - the forecasts are then averaged to produce probabilistic tercile category forecasts.
