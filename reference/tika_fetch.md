# Fetch Files with the Content-Type Preserved in the File Extension

On the Internet, Content-Type information is mainly communicated via the
server's headers. This is an issue if a file is saved to disk without
examining the headers. The file can have a missing or incorrect file
extension. For example, a URL ending in a slash (`/`) can produce file
with the Content-Type of `text/html`. The same URL might also produce a
`image/jpeg` or `application/pdf` file. URLs ending in `.php`, `.cfm`
can produce any Content-Type. The downloaded file will lose the server's
declared Content-Type unless its appended as a file extension.
`tika_fetch()` gets a file from the URL, examines the server headers,
and appends the matching file extension from Tika's database.

## Usage

``` r
tika_fetch(
  urls,
  download_dir = tempdir(),
  ssl_verifypeer = TRUE,
  retries = 1,
  quiet = TRUE
)
```

## Arguments

- urls:

  Character vector of one or more URLs to be downloaded.

- download_dir:

  Character vector of length one describing the path to the directory to
  save the results.

- ssl_verifypeer:

  Logical, with a default of TRUE. Some server SSL certificates might
  not be recognized by the host system, and in these rare cases the user
  can ignore that if they know why.

- retries:

  Integer of the number of times to retry each url after a failure to
  download.

- quiet:

  Logical if download warnings should be printed. Defaults to FALSE.

## Value

Character vector of the same length and order as input with the paths
describing the locations of the downloaded files. Errors are returned as
NA.

## Examples

``` r
# \donttest{
tika_fetch('https://tika.apache.org/')
#> [1] "/tmp/RtmpK7PZw5/rtika_file6f521c5fc59.html"
# a unique file name with .html appended to it
# }
```
