# Extract factor loadings from galamm object

Extract factor loadings from galamm object

## Usage

``` r
# S3 method for class 'galamm'
factor_loadings(object)
```

## Arguments

- object:

  Object of class `galamm` returned from
  [`galamm`](https://docs.ropensci.org/galamm/reference/galamm.md).

## Value

A matrix containing the estimated factor loadings with corresponding
standard deviations.

## Details

This function has been named `factor_loadings` rather than just
`loadings` to avoid conflict with
[`stats::loadings`](https://rdrr.io/r/stats/loadings.html).

## See also

[`fixef.galamm()`](https://docs.ropensci.org/galamm/reference/fixef.md)
for fixed regression coefficients,
[`confint.galamm()`](https://docs.ropensci.org/galamm/reference/confint.galamm.md)
for confidence intervals, and
[`coef.galamm()`](https://docs.ropensci.org/galamm/reference/coef.galamm.md)
for coefficients more generally.

Other details of model fit:
[`VarCorr`](https://docs.ropensci.org/galamm/reference/VarCorr.md),
[`appraise.galamm()`](https://docs.ropensci.org/galamm/reference/appraise.galamm.md),
[`coef.galamm()`](https://docs.ropensci.org/galamm/reference/coef.galamm.md),
[`confint.galamm()`](https://docs.ropensci.org/galamm/reference/confint.galamm.md),
[`derivatives.galamm()`](https://docs.ropensci.org/galamm/reference/derivatives.galamm.md),
[`deviance.galamm()`](https://docs.ropensci.org/galamm/reference/deviance.galamm.md),
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

## Author

The example for this function comes from `PLmixed`, with authors
Nicholas Rockwood and Minjeong Jeon (Rockwood and Jeon 2019) .

## Examples

``` r
# Logistic mixed model with factor loadings, example from PLmixed
data("IRTsim", package = "PLmixed")

# Reduce data size for the example to run faster
IRTsub <- IRTsim[IRTsim$item < 4, ]
IRTsub <- IRTsub[sample(nrow(IRTsub), 300), ]
IRTsub$item <- factor(IRTsub$item)

# Fix loading for first item to 1, and estimate the two others freely
loading_matrix <- matrix(c(1, NA, NA), ncol = 1)

# Estimate model
mod <- galamm(y ~ item + (0 + ability | sid) + (0 + ability | school),
  data = IRTsub, family = binomial, load_var = "item",
  factor = "ability", lambda = loading_matrix
)

# Show estimated factor loadings, with standard errors
factor_loadings(mod)
#>          ability        SE
#> lambda1 1.000000        NA
#> lambda2 1.222182 0.8141238
#> lambda3 1.158764 0.6707796
```
