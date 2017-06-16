---
layout: page
title: Projects
permalink: /projects/
---

## Non-Convex Optimization for Large-Scale Embedded Feature Selection in Classification 
We provide a demo of the parallel majorization-minimization algorithm for non-convex optimization in machine learning 
that was published in [1] (see also slides here [2]). Code is avaliable here: https://github.com/yankagan/PMM-DRD.

We proposed an optimization framework for nonconvex problems based on majorization-minimization that is particularity well-suited for cases when the number of features/parameters is very large. The original problem is broken into smaller parallel sub-problems while still guaranteeing the monotonic reduction of the original objective function and convergence to a local minimum. Due to the low dimensionality of each sub-problem, second-order optimization methods become computationally feasible and can be used to accelerate convergence. 

The advantages of this algorithm over other gradient-based methods for non-convex optimization (e.g., Gradient Descent, LBFGS, RMS-Prop, ADAGRAD) are as follows:

(1) No tuning of learning rates required
(2) Scale invariance (similar to 2nd order methods but without using the Hessian)
(3) Highly parallel - the parameters are split into small groups that can be processed in parallel 
(4) Cost function guarenteed to decrease monotonically (any increase is an indication of a bug) without any expensive line searches

Although the framework in [1] address a wide range of cost functions in the generalized linear model family, the current code only supports two specific models: sigmoid-loss SVM and logistic regression with logarithmic penalty (for promoting stronger sparsity). We hope to make the code more general in the future.

### References
1. Y. Kaganovsky, I. Odinaka, D. Carlson, and L. Carin, Parallel Majorization Minimization with Dynamically Restricted Domains for Nonconvex Optimization, Journal of Machine Learning Research W&CP Vol. 51: Proc 19th conference on Artificial Intelligence and Statistics (AISTATS) 2016.
2.  Y. Kaganovsky, Non-Convex Optimization Made Simpler, presented at Amazon, Seattle, June 2016.

## Image Reconstruction for Computed Tomography
We provide a demo of the VARD algorithm for image reconstruction in transmission tomography under Poisson noise [1].
We consider x-ray computed tomography (CT), but the algorithm applies more generally, e.g., it can be used for electron 
tomography.  VARD stands for Variational Automatic Relevance Determination and it is an extension of Automatic Relevance 
Determination (ARD) [2,3] to Poisson noise models with Beer's law. 

The key advantage of ARD or VARD is the lack of any tuning parameters. Typically, in penalized likelihood algorithms, 
one has to choose values for tuning parameters that control the balance between data-fit and the penalty due to 
prior knowledge (common choices are the l1 and TV penalties). One is then forced to perform many trials for different 
values of parameters and to choose the values by trial-and-error.

VARD uses a prior that promotes sparsity in the pixel/voxel differences domain and the weight of the prior 
relative to the data-fit is determined automatically from the data. VARD saves the agonizing pain of choosing values
for the tuning parameters; it can also save a lot of time spend on this task.

The demo is available here: https://github.com/yankagan/VARD-for-CT. We compare VARD to the maximum likelihood estimator in [4] and also to a penalized likelihood estimator [1].  
All the algorithms in the demo use separable surrogates which reduce the algorithms to parallel line searches, 
making them feasible for large scale problems such as x-ray CT.

The algorithms can be sped up considerably using various techniques (e.g., using a better initialization, ordered subsets) 
but these are not considered here.

### References
1. Y. Kaganovsky, S. Han, S. Degirmenci, D. G. Politte, D. J. Brady, J. A. O'Sullivan and L. Carin, Alternating Minimization Algorithm with Automatic Relevance Determination for Transmission Tomography under Poisson Noise,  SIAM Journal on Imaging Sciences, 8(3), 2015.  
2. R. M. Neal, Bayesian Learning for Neural Networks, PhD Thesis, 1995. 
3. M. E. Tipping, Sparse Bayesian Learning and the Relevance Vector Machine, Journal of Machine Learning Research, 2001. 
4. J. A. O'Sullivan and J. Benac, Alternating Minimization Algorithm for Transmission Tomography, IEEE Trans. on Medical Imaging, 2007.
