# Calculate approximate map scale

Calculate approximate map scale

## Usage

``` r
an_mapscale(map_dimensions, map_extent)
```

## Arguments

- map_dimensions:

  numeric: 2-element numeric giving width and height of the map, in mm

- map_extent:

  vector of c(longitude_min, longitude_max, latitude_min, latitude_max):
  the geographic extent of the map. `map_extent` can also be passed as a
  raster Extent object, a Raster object (in which case its extent will
  be used), a Spatial object (in which case the bounding box of the
  object will be used as the extent), or a matrix (in which case it will
  be assumed to be the output of
  [`sp::bbox`](https://edzer.github.io/sp/reference/bbox.html))

## Value

numeric

## Examples

``` r
## an A3-sized map of the Southern Ocean (1:20M)
an_mapscale(map_dimensions = c(400, 570), map_extent = c(-180, 180, -90, -40))
#> [1] 19967274
```
