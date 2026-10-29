# Check Tika against a checksum

This is used by
[`install_tika()`](https://docs.ropensci.org/rtika/reference/install_tika.md)
internally, or can be called directly on a `jar` file. The latest `jar`
files and checksums are at https://tika.apache.org/download.html.

## Usage

``` r
tika_check(digest, jar = tika_jar(), algo = "sha512")
```

## Arguments

- digest:

  Character vector of length one with the target checksum.

- jar:

  Optional alternative path to a Tika `jar` file.

- algo:

  Optional algorithm used to create checksum. Defaults to SHA512.

## Value

logical if the `jar` checksum matches `digest`.
