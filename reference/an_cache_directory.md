# The cache directory used by antanym

The cache directory used by antanym

## Usage

``` r
an_cache_directory(cache)
```

## Arguments

- cache:

  string: the gazetteer data can be cached locally, so that it can be
  used offline later. Valid values are `"session"`, `"persistent"`, or a
  directory name. Specifying `cache="session"` will use a temporary
  directory that persists only for the current session.
  `cache="persistent"` will use
  [`rappdirs::user_cache_dir()`](https://rappdirs.r-lib.org/reference/user_cache_dir.html)
  to determine the appropriate directory to use. Otherwise, the input
  string will be assumed to be the path to the directory to use

## Value

directory path

## See also

[`an_read`](https://docs.ropensci.org/antanym/reference/an_read.md)

## Examples

``` r
## per-session caching
an_cache_directory(cache = "session")
#> [1] "/tmp/RtmpqWb7or/antanym-cache"

## persistent caching that will keep the data from one R session to the next
an_cache_directory(cache = "persistent")
#> [1] "~/.cache/antanym"
```
