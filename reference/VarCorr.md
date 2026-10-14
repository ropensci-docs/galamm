# Extract variance and correlation components from model

Extract variance and correlation components from model

## Usage

``` r
# S3 method for class 'galamm'
VarCorr(x, sigma = 1, ...)
```

## Arguments

- x:

  An object of class `galamm` returned from
  [`galamm`](https://docs.ropensci.org/galamm/reference/galamm.md).

- sigma:

  Numeric value used to multiply the standard deviations. Defaults to 1.

- ...:

  Other arguments passed onto other methods. Currently not used.

## Value

An object of class `c("VarCorr.galamm", "VarCorr.merMod")`.

## See also

[`print.VarCorr.galamm()`](https://docs.ropensci.org/galamm/reference/print.VarCorr.galamm.md)
for the print function.

Other details of model fit:
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

# Extract information on variance and covariance
VarCorr(mod)
#>  Groups   Name        Variance Std.Dev.
#>  id       (Intercept) 0.98804  0.99400 
#>  Residual             0.95970  0.97964 

# Convert to data frame
# (this invokes lme4's function as.data.frame.VarCorr.merMod)
as.data.frame(VarCorr(mod))
#>        grp        var1 var2      vcov     sdcor
#> 1       id (Intercept) <NA> 0.9880425 0.9940033
#> 2 Residual        <NA> <NA> 0.9596999 0.9796427
```
