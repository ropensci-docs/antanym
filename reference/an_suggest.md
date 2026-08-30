# Suggest names for a map (experimental)

Features are given a suitability score based on maps prepared by expert
cartographers. Data were tabulated from a collection of such maps,
indicating for each feature whether it was named on a given map, along
with details (such as scale) of the map. These data are used as the
basis of a recommendation algorithm, which suggests the best features to
name on a map given its properties (extent and scale). This is an
experimental function and currently only implemented for `map_scale`
values of 10 million or larger.

## Usage

``` r
an_suggest(gaz, map_scale, map_extent, map_dimensions)
```

## Arguments

- gaz:

  data.frame or SpatialPointsDataFrame: as returned by
  [`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md),
  [`an_preferred`](https://docs.ropensci.org/antanym/reference/an_preferred.md),
  or
  [`an_filter`](https://docs.ropensci.org/antanym/reference/an_filter.md)

- map_scale:

  numeric: the scale of the map (e.g. 20e6 for a 1:20M map). If
  `map_scale` is not provided, it will be estimated from `map_extent`
  and `map_dimensions`

- map_extent:

  vector of c(longitude_min, longitude_max, latitude_min, latitude_max):
  the extent of the area for which name suggestions are sought. This is
  required if `map_scale` is not provided, and optional if `map_scale`
  is provided (if `map_extent` is provided in this situation then the
  `gaz` data frame will be filtered to this extent before the suggestion
  algorithm is applied; otherwise all names in `gaz` will be
  considered). `map_extent` can also be passed as a raster Extent
  object, a Raster object (in which case its extent will be used), a
  Spatial object (in which case the bounding box of the object will be
  used as the extent), or a matrix (in which case it will be assumed to
  be the output of
  [`sp::bbox`](https://edzer.github.io/sp/reference/bbox.html))

- map_dimensions:

  numeric: 2-element numeric giving width and height of the map, in mm.
  Not required if `map_scale` is provided

## Value

data.frame of names with a "score" column added. Score values range from
0 to 1. The data frame will be sorted in descending score order. Names
with higher scores are those that are suggested as the most suitable for
display.

## See also

[`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md)
[`an_thin`](https://docs.ropensci.org/antanym/reference/an_thin.md)

## Examples

``` r
if (FALSE) { # \dontrun{
 g <- an_read(cache = "session")

 ## get a single name per feature, preferring the
 ##  Australian name where there is one
 g <- an_preferred(g, origin = "Australia")

 ## suggested names for a 100x100 mm map covering 60-90E, 70-60S
 ##  (this is about a 1:12M scale map)
 suggested <- an_suggest(g, map_extent = c(60, 90, -70, -60), map_dimensions = c(100, 100))
 head(suggested, 20) ## top 20 names

 ## an equivalent result can be achieved by supplying map scale and extent
 suggested <- an_suggest(g, map_scale = 12e6, map_extent = c(60, 90, -70, -60))
} # }
```
