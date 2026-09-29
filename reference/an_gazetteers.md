# The place name gazetteers available

Return a character vector that lists all of the gazetteers present in
the `gaz` data, or (if `gaz` was not provided) all of the gazetteers
available through the antanym package. Currently only one gazetteer is
available: the Composite Gazetteer of Antarctica.

## Usage

``` r
an_gazetteers(gaz)
```

## Arguments

- gaz:

  data.frame or SpatialPointsDataFrame: (optional) as returned by
  [`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md),
  [`an_preferred`](https://docs.ropensci.org/antanym/reference/an_preferred.md),
  or
  [`an_filter`](https://docs.ropensci.org/antanym/reference/an_filter.md)

## Value

character vector. If `gaz` was provided, this will be a list of all
gazetteers present in `gaz`. Otherwise, it will be a list of all
gazetteers available through the antanym package

## See also

[`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md),
[`an_filter`](https://docs.ropensci.org/antanym/reference/an_filter.md)

## Examples

``` r

an_gazetteers()
#> [1] "CGA"

if (FALSE) { # \dontrun{
 g <- an_read(cache = "session")
 an_gazetteers(g)
} # }
```
