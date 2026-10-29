# Get Plain Text

If `output_dir` is specified, files will have the `.txt` file extension.

## Usage

``` r
tika_text(input, ...)
```

## Arguments

- input:

  Character vector describing the paths and/or urls to the input
  documents.

- ...:

  Other parameters to be sent to
  [`tika()`](https://docs.ropensci.org/rtika/reference/tika.md).

## Value

A character vector in the same order and with the same length as
`input`, of plain text. Unprocessed files are `as.character(NA)`.

## Examples

``` r
# \donttest{
batch <- c(
 system.file("extdata", "jsonlite.pdf", package = "rtika"),
 system.file("extdata", "curl.pdf", package = "rtika"),
 system.file("extdata", "table.docx", package = "rtika"),
 system.file("extdata", "xml2.pdf", package = "rtika"),
 system.file("extdata", "R-FAQ.html", package = "rtika"),
 system.file("extdata", "calculator.jpg", package = "rtika"),
 system.file("extdata", "tika.apache.org.zip", package = "rtika")
)
text <- tika_text(batch)
#> Error in tika(input = input, output = "text", ...): !any(is.na(jar)) is not TRUE
# }
```
