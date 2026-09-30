# Calculate variance-covariance matrix for GALAMM fit

Calculate variance-covariance matrix for GALAMM fit

## Usage

``` r
# S3 method for class 'galamm'
vcov(object, parm = "beta", ...)
```

## Arguments

- object:

  Object of class `galamm` returned from
  [`galamm`](https://docs.ropensci.org/galamm/reference/galamm.md).

- parm:

  The parameters for which the variance-covariance matrix should be
  calculated. Character vector with one or more of the elements "theta",
  "beta", "lambda", and "weights". Can also be an integer vector. When
  given as a character, it must be in only lowercase letters.

- ...:

  Further arguments passed on to other methods. Currently not used.

## Value

A variance-covariance matrix.

## See also

[`confint.galamm()`](https://docs.ropensci.org/galamm/reference/confint.galamm.md)
for the method computing confidence intervals. See
[`vcov()`](https://rdrr.io/r/stats/vcov.html) for the generic function.

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
[`predict.galamm()`](https://docs.ropensci.org/galamm/reference/predict.galamm.md),
[`print.VarCorr.galamm()`](https://docs.ropensci.org/galamm/reference/print.VarCorr.galamm.md),
[`ranef.galamm()`](https://docs.ropensci.org/galamm/reference/ranef.galamm.md),
[`residuals.galamm()`](https://docs.ropensci.org/galamm/reference/residuals.galamm.md),
[`response()`](https://docs.ropensci.org/galamm/reference/response.md),
[`sigma.galamm()`](https://docs.ropensci.org/galamm/reference/sigma.galamm.md)

## Examples

``` r
# Linear mixed model with heteroscedastic residuals
mod <- galamm(
  formula = y ~ x + (1 | id),
  dispformula = ~ (1 | item),
  data = hsced
)

# Extract covariance matrix for fixed regression coefficients
vcov(mod, parm = "beta")
#>              [,1]         [,2]
#> [1,]  0.009841573 -0.007511908
#> [2,] -0.007511908  0.014715234

# and then for weights, which gives us the variance.
vcov(mod, parm = "weights")
#>             [,1]
#> [1,] 0.002459613
```
