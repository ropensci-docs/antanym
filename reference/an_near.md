# Find placenames near a given location

Find placenames near a given location

## Usage

``` r
an_near(gaz, loc, max_distance)
```

## Arguments

- gaz:

  data.frame or SpatialPointsDataFrame: as returned by
  [`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md),
  [`an_preferred`](https://docs.ropensci.org/antanym/reference/an_preferred.md),
  or
  [`an_filter`](https://docs.ropensci.org/antanym/reference/an_filter.md)

- loc:

  numeric: target location (a two-element numeric vector giving
  longitude and latitude, or a SpatialPoints object)

- max_distance:

  numeric: maximum search distance in kilometres

## Value

data.frame of results

## References

<https://data.aad.gov.au/aadc/gaz/scar/>,
<https://www.scar.org/data-products/place-names/>

## See also

[`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md)

## Examples

``` r
if (FALSE) { # \dontrun{
 g <- an_read(cache = "session")

 ## named features within 10km of 110E, 66S
 an_near(g, loc = c(110, -66), max_distance = 10)

 ## using pipe operator
 g %>% an_near(loc = c(100, -66), max_distance = 10)

 ## with sp objects
 gsp <- an_read(cache = "session", sp = TRUE)
 loc <- sp::SpatialPoints(matrix(c(110, -66), nrow = 1),
   proj4string = CRS("+proj=longlat +datum=WGS84 +ellps=WGS84"))
 an_near(gsp, loc = loc, max_distance = 10)
} # }
```
