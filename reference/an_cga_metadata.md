# Information about the Composite Gazetteer of Antarctica data structure

The Composite Gazetteer of Antarctica data structure (as returned by
[`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md)):

## Usage

``` r
an_cga_metadata(simplified = TRUE)
```

## Arguments

- simplified:

  logical: if TRUE, only describe the simplified set of columns (see the
  equivalent parameter in
  [`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md))

## Value

a data frame with columns "field" and "description"

## References

<https://data.aad.gov.au/aadc/gaz/scar/>,
<https://www.scar.org/data-products/place-names/>

## See also

[`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md)

## Examples

``` r

an_cga_metadata()
#>                        field
#> 1                     gaz_id
#> 2             scar_common_id
#> 3                 place_name
#> 4  place_name_transliterated
#> 5                  longitude
#> 6                   latitude
#> 7                   altitude
#> 8          feature_type_name
#> 9                 date_named
#> 10                 narrative
#> 11                 named_for
#> 12                    origin
#> 13                     relic
#> 14                 gazetteer
#>                                                                                                                                                                                                                                                                                                                                                                   description
#> 1  The unique identifier of each gazetteer entry. Note that the same feature (e.g. 'Browns Glacier') might have multiple gazetteer entries, each with their own gaz_id, because the feature has been named multiple times by different naming authorities. The scar_common_id value for these entries will be identical, because scar_common_id identifies the feature itself
#> 2                                                                                                                                                                                                            The unique identifier (in the Composite Gazetteer of Antarctica) of the feature. A single feature may have multiple names, given by different naming authorities
#> 3                                                                                                                                                                                                                                                                                                                                                     The name of the feature
#> 4                                                                                                                                                                                                                                                                     The name of the feature transliterated to simple ASCII characters (e.g. with diacritical marks removed)
#> 5                                                                                                                 The longitude of the feature (negative values indicate degrees west). Note that many features are not point features (e.g. mountains, lakes), in which case the longitude and latitude values are indicative only, generally of the centroid of the feature
#> 6                                                                                                                 The latitude of the feature (negative values indicate degrees south). Note that many features are not point features (e.g. mountains, lakes), in which case the longitude and latitude values are indicative only, generally of the centroid of the feature
#> 7                                                                                                                                                                                                                                                             The altitude of the feature, in metres relative to sea level. Negative values indicate features below sea level
#> 8                                                                                                                                                                                                                                                                          The feature type (e.g. 'Archipelago', 'Channel', 'Mountain'). See an_feature_types for a full list
#> 9                                                                                                                                                                                                                                                                                                                                     The date on which the feature was named
#> 10                                                                                                                                                                                                                                                                                       A text description of the feature; may include a synopsis of the history of its name
#> 11                                                                                                                                                                                              The person after whom the feature was named, or other reason for its naming. For historical reasons the distinction between 'narrative' and 'named for' is not always obvious
#> 12                                                                                                                                                                                                                               The naming authority that provided the name. This is a country name, or organisation name for names that did not come from a national source
#> 13                                                                                                                                                                                                                                                     If TRUE, this name is associated with a feature that no longer exists (e.g. an ice shelf feature that has disappeared)
#> 14                                                                                                                                                                                                                                                                                                      The gazetteer from which this information came (currently only 'CGA')
```
