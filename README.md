# Code for Bayesian Causal Forest with Instrumental Variable

In this repository we provide the code for the _BCF-IV_ and _BCF-ITT_ functions and for the application and simulations' Sections of the paper <a href="https://arxiv.org/abs/1905.12707"> _"Heterogeneous causal effects with imperfect compliance: a novel Bayesian machine learning approach"_ </a> by F.J. Bargagli-Stoffi, K. De Witte and G. Gnecco. 

The _BCF-IV_ function discovers and estimates, in an interpretable manner, the effects heterogeneity in settings where the assignment mechanism is irregular (e.g., instrumental variable and fuzzy regression discontinuity scenarios). This function is directly built to discover and estimate the heterogeneity in the Complier Average Treatment Effects (CACE). The _BCF-ITT_ function discovers the heterogeneity in the intention-to-treat (ITT) and then estimates the effect both for the conditional ITT and the conditional CACE for the discovered subgroups.

# BCF-IV function

The function takes as inputs:

* <tt>`y`</tt>: the outcome variable;
* <tt>`w`</tt>: the reception of the treatment variable (binary);
* <tt>`z`</tt>: the assignment to the treatment variable (binary);
* <tt>`max_depth`</tt>: the maximal depth of the tree generated by the function;
* <tt>`n_burn`</tt>: the number of iterations discarded by the BCF-IV algorithm for the burn-in;
* <tt>`n_sim`</tt>: the number of iterations used by the BCF-IV algorithm  to get the posterior distribution of the estimands;
* <tt>`inference_ratio`</tt>: the ratio of observations to be assigned to the interence subsample;
* <tt>`binary`</tt>: this option should be set to <tt>`TRUE`</tt> when the outcome variable is binary and to <tt>`FALSE`</tt> if the outcome variable is either discrete or continuous.

The _bcf_iv_ function returns the discovered sub-population, the conditional complier average treatment effect (CCACE), the p-value for this effect, the p-value for a weak-instrument test, the proportion of compliers, the conditional intention-to-treat effect (CITT) and the proportion of compliers in the node.

# BCF-ITT function

The function takes as inputs:

* <tt>`y`</tt>: the outcome variable;
* <tt>`w`</tt>: the reception of the treatment variable (binary);
* <tt>`z`</tt>: the assignment to the treatment variable (binary);
* <tt>`max_depth`</tt>: the maximal depth of the tree generated by the function;
* <tt>`n_burn`</tt>: the number of iterations discarded by the BCF-IV algorithm for the burn-in;
* <tt>`n_sim`</tt>: the number of iterations used by the BCF-IV algorithm  to get the posterior distribution of the estimands;
* <tt>`inference_ratio`</tt>: the ratio of observations to be assigned to the interence subsample;
* <tt>`binary`</tt>: this option should be set to <tt>`TRUE`</tt> when the outcome variable is binary and to <tt>`FALSE`</tt> if the outcome variable is either discrete or continuous.

The _bcf_itt_ function returns the discovered sub-population, the conditional complier average treatment effect (CCACE), the conditional intention-to-treat (CITT), the p-value for this effect, the p-value for a weak-instrument test, the proportion of compliers, the conditional intention-to-treat effect (CITT) and the proportion of compliers in the node.

# Example usage

```R
source("bcf-iv.R")

bcf_iv(y, w, z, x, max_depth = 2, n_burn = 2000, n_sim = 2000, inference_ratio = 0.50, binary = TRUE)

bcf_itt(y, w, z, x, max_depth = 2, n_burn= 2000, n_sim = 2000, inference_ratio = 0.50, binary = TRUE)
```

#### References
* Falco J. Bargagli-Stoffi, Kristof De Witte, Giorgio Gnecco. <b>Heterogeneous causal effects with imperfect compliance: a novel Bayesian machine learning approach.</b> [<a href="https://arxiv.org/abs/1905.12707">link</a>]
* P. Richard Hahn, Jared S. Murray, Carlos Carvalho. <b>Bayesian regression tree models for causal inference: regularization, confounding, and heterogeneous effects.</b> [<a href="https://arxiv.org/abs/1706.09523">link</a>]

