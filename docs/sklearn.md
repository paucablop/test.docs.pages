---
title: Sci-kit learn integration
layout: default
parent: Docs
nav_order: 1
---


# __Integration with scikit-learn__

## __Working with single spectra (1D arrays)__
Preprocessing techniques in scikit-learn are primarily designed to work with 2D arrays, where each row represents a sample and each column represents a feature (i.e., matrices). However, in spectroscopy, single spectra are often of interest, which are represented as 1D arrays (i.e., vectors). To apply scikit-learn and chemotools techniques to single spectra, they need to be reshaped into 2D arrays (i.e., a matrix with one row). To achieve this, you can use the following code that reshapes a 1D array into a 2D array with a single row:

```python
import numpy as np

from chemotools.scatter import MultiplicativeScatterCorrection

msc = MultiplicativeScatterCorrection()
spectra_msc = msc.fit_transform(spectra.reshape(1, -1))
```
The ```.reshape(1, -1)``` method is applied to the 1D array ```spectra```, which is converted into a 2D array with a single row.


## __Pipelines integration with scikit-learn__
All preprocessing techniques in this package are compatible with ```scikit-learn``` and can be used in pipelines. For example, the following code creates a pipeline that performs multiplicative scatter correction, followed by a min-max scaling and a Savitzky-Golay smoothing:

```python
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(AirPls(), MultiplicativeScatterCorrection(), StandardScaler(with_std=False)) 
spectra_transformed = pipeline.fit_transform(spectra)
```

<iframe src="figures/pipeline.html" width="800px" height="500px" style="border: none;"></iframe>