# Introduction

``` r

library(galamm)
```

This vignette is aimed to give you a high-level overview of the types of
models supported by the galamm package, and to point you to relevant
vignettes where you can find more information.

### Generalized Additive Latent and Mixed Models

Generalized additive latent and mixed models (GALAMMs) ([Sørensen et al.
2023](#ref-sorensenLongitudinalModelingAgeDependent2023)) is an
extension of generalized linear latent and mixed models (GLLAMMs)
([Rabe-Hesketh et al.
2004](#ref-rabe-heskethGeneralizedMultilevelStructural2004); [Skrondal
and Rabe-Hesketh 2004](#ref-skrondalGeneralizedLatentVariable2004))
which allows both observed responses and latent variables to depend
smoothly on observed variables. *Smoothly* here means that the
relationship is not assumed to follow a particular parametric form,
e.g., as specified by a linear model. Instead, an *a priori* assumption
is made that the relationship is smooth, and the model then attempts to
learn the relationship from the data. GALAMM uses smoothing splines to
obtain this, identically to how generalized additive models (GAMs)
([Wood 2017](#ref-woodGeneralizedAdditiveModels2017)) are estimated.

The GLLAMM framework contains many elements which are currently not
implemented in the galamm package. This includes both nonparametric
random effects and a large number of model families, e.g., for censored
responses. If you need any of this, but not semiparametric estimation,
the Stata based [GLLAMM package](http://www.gllamm.org/) is likely the
place you should go. Conversely, galamm incorporates crossed random
effects easily and efficiently, while these are hard to specify using
GLLAMM.

#### Response Model

GALAMMs are specified using three building blocks. First, \\n\\
responses \\y\_{1}, \dots, y\_{n}\\ are assumed independently
distributed according to an exponential family with density

\\ f\left(y \| \theta, \phi\right) = \exp \left( \frac{y\theta(\mu) -
b\left(\theta(\mu)\right)}{\phi} + c\left(y, \phi\right) \right) \\

here \\\mu = g^{-1}(\nu)\\ is the mean, \\g^{-1}(\cdot)\\ is the inverse
of link function \\g(\cdot)\\, \\\nu\\ is a “nonlinear predictor”,
\\\phi\\ is a dispersion parameter, and \\b(\cdot)\\ and \\c(\cdot)\\
are known functions. In contrast to what is assumed, e.g., by
[lme4](https://cran.r-project.org/package=lme4) ([Bates et al.
2015](#ref-batesFittingLinearMixedEffects2015)), the functions
\\b(\cdot)\\, \\c(\cdot)\\, and \\g(\cdot)\\ are allowed to vary between
observations. That is, the observations can come from different members
of the exponential family. The vignette on [models with mixed response
types](https://docs.ropensci.org/galamm/articles/mixed_response.html)
describes this in detail.

Using canonical link functions, the response model simplifies to

\\ f\left(y \| \nu, \phi\right) = \exp \left( \frac{y\nu -
b\left(\nu\right)}{\phi} + c\left(y, \phi\right) \right) \\

#### Nonlinear Predictor

Next, the nonlinear predictor, which corresponds to the measurement
model in a classical structural equation model, is defined by

\\ \nu = \sum\_{s=1}^{S} f\_{s}\left(\mathbf{x}\right) +
\sum\_{l=2}^{L}\sum\_{m=1}^{M\_{l}} \eta\_{m}^{(l)}
\mathbf{z}^{(l)}\_{m}{}^{'}\pmb{\lambda}\_{m}^{(l)}, \\

where \\\mathbf{x}\\ are explanatory variables, \\f\_{s}(\mathbf{x})\\,
\\s=1,\dots,S\\ are smooth functions, \\\eta\_{m}^{(l)}\\ are latent
variables varying at level \\l\\, and \\\pmb{\lambda}\_{m}^{(l)}{}^{T}
\mathbf{z}\_{m}^{(l)}\\ is the weighted sum of a vector of explanatory
variables \\\mathbf{z}\_{m}^{(l)}\\ varying at level \\l\\ and
parameters \\\pmb{\lambda}\_{m}^{(l)}\\. Let

\\\pmb{\eta}^{(l)} = \[\eta\_{1}^{(l)}, \dots,
\eta\_{M\_{l}}^{(l)}\]^{T} \in \mathbb{R}^{M\_{l}}\\

be the vector of all latent variables at level \\l\\, and

\\\pmb{\eta} = \[\pmb{\eta}^{(2)}, \dots, \pmb{\eta}^{(L)}\]^{T} \in
\mathbb{R}^{M}\\

the vector of all latent variables belonging to a given level-2 unit,
where \\M = \sum\_{l=2}^{L} M\_{l}\\. The word “level” is here used to
denote a grouping level; they are not necessarily hierarchical.

### Structural Model

The structural model specifies how the latent variables are related to
each other and to observed variables, and is given by

\\ \pmb{\eta} = \mathbf{B}\pmb{\eta} +
\mathbf{h}\left(\mathbf{w}\right) + \pmb{\zeta} \\

where \\\mathbf{B}\\ is an \\M \times M\\ matrix of regression
coefficients for regression among latent variables and \\\mathbf{w} \in
\mathbb{R}^{Q}\\ is a vector of \\Q\\ predictors for the latent
variables. \\\mathbf{h}(\mathbf{w}) = \[\mathbf{h}\_{2}(\mathbf{w}),
\dots, \mathbf{h}\_{L}(\mathbf{w})\] \in \mathbb{R}^{M}\\ is a vector of
smooth functions whose components \\\mathbf{h}\_{l}(\mathbf{w}) \in
\mathbb{R}^{M\_{l}}\\ are vectors of functions predicting the latent
variables varying at level \\l\\, and depending on a subset of the
elements \\\mathbf{w}\\. \\\pmb{\zeta}\\ is a vector of normally
distributed random effects, \\\pmb{\zeta}^{(l)} \sim N(\mathbf{0},
\pmb{\Psi}^{(l)})\\ for \\l=2,\dots,L\\, where \\\pmb{\Psi}^{(l)} \in
\mathbb{R}^{M\_{l} \times M\_{l}}\\ is the covariance matrix of random
effects at level \\l\\. Defining the \\M \times M\\ covariance matrix
\\\pmb{\Psi} = \text{diag}(\pmb{\Psi}^{(2)}, \dots, \pmb{\Psi}^{(L)})\\,
we also have \\\pmb{\zeta} \sim N(\mathbf{0}, \pmb{\Psi})\\.

### Mixed Model Representation

In Sørensen et al.
([2023](#ref-sorensenLongitudinalModelingAgeDependent2023)) we show that
any model specified as above can be transformed to a GLLAMM, which is
essentially a generalized nonlinear mixed model. This transformation is
rather complex, so we won’t spell it out here, but the key steps are:

1.  Converting smooth terms to their mixed model form.
2.  Estimate the resulting GLLAMM.
3.  Convert back to the original parametrization.

In galamm we use the same transformations as the
[gamm4](https://CRAN.R-project.org/package=gamm4) package does.

### Maximum Marginal Likelihood Estimation

In mixed model representation, the nonlinear predictor can be written on
the form

\\ \pmb{\nu} = \mathbf{X}(\pmb{\lambda}, \mathbf{B}) \pmb{\beta} +
\mathbf{Z}(\pmb{\lambda}, \mathbf{B}) \pmb{\zeta} \\

where \\\mathbf{X}(\pmb{\lambda}, \mathbf{B})\\ is the regression matrix
for fixed effects \\\pmb{\beta}\\ and \\\mathbf{Z}(\pmb{\lambda},
\mathbf{B})\\ is the regression matrix for random effects
\\\pmb{\zeta}\\. In contrast to with generalized linear mixed models,
however, both matrices will in general depend on factor loadings
\\\pmb{\lambda}\\ and regression coefficients between latent variables
\\\mathbf{B}\\. Both of these are parameters that need to be estimated,
and hence \\\mathbf{X}(\pmb{\lambda}, \mathbf{B})\\ and \\\pmb{\beta}\\
and \\\mathbf{Z}(\pmb{\lambda}, \mathbf{B})\\ need to be updated
throughout the estimation process.

#### Evaluating the Marginal Likelihood

Plugging the nonlinear predictor into the structural model, we obtain
the joint likelihood for the model. We then obtain the marginal
likelihood by integrating over the random effects, yielding a marginal
likelihood function of the form

\\ L\left(\pmb{\beta}, \pmb{\Lambda}, \pmb{\Gamma}, \pmb{\lambda},
\mathbf{B}, \pmb{\phi}\right) = \left(2 \pi \phi\_{1}\right)^{-r/2}
\int\_{\mathbb{R}^{r}} \exp\left( g\left(\pmb{\beta}, \pmb{\Lambda},
\pmb{\Gamma}, \pmb{\lambda}, \mathbf{B}, \pmb{\phi}, \mathbf{u}\right)
\right) \text{d} \mathbf{u} \\

where \\\mathbf{u}\\ is a standardized version of \\\pmb{\zeta}\\. In
order to evaluate the marginal likelihood at a given set of parameter
values, we use the Laplace approximation combined with sparse matrix
operations, extending Bates et al.
([2015](#ref-batesFittingLinearMixedEffects2015))’s algorithm for linear
mixed models.

#### Maximizing the Marginal Likelihood

We obtain maximum marginal likelihood estimates by maximizing
\\L\left(\pmb{\beta}, \pmb{\Lambda}, \pmb{\Gamma}, \pmb{\lambda},
\mathbf{B}, \pmb{\phi}\right)\\, subject to possible constraints, e.g.,
that variances are non-negative. For this, we use the L-BFGS-B algorithm
implement in [`stats::optim`](https://rdrr.io/r/stats/optim.html). The
predicted values of random effects, \\\widehat{\mathbf{u}}\\ are
obtained as posterior modes at the final estimates.

### Example Models

To see how galamm is used in practice, take a look at the vignettes
describing models with different components.

- [Linear mixed models with factor
  structures](https://docs.ropensci.org/galamm/articles/lmm_factor.html).
- [Generalized linear mixed models with factor
  structures](https://docs.ropensci.org/galamm/articles/glmm_factor.html).
- [Linear mixed models with heteroscedastic
  residuals](https://docs.ropensci.org/galamm/articles/lmm_heteroscedastic.html).
- [Models with interactions between latent and observed
  covariates](https://docs.ropensci.org/galamm/articles/latent_observed_interaction.html).
- [Mixed models with mixed response
  types](https://docs.ropensci.org/galamm/articles/mixed_response.html).
- [Generalized additive mixed models with factor
  structures](https://docs.ropensci.org/galamm/articles/semiparametric.html).

## References

Bates, Douglas M, Martin Mächler, Ben Bolker, and Steve Walker. 2015.
“Fitting Linear Mixed-Effects Models Using Lme4.” *Journal of
Statistical Software* 67 (1): 1–48.
<https://doi.org/10.18637/jss.v067.i01>.

Rabe-Hesketh, Sophia, Anders Skrondal, and Andrew Pickles. 2004.
“Generalized Multilevel Structural Equation Modeling.” *Psychometrika*
69 (2): 167–90. <https://doi.org/10.1007/BF02295939>.

Skrondal, Anders, and Sophia Rabe-Hesketh. 2004. *Generalized Latent
Variable Modeling*. Interdisciplinary Statistics Series. Chapman and
Hall/CRC.

Sørensen, Øystein, Anders M. Fjell, and Kristine B. Walhovd. 2023.
“Longitudinal Modeling of Age-Dependent Latent Traits with Generalized
Additive Latent and Mixed Models.” *Psychometrika* 88 (2): 456–86.
<https://doi.org/10.1007/s11336-023-09910-z>.

Wood, Simon N. 2017. *Generalized Additive Models: An Introduction with
R*. 2nd ed. Chapman and Hall/CRC.
