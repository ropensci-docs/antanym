# Thin names to give approximately uniform spatial coverage

The provided data.frame of names will be thinned down to a smaller
number of names. The thinning process attempts to select a subset of
names that are uniformly spatially distributed, while simultaneously
choosing the most important names (according to their relative score in
the `score_col` column.

## Usage

``` r
an_thin(gaz, n, score_col = "score", score_weighting = 5, row_limit = 2000)
```

## Arguments

- gaz:

  data.frame or SpatialPointsDataFrame: typically as returned by
  [`an_suggest`](https://docs.ropensci.org/antanym/reference/an_suggest.md)

- n:

  numeric: number of names to return

- score_col:

  string: the name of the column that gives the relative score of each
  name (e.g. as returned by `an_suggest`). Names with higher scores will
  be preferred by the thinning process. If the specified `score_col`
  column is not present in `gaz`, or if all values within that column
  are equal, then the thinning will be based entirely on the spatial
  distribution of the features

- score_weighting:

  numeric: weighting of scores relative to spatial distribution. A lower
  `score_weighting` value will tend to choose lower-scored names in
  order to achieve better spatial uniformity. A higher `score_weighting`
  value will trade spatial uniformity in favour of selecting
  higher-scored names

- row_limit:

  integer: the maximum number of rows allowed in `gaz`; see Details.
  Data frames larger than this will not be processed (with an error).

## Value

data.frame

## Details

Note that the algorithm calculates all pairwise distances between the
rows of `gaz`. This is memory-intensive, and so if `gaz` has many rows
the algorithm will fail or on some platforms might crash. Input `gaz`
data.frames with more than `row_limit` rows will not be processed for
this reason. You can try increasing `row_limit` from its default value
if necessary.

## See also

[`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md),
[`an_suggest`](https://docs.ropensci.org/antanym/reference/an_suggest.md)

## Examples

``` r
if (FALSE) { # \dontrun{
 g <- an_read(cache = "session")

 ## get a single name per feature, preferring the
 ##  Japanese name where there is one
 g <- an_preferred(g, origin = "Japan")

 ## suggested names for a 100x100 mm map covering 60-90E, 70-60S
 ##  (this is about a 1:12M scale map)
 suggested <- an_suggest(g, map_extent = c(60, 90, -70, -60), map_dimensions = c(100, 100))

 ## find the top 20 names by score
 head(suggested, 20)

 ## find the top 20 names chosen for spatial coverage and score
 an_thin(suggested, 20)
} # }
```
