# Load Antarctic place name data

Place name data will be downloaded and optionally cached locally. If you
wish to be able to use `antanym` offline, consider using
`cache = "persistent"` so that the cached data will persist from one R
session to the next. See
[`an_cache_directory`](https://docs.ropensci.org/antanym/reference/an_cache_directory.md)
to get the path to the cache directory.

## Usage

``` r
an_read(
  gazetteers = "all",
  sp = FALSE,
  cache,
  refresh_cache = FALSE,
  simplified = TRUE,
  verbose = FALSE
)
```

## Arguments

- gazetteers:

  character: vector of gazetteers to load. For the list of available
  gazetteers, see
  [`an_gazetteers`](https://docs.ropensci.org/antanym/reference/an_gazetteers.md).
  Use `gazetteers = "all"` to load all available gazetteers. Currently
  only one gazetteer is available: the Composite Gazetteer of Antarctica

- sp:

  logical: if FALSE return a data.frame; if TRUE return a
  SpatialPointsDataFrame

- cache:

  string: the gazetteer data can be cached locally, so that it can be
  used offline later. Valid values are `"session"`, `"persistent"`, or a
  directory name. Specifying `cache = "session"` will use a temporary
  directory that persists only for the current session.
  `cache = "persistent"` will use
  [`rappdirs::user_cache_dir()`](https://rappdirs.r-lib.org/reference/user_cache_dir.html)
  to determine the appropriate directory to use. Otherwise, if a string
  is provided it will be assumed to be the path to the directory to use.
  In this case, an attempt will be made to create the cache directory if
  it does not exist. A warning will be given if a cached copy of the
  data exists and is more than 30 days old

- refresh_cache:

  logical: if TRUE, and a data file already exists in the cache, it will
  be refreshed. If FALSE, the cached copy will be used

- simplified:

  logical: if TRUE, only return a simplified set of columns (see details
  in "Value", below)

- verbose:

  logical: show progress messages?

## Value

a data.frame or SpatialPointsDataFrame, with the following columns (note
that not all information is populated for all place names):

- gaz_id - the unique identifier of each gazetteer entry. Note that the
  same feature (e.g. "Browns Glacier") might have multiple gazetteer
  entries, each with their own `gaz_id`, because the feature has been
  named multiple times by different naming authorities. The
  `scar_common_id` for these entries will be identical, because
  `scar_common_id` identifies the feature itself

- scar_common_id - the unique identifier (in the Composite Gazetteer of
  Antarctica) of the feature. A single feature may have multiple names,
  given by different naming authorities

- place_name - the name of the feature

- place_name_transliterated - the name of the feature transliterated to
  simple ASCII characters (e.g. with diacritical marks removed)

- longitude and latitude - the longitude and latitude of the feature
  (negative values indicate degrees west or south). Note that many
  features are not point features (e.g. mountains, lakes), in which case
  the `longitude` and `latitude` values are indicative only, generally
  of the centroid of the feature

- altitude - the altitude of the feature, in metres relative to sea
  level. Negative values indicate features below sea level

- feature_type_name - the feature type (e.g. "Archipelago", "Channel",
  "Mountain")

- date_named - the date on which the feature was named

- narrative - a text description of the feature; may include a synopsis
  of the history of its name

- named_for - the person after whom the feature was named, or other
  reason for its naming. For historical reasons the distinction between
  "narrative" and "named for" is not always obvious

- origin - the naming authority that provided the name. This is a
  country name, or organisation name for names that did not come from a
  national source

- relic - if `TRUE`, this name is associated with a feature that no
  longer exists (e.g. an ice shelf feature that has disappeared)

- gazetteer - the gazetteer from which this information came (currently
  only "CGA")

If `simplified` is FALSE, these additional columns will also be
included:

- meeting_date - the date on which the name was formally approved by the
  associated naming authority. This is not available for many names: see
  the `date_named` column

- meeting_paper - references to papers or documents associated with the
  naming of the feature

- remote_sensor_info - text describing the remote sensing information
  (e.g. satellite platform name and image details) used to define the
  feature, if applicable

- coordinate_accuracy - an indicator of the accuracy of the coordinates,
  in metres

- altitude_accuracy - an indicator of the accuracy of the altitude
  value, in metres

- cga_source_gazetteer - for the Composite Gazetteer, this entry gives
  the source gazetteer from which this entry was taken. This is
  currently either a three-letter country code (e.g. "ESP", "USA") or
  "GEBCO" (for the GEBCO gazetteer of undersea features)

- country_name - the full name of the country where
  `cga_source_gazetteer` is a country

- source_name - the cartographic/GIS/remote sensing source from which
  the coordinates were derived

- source_publisher - where coordinates were derived from a map, the
  publisher of that map

- source_scale - the scale of the map from which the coordinates were
  derived

- source_institution - the institution from which the coordinate
  information came

- source_person - the contact person at the source institution, if
  applicable

- source_country_code - the country from which the coordinate
  information came

- source_identifier - where a coordinate or elevation was derived from a
  map, the identifier of that map

- comments - comments about the name or naming process

## References

<https://data.aad.gov.au/aadc/gaz/scar/>,
<https://www.scar.org/data-products/place-names/>

## See also

[`an_cache_directory`](https://docs.ropensci.org/antanym/reference/an_cache_directory.md),
[`an_gazetteers`](https://docs.ropensci.org/antanym/reference/an_gazetteers.md),
[`an_cga_metadata`](https://docs.ropensci.org/antanym/reference/an_cga_metadata.md)

## Examples

``` r
if (FALSE) { # \dontrun{
 ## download without caching
 g <- an_read()

 ## download to session cache, in sp format
 g <- an_read(cache = "session", sp = TRUE)

 ## download and cache to a persistent directory for later, offline use
 g <- an_read(cache = "persistent")

 ## refresh the cached copy
 g <- an_read(cache = "persistent", refresh_cache = TRUE)

 ## download and cache to a persistent directory of our choice
 g <- an_read(cache = "c:/my/cache/directory")
} # }
```
