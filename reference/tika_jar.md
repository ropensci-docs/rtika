# Path to Apache Tika

Gets the path to the Tika App `.jar` installed by `tika_install()`.

## Usage

``` r
tika_jar()
```

## Value

A string describing the file path to the Tika App `.jar` file. If not
found, `NA`.

## Details

The `tika_jar()` function also checks if the `.jar` is actually on the
file system.

The file path is used by all of the
[`tika()`](https://docs.ropensci.org/rtika/reference/tika.md) functions
by default.

## Alternative Uses

You can call Apache Tika directly, as shown in the examples here.

It is better to use the `sys` package and avoid
[`system2()`](https://rdrr.io/r/base/system2.html), which has caused
erratic, intermittent errors with Tika.

## Examples

``` r
# \donttest{
jar <- tika_jar()
# see help
sys::exec_wait('java',c('-jar',jar, '--help'))
#> [1] 1
# detect language of web page
sys::exec_wait('java',c('-jar',jar, '--language','https://tika.apache.org/'))
#> [1] 1
# }
```
