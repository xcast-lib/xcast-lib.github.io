---
layout: page 
title: Skill Metrics in XCast
permalink: /metric/ 
---

# Metric Decorator
### xc.metric ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/verification/base_verification.py#L65)) 

After BaseEstimator, metric is probably the second most important thing in XCast. It is the driver behind all of XCast’s skill metrics, similar to how BaseEstimator is the driver behind all of XCast’s estimators. 

Since Python functions cannot “subclass” another function, metric is implemented as a function “decorator” - meaning it is a function that takes a function as input, and returns a modified version of that function under the same name. 

It even has a special syntax in Python, as of like Python 3.6: 

```
@metric
def my_skill(x, y): # where x and y are both numpy arrays
	return np.mean((x-y)**2)
```

Ta-da - now even though you wrote my_skill as a metric for a single gridpoint, ie, x and y are two numpy arrays, after decoration with the @metric decorator, my_skill will accept and produce xarray dataarrays (where your original my_skill function was applied at each grid point!) 

Any function decorated with @metric will use the following set of args, kwargs, and return values. The caveat is that, the function decorated MUST accept two NxM numpy arrays, and return a single floating point number (think , correlation coefficient comes from two vectors )

**arguments**
- X: an xarray data array conforming to xcast dimensionality conventions
- Y: an xarray data array conforming to xcast dimensionality conventions, and compatible with X for the purposes of the underlying function. 

**keyword arguments** 
- guess coords kwargs for x and y 
- kwargs to be forwarded to the underlying function 

**returns**
- ret: an xarray dataarray which contains the skill score calculated by the underlying function .


XCast has a TON of skill metrics. please refer to [this document](https://github.com/xcast-lib/xcast-lib.github.io/blob/2af918a65059510f948c8bb96ff0405bf33b373f/xcast_metrics.pdf) for more information! 
