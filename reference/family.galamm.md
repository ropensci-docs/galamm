# Extract family or families from fitted galamm

This function returns a list of families for an object of class
`galamm`, returned from
[`galamm`](https://docs.ropensci.org/galamm/reference/galamm.md).

## Usage

``` r
# S3 method for class 'galamm'
family(object, ...)
```

## Arguments

- object:

  An object of class `galamm` returned from
  [`galamm`](https://docs.ropensci.org/galamm/reference/galamm.md).

- ...:

  Optional arguments passed on to other methods. Currently not used.

## Value

A list of family objects.

## See also

[`galamm()`](https://docs.ropensci.org/galamm/reference/galamm.md)

Other details of model fit:
[`VarCorr`](https://docs.ropensci.org/galamm/reference/VarCorr.md),
[`appraise.galamm()`](https://docs.ropensci.org/galamm/reference/appraise.galamm.md),
[`coef.galamm()`](https://docs.ropensci.org/galamm/reference/coef.galamm.md),
[`confint.galamm()`](https://docs.ropensci.org/galamm/reference/confint.galamm.md),
[`derivatives.galamm()`](https://docs.ropensci.org/galamm/reference/derivatives.galamm.md),
[`deviance.galamm()`](https://docs.ropensci.org/galamm/reference/deviance.galamm.md),
[`factor_loadings.galamm()`](https://docs.ropensci.org/galamm/reference/factor_loadings.galamm.md),
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
# Mixed response model
loading_matrix <- matrix(c(1, NA), ncol = 1)
families <- gfam(list(gaussian, binomial))

mixed_resp <- galamm(
  formula = y ~ x + (0 + level | id),
  data = mresp,
  family = families,
  load_var = "itemgroup",
  lambda = loading_matrix,
  factor = "level"
)

# This model has two family objects
family(mixed_resp)
#> [[1]]
#> 
#> Family: gaussian 
#> Link function: identity 
#> 
#> 
#> [[2]]
#> 
#> Family: binomial 
#> Link function: logit 
#> 
#> 
#> attr(,"class")
#> [1] "galamm_extended_family"
```
