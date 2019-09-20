Dependent assignment
================

### R example

[Tidyverse](https://www.tidyverse.org/) allows us to use newly
created/modified variables within a single `mutate` assignment. Note for
the example below, `area` is dependent on the new `length` and `width`
variables.

``` r
# measure in mm instead of cm and compute area
df %>% 
  mutate(
    length = length * 10,
    width = width * 10,
    area = length * width) %>% 
  head(5)
```

    ##   length width area
    ## 1     51    35 1785
    ## 2     49    30 1470
    ## 3     47    32 1504
    ## 4     46    31 1426
    ## 5     50    36 1800

### Python example

Dependent assignment in pandas (as of 0.25.x) requires a workaround
using [anonymous
functions](https://github.com/pandas-dev/pandas/issues/14207).

``` python
(df
  .assign(
    length = df["length"] * 10,
    width = df["width"] * 10,
  # area = df["length"] * df["width"] this will throw an error 
    area = lambda df: df["length"] * df["width"])
  .head(5))
```

    ##    length  width    area
    ## 0    51.0   35.0  1785.0
    ## 1    49.0   30.0  1470.0
    ## 2    47.0   32.0  1504.0
    ## 3    46.0   31.0  1426.0
    ## 4    50.0   36.0  1800.0
