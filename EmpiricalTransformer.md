---
layout: page
title: EmpiricalTransformer
permalink: /EmpiricalTransformer/
---

# EmpiricalTransformer

The `EmpiricalTransformer` class transforms a dataset by first converting it to its corresponding percentiles along the sample dimension, and then converting those percentiles corresponding Z-scores along the gaussian normal distribution. It is intended to make data fit gaussian assumptions better. 

```
emp = xc.EmpiricalTransformer()
emp.fit(X) 
Xe = emp.transform(X) # this could be X1, a dataset from a different year of the same format as X.
```

Empirical Transformers let you coerce your data into fitting gaussian assumptions a little better, but generally are slow, don't work perfectly, and aren't recommended. There are better ways to address non-gaussian data sets.





