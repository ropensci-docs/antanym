# List the origins of place names present in gazetteer data

The Composite Gazetteer of Antarctica is a compilation of place names
provided by different countries and organisations. This function lists
the originating bodies that provided the names in a given data frame.

## Usage

``` r
an_origins(gaz)
```

## Arguments

- gaz:

  data.frame or SpatialPointsDataFrame: as returned by
  [`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md),
  [`an_preferred`](https://docs.ropensci.org/antanym/reference/an_preferred.md),
  or
  [`an_filter`](https://docs.ropensci.org/antanym/reference/an_filter.md)

## Value

character vector of origin names (countries or organisations)

## See also

[`an_filter`](https://docs.ropensci.org/antanym/reference/an_filter.md)
for filtering data according to origin

## Examples

``` r
if (FALSE) { # \dontrun{
 g <- an_read(cache = "session")

 ## which bodies (countries or organisations) provided the names in our data?
 an_origins(g)
} # }
```
