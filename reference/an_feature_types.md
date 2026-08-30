# List feature types present in gazetteer data

The gazetteer place names are associated with different feature types
(e.g. "Hill", "Mountain", "Water body"). This function lists the feature
types that are present in a given data frame.

## Usage

``` r
an_feature_types(gaz)
```

## Arguments

- gaz:

  data.frame or SpatialPointsDataFrame: as returned by
  [`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md),
  [`an_preferred`](https://docs.ropensci.org/antanym/reference/an_preferred.md),
  or
  [`an_filter`](https://docs.ropensci.org/antanym/reference/an_filter.md)

## Value

character vector of country names

## See also

[`an_filter`](https://docs.ropensci.org/antanym/reference/an_filter.md)
for filtering data according to feature type

## Examples

``` r
if (FALSE) { # \dontrun{
 g <- an_read(cache = "session")

 ## what feature types do we have in our data?
 an_feature_types(g)
} # }
```
