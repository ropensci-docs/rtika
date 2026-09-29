# Get json Metadata and Plain Text Content

Tika can parse and extract text from almost anything, including zip,
tar, tar.bz2, and other archives that contain documents. If you have a
zip file with 100 text files in it, you can get the text and metadata
for each file nested inside of the zip file. This recursive output is
currently used for the jsonified mode. See:
https://wiki.apache.org/tika/RecursiveMetadata

The document contents are plain text in the "X-TIKA:content" field.

If `output_dir` is specified, files will have the `.json` file
extension.

## Usage

``` r
tika_json_text(input, ...)
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
`input`, of unparsed `json`. Unprocessed files are `as.character(NA)`.

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
json <- tika_json_text(batch)
#> Error in tika(input = input, output = c("jsonRecursive", "text"), ...): !any(is.na(jar)) is not TRUE
# }
```
