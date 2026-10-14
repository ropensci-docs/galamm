# Extract deviance of galamm object

Extract deviance of galamm object

## Usage

``` r
# S3 method for class 'galamm'
deviance(object, ...)
```

## Arguments

- object:

  Object of class `galamm`, returned from
  [`galamm`](https://docs.ropensci.org/galamm/reference/galamm.md).

- ...:

  Other arguments passed on to other methods. Currently not used.

## Value

A numeric value giving the deviance of the model fit.

## See also

[`logLik.galamm()`](https://docs.ropensci.org/galamm/reference/logLik.galamm.md)
for a function returning the log likelihood and
[`deviance()`](https://rdrr.io/r/stats/deviance.html) for the generic
function.

Other details of model fit:
[`VarCorr`](https://docs.ropensci.org/galamm/reference/VarCorr.md),
[`appraise.galamm()`](https://docs.ropensci.org/galamm/reference/appraise.galamm.md),
[`coef.galamm()`](https://docs.ropensci.org/galamm/reference/coef.galamm.md),
[`confint.galamm()`](https://docs.ropensci.org/galamm/reference/confint.galamm.md),
[`derivatives.galamm()`](https://docs.ropensci.org/galamm/reference/derivatives.galamm.md),
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
[`sigma.galamm()`](https://docs.ropensci.org/galamm/reference/sigma.galamm.md),
[`vcov.galamm()`](https://docs.ropensci.org/galamm/reference/vcov.galamm.md)

## Examples

``` r
# Linear mixed model with heteroscedastic residuals
mod <- galamm(
  formula = y ~ x + (1 | id),
  dispformula = ~ (1 | item),
  data = hsced
)

# Extract deviance
deviance(mod)
#> [1] 4116.28
```
