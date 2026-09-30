# Predictions from a model at new data values

Predictions are given at the population level, i.e., with random effects
set to zero. For fitted models including random effects, see
[`fitted.galamm`](https://docs.ropensci.org/galamm/reference/fitted.galamm.md).
For mixed response models, only predictions on the scale of the linear
predictors is supported.

## Usage

``` r
# S3 method for class 'galamm'
predict(object, newdata = NULL, type = c("link", "response", "lpmatrix"), ...)
```

## Arguments

- object:

  An object of class `galamm` returned from
  [`galamm`](https://docs.ropensci.org/galamm/reference/galamm.md).

- newdata:

  Data from for which to evaluate predictions, in a `data.frame`.
  Defaults to "NULL", which means that the predictions are evaluate at
  the data used to fit the model.

- type:

  Character argument specifying the type of prediction object to be
  returned. Case sensitive.

- ...:

  Optional arguments passed on to other methods. Currently used for
  models with smooth terms, for which these arguments are forwarded to
  [`mgcv::predict.gam`](https://rdrr.io/pkg/mgcv/man/predict.gam.html).

## Value

A numeric vector of predicted values.

## See also

[`fitted.galamm()`](https://docs.ropensci.org/galamm/reference/fitted.galamm.md)
for model fits,
[`residuals.galamm()`](https://docs.ropensci.org/galamm/reference/residuals.galamm.md)
for residuals, and [`predict()`](https://rdrr.io/r/stats/predict.html)
for the generic function.

Other details of model fit:
[`VarCorr`](https://docs.ropensci.org/galamm/reference/VarCorr.md),
[`appraise.galamm()`](https://docs.ropensci.org/galamm/reference/appraise.galamm.md),
[`coef.galamm()`](https://docs.ropensci.org/galamm/reference/coef.galamm.md),
[`confint.galamm()`](https://docs.ropensci.org/galamm/reference/confint.galamm.md),
[`derivatives.galamm()`](https://docs.ropensci.org/galamm/reference/derivatives.galamm.md),
[`deviance.galamm()`](https://docs.ropensci.org/galamm/reference/deviance.galamm.md),
[`factor_loadings.galamm()`](https://docs.ropensci.org/galamm/reference/factor_loadings.galamm.md),
[`family.galamm()`](https://docs.ropensci.org/galamm/reference/family.galamm.md),
[`fitted.galamm()`](https://docs.ropensci.org/galamm/reference/fitted.galamm.md),
[`fixef`](https://docs.ropensci.org/galamm/reference/fixef.md),
[`formula.galamm()`](https://docs.ropensci.org/galamm/reference/formula.galamm.md),
[`llikAIC()`](https://docs.ropensci.org/galamm/reference/llikAIC.md),
[`logLik.galamm()`](https://docs.ropensci.org/galamm/reference/logLik.galamm.md),
[`model.frame.galamm()`](https://docs.ropensci.org/galamm/reference/model.frame.galamm.md),
[`nobs.galamm()`](https://docs.ropensci.org/galamm/reference/nobs.galamm.md),
[`print.VarCorr.galamm()`](https://docs.ropensci.org/galamm/reference/print.VarCorr.galamm.md),
[`ranef.galamm()`](https://docs.ropensci.org/galamm/reference/ranef.galamm.md),
[`residuals.galamm()`](https://docs.ropensci.org/galamm/reference/residuals.galamm.md),
[`response()`](https://docs.ropensci.org/galamm/reference/response.md),
[`sigma.galamm()`](https://docs.ropensci.org/galamm/reference/sigma.galamm.md),
[`vcov.galamm()`](https://docs.ropensci.org/galamm/reference/vcov.galamm.md)

## Examples

``` r
# Poisson GLMM
count_mod <- galamm(
  formula = y ~ lbas * treat + lage + v4 + (1 | subj),
  data = epilep, family = poisson
)

# Plot response versus link:
plot(
  predict(count_mod, type = "link"),
  predict(count_mod, type = "response")
)


# Predict on a new dataset
nd <- data.frame(lbas = c(.3, .2), treat = c(0, 1), lage = 0.2, v4 = -.2)
predict(count_mod, newdata = nd)
#>       [,1]
#> 1 2.188055
#> 2 1.832320
predict(count_mod, newdata = nd, type = "response")
#>       [,1]
#> 1 8.917850
#> 2 6.248365

# Semiparametric model
dat <- subset(cognition, domain == 1 & item == "11")
dat$y <- dat$y[, 1]
mod <- galamm(y ~ s(x) + (1 | id), data = dat)

# Get the linear predictor matrix
Xp <- predict(mod, type = "lpmatrix")
# Compute the estimated smooth function
# See the vignette on posterior sampling for details
betas <- coef(mod$gam)
fit <- Xp %*% betas
plot(dat$x, fit)

```
