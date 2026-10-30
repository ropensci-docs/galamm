# Print method for variance-covariance objects

Print method for variance-covariance objects

## Usage

``` r
# S3 method for class 'VarCorr.galamm'
print(
  x,
  digits = max(3, getOption("digits") - 2),
  comp = c("Std.Dev.", "Variance"),
  corr = any(comp == "Std.Dev."),
  ...
)
```

## Arguments

- x:

  An object of class `c("VarCorr.galamm", "VarCorr.merMod")`, returned
  from
  [`VarCorr.galamm`](https://docs.ropensci.org/galamm/reference/VarCorr.md).

- digits:

  Optional arguments specifying number of digits to use when printing.

- comp:

  Character vector of length 1 or 2 specifying which variance components
  to print. Case sensitive. Can take one of the values "Std.Dev." and
  "Variance".

- corr:

  Logical value indicating whether covariances or correlations should be
  printed.

- ...:

  Optional arguments passed on to other methods. Currently not used.

## Value

The variance-covariance information is printed to the console and the
argument `x` is silently returned.

## References

Bates DM, Mächler M, Bolker B, Walker S (2015). “Fitting Linear
Mixed-Effects Models Using Lme4.” *Journal of Statistical Software*,
**67**(1), 1–48. ISSN 1548-7660.
[doi:10.18637/jss.v067.i01](https://doi.org/10.18637/jss.v067.i01) .

## See also

[`VarCorr.galamm()`](https://docs.ropensci.org/galamm/reference/VarCorr.md)
for the function creating the variance-covariance objects.

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
[`ranef.galamm()`](https://docs.ropensci.org/galamm/reference/ranef.galamm.md),
[`residuals.galamm()`](https://docs.ropensci.org/galamm/reference/residuals.galamm.md),
[`response()`](https://docs.ropensci.org/galamm/reference/response.md),
[`sigma.galamm()`](https://docs.ropensci.org/galamm/reference/sigma.galamm.md),
[`vcov.galamm()`](https://docs.ropensci.org/galamm/reference/vcov.galamm.md)

## Author

This function is derived from `lme4:::print.VarCorr.merMod` written by
Douglas M. Bates, Martin Maechler, Ben Bolker, and Steve Walker.

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
```
