
# tidypredict <img src="man/figures/logo.png" align="right" width = "120px"/>

[![Build
Status](https://travis-ci.org/tidymodels/tidypredict.svg?branch=master)](https://travis-ci.org/tidymodels/tidypredict)
[![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/tidypredict)](https://cran.r-project.org/package=tidypredict)
[![Coverage
Status](https://img.shields.io/codecov/c/github/tidymodels/tidypredict/master.svg)](https://codecov.io/github/tidymodels/tidypredict?branch=master)

Run predictions inside the database. `tidypredict` parses a fitted R
model object, and returns a formula in ‘Tidy Eval’ code that calculates
the predictions.

**It works with several databases back-ends** because it uses `dplyr`
and `dbplyr` for the final SQL translation of the algorithm.

## Supported models

The following models are supported by `tidypredict`:

  - Linear Regression - `lm()`
  - Generalized Linear model - `glm()`
  - Random Forest models - `randomForest::randomForest()`
  - Random Forest models, via `ranger` - `ranger::ranger()`
  - MARS models - `earth::earth()`
  - XGBoost models - `xgboost::xgb.Booster.complete()`
  - Cubist models - `Cubist::cubist()`

## Installation

Install `tidypredict` from CRAN using:

``` r
install.packages("tidypredict")
```

Or install the development version using `devtools` as follows:

``` r
devtools::install_github("tidymodels/tidypredict")
```

## Intro

`tidypredict` is able to parse an R model object, such as:

``` r
model <- lm(mpg ~ wt + cyl, data = mtcars)
```

And then creates the SQL statement needed to calculate the fitted
prediction:

``` r
tidypredict_sql(model, dbplyr::simulate_mssql())
```

    ## <SQL> 39.6862614802529 + (`wt` * -3.19097213898374) + (`cyl` * -1.5077949682598)
