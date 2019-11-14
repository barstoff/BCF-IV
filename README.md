# Code for the paper "Heterogeneous causal effects with imperfect compliance: a novel Bayesian machine learning approach" by F.J. Bargagli-Stoffi, K. De Witte and G. Gnecco

In this repository we provide the code for the BCF-IV function and for the application part of the paper.

# BCF-IV function

\par The function takes as inputs:

* <tt>`y</tt>`: the outcome variable;
\item \texttt{w}: the reception of the treatment variable (binary);
\item \texttt{z}: the assignment to the treatment variable (binary);
\item \texttt{max\_depth}: the maximal depth of the tree generated by the function;
\item \texttt{n\_burn}: the number of iterations discarded by the \texttt{BCF} algorithm for the \textit{burn-in};
\item \texttt{n\_sim}: the number of iterations used by the \texttt{BCF} algorithm  to get the posterior distribution of the estimands;
\item \texttt{binary}: this option should be set to \texttt{TRUE} when the outcome variable is binary (i.e., $y \in \{0,1\}$) and to \texttt{FALSE} if the outcome variable is either discrete or continuous\footnote{The default ofption is \texttt{binary = FALSE.}}.
\end{itemize}

# Probit BCF-IV

The default BCF algorithm by Hahn et al. (2017) is implemented just for continuous outcomes. However, Chipman et al. (2010) and Starling et al. (2019) propose probit versions of the BART and BCF algorithms, respectively, to handle binary outcomes.  The new algorithm is described in detail in the following.
\par The original BCF-IV objective function that we propose is the following:
\begin{equation} \label{iv-bart}
    y_i = \mu(x_i, \hat{\pi}(x_i)) + ITT_{Y}(x_i)\cdot z_i.
\end{equation}
If we let $y$ be a Gaussian latent variable, then, following the original BART paper by Chipman et al. (2010) and the recent paper by Starling et al. (2019):
\begin{equation}
    P(y_i=1|z_i, x_i)= \phi(\mu(x_i, \hat{\pi}(x_i)) + ITT_{Y}(x_i)\cdot z_i),
\end{equation}
where $\phi$ is the standard normal CDF.
Hence, the counterfactual probabilities are:
\begin{eqnarray}
\omega_i(0) &=& \phi(\mu(x_i, \hat{\pi}(x_i))) \\
\omega_i(1) &=& \phi(\mu(x_i, \hat{\pi}(x_i)) + ITT_{Y}(x_i)\cdot z_i),
\end{eqnarray}
and $y_i \in {0,1}$ is:
\begin{equation}
   y_i= \begin{cases} 1 \text{ if } P(y_i=1|z_i, x_i) \geq 0.5 \\
   0 \text{ if } P(y_i=1|z_i, x_i) < 0.5.
    \end{cases}
\end{equation}

# Method-of-Moments BCF-IV

In the original \texttt{BCF-IV} algorithm we implement an IV estimator that runs a 2SLS that controls for the covariates in any single node. In order to reproduce the IV method-of-moments estimator described in the paper (and in order to get the estimation of ITT and the complier subpopulations) we implemented the \texttt{mm\_bcf\_iv} algorithm that is the 2SLS equivalent of the method-of-moment estimator for CACE (namely, we do not control for the covariates in the nodes). We suggest to use this algorithm whenver we can suppose that the unconfoundedness assumption holds within any sub-populations and it is possible to rule out to control for the confounders in the sub-population.

