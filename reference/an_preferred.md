# Find one name per feature in the Composite Gazetteer

The Composite Gazetteer of Antarctica is a compilation of place names
provided by different countries and organisations. The composite nature
of the CGA means that there may be multiple names associated with a
single feature. The `an_preferred` function can be used to resolve a
single name per feature. Provide one or more `origin` entries and the
input `gaz` will be filtered to a single name per feature. For features
that have multiple names (e.g. have been named by multiple countries) a
single name will be chosen, preferring names from the specified `origin`
bodies where possible.

## Usage

``` r
an_preferred(gaz, origin, unmatched = "random")
```

## Arguments

- gaz:

  data.frame or SpatialPointsDataFrame: as returned by
  [`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md) or
  [`an_filter`](https://docs.ropensci.org/antanym/reference/an_filter.md)

- origin:

  character: vector of preferred name origins (countries or
  organisations), in order of preference. If a given feature has been
  named by one of these bodies, this place name will be chosen. If the
  feature in question has not been given a name by any of these bodies,
  a place name given by another body will be chosen, with preference
  according to the `unmatched` parameter. For valid `origin` values, see
  [`an_origins`](https://docs.ropensci.org/antanym/reference/an_origins.md)

- unmatched:

  string: how should names be chosen for features that have not been
  been named by one of the preferred `origin` bodies? Valid values are
  "random" (the non-preferred originating bodies will be randomly
  ordered) or "count" (the non-preferred originating bodies will be
  ordered by their number of entries, with the largest first)

## Value

data.frame of results

## References

<https://data.aad.gov.au/aadc/gaz/scar/>,
<https://www.scar.org/data-products/place-names/>

## See also

[`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md),
[`an_origins`](https://docs.ropensci.org/antanym/reference/an_origins.md)

## Examples

``` r
if (FALSE) { # \dontrun{
 g <- an_read(cache = "session")

 ## get a single name per feature, preferring the
 ##  Polish name where there is one
 pnames <- an_preferred(g, origin = "Poland")

 ## names starting with "Sm", preferring US names then
 ##  Australian ones if available
 g %>% an_filter("^Sm") %>%
       an_preferred(origin = c("United States of America", "Australia"))
} # }
```
