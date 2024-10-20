# Python Code for Inverse M-Kernels 
This library provides linear universal approximators of non-negative functions with inverse M-kernels. For details, see our NeurIPS2024 paper [1].

The code was tested on Python 3.10.8.

# Installation
~~To install latest version:~~ Under construction!
```
pip install git+https://github.com/HidKim/IM-Kernel
```

# Basic Usage
Import SurvPP class:
```
from HidKim_SurvPP import survival_permanental_process as SurvPP
```
Initialize SurvPP:
```
model = SurvPP(kernel='Gaussian', eq_kernel='RFM', eq_kernel_options={'n_rfm':500})
```
- `kernel`: *string, default='Gaussian'* <br> 
  >The kernel function for Gaussian process. Only 'Gaussian' is available now.
- `eq_kernel`:  *string, default='RFM'* <br>
  >The approach to constructing equivalent kernel. Only 'RFM' is available now.  
- `eq_kernel_options`:  *dict, default={'n_rfm':500}* <br>
  >The options for constructing equivalent kernel. `'n_rfm'` specifies the number of feature samples for the random feature map approach to constructing equivalent kernel.
  
Fit SurvPP with data:
```
time = model.fit(formula, df, set_par, lr=0.05, display=True)
```
- `formula`: *string in the form 'Surv(Start, Stop, Event) ~ cov1 + cov2 + ...'* <br> 
  >Identify the column labels of start time (Start), stop time (Stop), event indicator (Event, 1 represents that an event occurred at stop time, and 0 represents that observation is right-censored), and covariates used for survival analysis.
- `df`:  *pandas.DataFrame*  <br>
  > The survival data in counting process format. Each row represents a sub-interval for a subject, and should contain start and end time points, event indicator (0/1), and values of covariates in the sub-interval.  
- `set_par`:  *ndarray of shape (n_candidates, dim_hyperparameter)*  <br>
  >The set of hyper-parameters for hyper-parameter optimization. The optimization is performed by maximizing the marginal likelihood.
- `lr`: *float, default=0.05* <br>
  >The learning rate for gradient descent algorithm (Adam).
- `display`:  *bool, default=True*  <br>
  >Display the summary of the data and the fitting. 
- **Return**: *float* <br>
  >The execution time.

Predict hazard function on specified covariate values:
```
r_est = model.predict(y, conf_int=[0.025,0.5,0.975])
```
- `y`: *ndarray of shape (n_points, dim_covariate)* <br> 
  >The points on covariate domain for evaluating intensity values.
- `conf_int`:  *ndarray of shape (n_quantiles,), default=[.025, .5, .975]*  <br>
  > The quantiles for predicted hazard function.
- **Return**: *ndarray of shape (n_quantiles, n_points)* <br>
  >The predicted values of hazard function at the specified points.

# Reference
1. Hideaki Kim. "Inverse M-Kernels for Linear Universal Approximators of Non-Negative Functions", *Advances in Neural Information Processing Systems 37*, 2024.
```
@inproceedings{kim2024inversem,
  title={Inverse M-Kernels for Linear Universal Approximators of Non-Negative Functions},
  author={Kim, Hideaki},
  booktitle={Advances in Neural Information Processing Systems 37},
  year={2024}
}
``` 

# License
Released under "SOFTWARE LICENSE AGREEMENT FOR EVALUATION". Be sure to read it.

# Contact
Feel free to contact the author Hideaki Kim (hideaki.kin@ntt.com).