---
layout: page
title: RollingOneHotEncoder
permalink: /RollingOneHotEncoder/
---

# RollingOneHotEncoder

The RollingOneHotEncoder class applies one-hot encoding to sub-seasonal data based on a "rolling window" of user-specified width. One should not use the standard OneHotEncoder class on data with multiple samples per year from a given season because, for example, when encoding two-week aggregated data from the NDJFM season, February and March values could follow entirely different distributions than November and December values. The 66th percentile could be purely determined by the intra-seasonal variability, making the one-hot encodings somewhat nonsensical. The Rolling One-Hot Encoder accounts for this by doing the one-hot encoding separately at each week-in-year, plus/minus the window size. So rather than one-hot encoding seeing all the February values as the highest, it will encode those separately from the other periods within the NDJFM season, based on the 66th percentile of the February values only. The specific time period used to determine the thresholds is defined by the window size in days specified by the user, centered at each sample. Each sample is encoded separately based on this window centered around it. For this reason, xarray.DataArrays passed to RollingOneHotEncoder must have sample-dimension coordinates convertible to pandas.Timestamp. Once instantiated, you need to fit a `RollingOneHotEncoder` on an xarray.DataArray, X, which should have the four dimensions expected by XCast (see [data in xcast](https://xcast-lib.github.io/data/)). After fitting, these objects can then be used to one-hot encode data formatted like `X`.  

For this class, data arrays like `X` must have coordinates along the sample dimension which are convertible to pandas.Timestamp. The difference between this class and the standard one-hot encoder class is that this class will separately one-hot encode each sample along the sample dimension. It will take any samples which, for any calendar year, fall into the day-in-year range defined by ( the coordinate of the given sample (say, initialization of June 1) plus `lead_low` (by default this is -7 to reflect one-week-prior to that sample in the year), and the coordinate of the given sample (say, initialization of June 1) plus `lead_high` (by default this is 7 to reflect one-week-post that sample in the year)

```
rohc = xc.RollingOneHotEncoder(
  lead_low=-7,  # defines the number of days prior to an initialization date to include in the one-hot-encoding window 
  lead_high=7,  # defines the number of days post- an initialization date to include in the one-hot encoding window
  base_year=1999, # first year to search - make sure all your data falls between 1/1/base_year and 12/31/(base_year+n_years_to_search) 
  n_years_to_search=30
)
rohc.fit(X) 
T = rohc.transform(X) # this could be X1, a dataset from a different year of the same format as X. T will have three features - one representing 'Below Normal (~1-33rd percentiles, one for 'Near Normal' (~34-66 percentiles), and one for 'Above Normal' (~67-99th percentiles) 
```

While no XCast estimators (as of v1.0.0) require One-Hot Encoded training data, `RollingOneHotEncoder` is still used to transform observations for the sake of comparison. Many of XCast's metrics require one-hot encoded observation data for comparison with probabilistic forecasts. 






