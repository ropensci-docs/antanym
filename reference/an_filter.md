# Filter a collection of place names by various criteria

A data frame of place names can be filtered according to name,
geographic location, feature type, or other criteria. All text-related
matches are by default treated as regular expressions and are
case-insensitive: you can change this behaviour via the `ignore_case`
and `as_regex` parameters.

## Usage

``` r
an_filter(
  gaz,
  query,
  feature_ids,
  extent,
  feature_type,
  origin,
  origin_gazetteer,
  ignore_case = TRUE,
  as_regex = TRUE
)
```

## Arguments

- gaz:

  data.frame or SpatialPointsDataFrame: as returned by
  [`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md) or
  [`an_preferred`](https://docs.ropensci.org/antanym/reference/an_preferred.md)

- query:

  character: vector of place name terms to search for. Returned place
  names will be those that match all entries in `query`

- feature_ids:

  numeric: return only place names associated with the features
  identified by these identifiers. Currently these values can only be
  `scar_common_id` values

- extent:

  vector of c(longitude_min, longitude_max, latitude_min, latitude_max):
  if provided, search only for names within this bounding box. `extent`
  can also be passed as a raster Extent object, a Raster object (in
  which case its extent will be used), a Spatial object (in which case
  the bounding box of the object will be used as the extent), or a
  matrix (in which case it will be assumed to be the output of
  [`sp::bbox`](https://edzer.github.io/sp/reference/bbox.html))

- feature_type:

  string: return only place names corresponding to feature types
  matching this pattern. For valid feature type names see
  [`an_feature_types`](https://docs.ropensci.org/antanym/reference/an_feature_types.md)

- origin:

  string: return only place names originating from bodies (countries or
  organisations) matching this pattern. For valid `origin` values see
  `link{an_origins}`

- origin_gazetteer:

  string: return only place names originating from gazetteers matching
  this pattern. For valid gazetteer names see
  [`an_gazetteers`](https://docs.ropensci.org/antanym/reference/an_gazetteers.md)

- ignore_case:

  logical: if `TRUE`, use case-insensitive text matching

- as_regex:

  logical: if `TRUE`, treat `query` and other string input parameters as
  regular expressions. If `FALSE`, they will be treated as fixed strings
  to match against

## Value

data.frame of results

## References

<https://data.aad.gov.au/aadc/gaz/scar/>,
<https://www.scar.org/data-products/place-names/>

## See also

[`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md),
[`an_gazetteers`](https://docs.ropensci.org/antanym/reference/an_gazetteers.md),
[`an_origins`](https://docs.ropensci.org/antanym/reference/an_origins.md)

## Examples

``` r
if (FALSE) { # \dontrun{
 g <- an_read(cache = "session")

 ## simple search for any place name containing the word 'William'
 an_filter(g, query = "William")

 ## which bodies (countries or organisations) provided the names in our data?
 an_origins(g)

 ## find names containing "William" and originating from Australia or the USA
 an_filter(g, query = "William", origin = "Australia|United States of America")

 ## this search will return no matches
 ## because the actual place name is 'William Scoresby Archipelago'
 an_filter(g, query = "William Archipelago")

 ## we can split the search terms so that each is matched separately
 an_filter(g, query = c("William", "Archipelago"))

 ## or use a regular expression
 an_filter(g, query = "William .* Archipelago")

 ## or refine the search using feature type
 an_filter(g, query = "William", feature_type = "Archipelago")

 ## what feature types do we have in our data?
 an_feature_types(g)

 ## for more complex text searching, use regular expressions
 ## e.g. names matching "West" or "East"
 an_filter(g, query = "West|East")

 ## names starting with "West" or "East"
 an_filter(g, query = "^(West|East)")

 ## names with "West" or "East" appearing as complete words in the name
 ## ["\b" matches a word boundary: see help("regex") ]
 an_filter(g, query = "\\b(West|East)\\b")

 ## filtering by spatial extent
 nms <- an_filter(g, extent = c(100, 120, -70, -65), origin = "Australia")
 with(nms, plot(longitude, latitude))
 with(nms, text(longitude, latitude, place_name))

 ## searching within the extent of an sp object
 my_sp <- sp::SpatialPoints(cbind(c(100, 120), c(-70, -65)))
 an_filter(g, extent = my_sp)

 ## or equivalently
 an_filter(g, extent = bbox(my_sp))

 ## or using the sp form of the gazetteer data
 gsp <- an_read(cache = "session", sp = TRUE)
 an_filter(gsp, extent = my_sp)

 ## using the pipe operator
 g %>% an_filter(query = "Ross", feature_type = "Ice shelf|Mountain")

 g %>% an_near(loc = c(100, -66), max_distance = 20) %>%
       an_filter(feature_type = "Island")

 ## find all names for feature 1589 and the naming
 ##  authority for each name
 an_filter(g, feature_ids = 1589)[, c("place_name", "origin")]
} # }
```
