# Get links to gazetteer entries

Each entry in the Composite Gazetteer of Antarctica has its own web
page. The `an_url` function will return the URL of the page associated
with a given gazetteer entry.

## Usage

``` r
an_get_url(gaz)
```

## Arguments

- gaz:

  data.frame or SpatialPointsDataFrame: as returned by
  [`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md),
  [`an_preferred`](https://docs.ropensci.org/antanym/reference/an_preferred.md),
  or
  [`an_filter`](https://docs.ropensci.org/antanym/reference/an_filter.md)

## Value

character vector, where each component is a URL to a web page giving
more information about the associated gazetteer entry

## References

<https://data.aad.gov.au/aadc/gaz/scar/>,
<https://www.scar.org/data-products/place-names/>

## Examples

``` r
if (FALSE) { # \dontrun{
 g <- an_read(cache = "session")
 my_url <- an_get_url(an_filter(g, query = "Ufs Island")[1, ])
 browseURL(my_url)
} # }
```
