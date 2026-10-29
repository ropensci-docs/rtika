# Main R Interface to 'Apache Tika'

Extract text or metadata from over a thousand file types. Get either
plain text or structured `XHTML`. Metadata includes `Content-Type`,
character encoding, and Exif data from jpeg or tiff images. See the long
list of supported file types, click the "Supported Formats" link on this
page : <https://tika.apache.org/>.

## Usage

``` r
tika(
  input,
  output = c("text", "jsonRecursive", "xml", "html")[1],
  output_dir = "",
  return = TRUE,
  java = rtika::java(),
  jar = rtika::tika_jar(),
  threads = 2,
  max_restarts = integer(),
  timeout = 3e+05,
  max_file_size = integer(),
  config = system.file("extdata", "ocr.xml", package = "rtika"),
  args = character(),
  quiet = TRUE,
  cleanup = TRUE,
  lib.loc = .libPaths()
)
```

## Arguments

- input:

  Character vector describing the paths to the input documents. Strings
  starting with 'http://','https://', or 'ftp://' are downloaded to a
  temporary directory. On Windows, the local paths cannot span drives
  because of a Windows convention.

- output:

  Optional character vector of the output format. The default, `"text"`,
  gets plain text without metadata. `"xml"` and `"html"` get `XHTML`
  text with metadata. `"jsonRecursive"` gets `XHTML` text and `json`
  metadata. `c("jsonRecursive","text")` or `c("J","t")` get plain text
  and `json` metadata. See the 'Output Details' section.

- output_dir:

  Optional directory path to save the converted files in. Tika may
  overwrite files so an empty directory is best. See the 'Output
  Details' section before using.

- return:

  Logical if an R object should be returned. Defaults to TRUE. If set to
  FALSE, and output_dir (above) must be specified.

- java:

  Optional command to invoke Java. For example, it can be the full path
  to a particular Java version. See the Configuration section below.

- jar:

  Optional alternative path to a `tika-app-X.XX.jar`. Useful if this
  package becomes out of date.

- threads:

  Integer of the number of file consumer threads Tika uses. Defaults to
  2.

- max_restarts:

  Integer of the maximum number of times the watchdog process will
  restart the child process. The default is no limit.

- timeout:

  Integer of the number of milliseconds allowed to a parse before the
  process is killed and restarted. Defaults to 300000.

- max_file_size:

  Integer of the maximum bytes allowed. Do not process files larger than
  this. The default is unlimited.

- config:

  Path to the XML config file. Defaults to
  `system.file("extdata", "ocr.xml", package = "rtika")`'. There is also
  a `no-ocr.xml` file available.

- args:

  Optional character vector of additional arguments passed to Tika, that
  may not yet be implemented in this R interface, in the pattern of
  `c('-arg1','setting1','-arg2','setting2')`.

- quiet:

  Logical if Tika command line messages and errors are to be suppressed.
  Defaults to `TRUE`.

- cleanup:

  Logical to clean up temporary files after running the command, which
  can accumulate. Defaults to `TRUE`. They are in
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html). These files are
  automatically removed at the end of the R session even if set to
  FALSE.

- lib.loc:

  Optional character vector describing the library paths. Normally, it's
  best to leave this parameter alone. The parameter is included mainly
  for package testing.

## Value

A character vector in the same order and with the same length as
`input`. Unprocessed files are `as.character(NA)`. If `return = FALSE`,
then a `NULL` value is invisibly returned. See the Output Details
section below.

## Output Details

If an input file did not exist, could not be downloaded, was a
directory, or Tika could not process it, the result will be
`as.character(NA)` for that file.

By default, `output = "text"` and this produces plain text with no
metadata. Some formatting is preserved in this case using tabs, newlines
and spaces.

Setting `output` to either `"xml"` or the shortcut `"x"` will produce a
strict form of `HTML` known as `XHTML`, with metadata in the `head` node
and formatted text in the `body`. Content retains more formatting with
`"xml"`. For example, a Word or Excel table will become a HTML `table`,
with table data as text in `td` elements. The `"html"` option and its
shortcut `"h"` seem to produce the same result as `"xml"`. Parse XHTML
output with
[`xml2::read_html`](http://xml2.r-lib.org/reference/read_xml.md).

Setting `output` to `"jsonRecursive"` or its shortcut `"J"` produces a
tree structure in \`json\`. Metadata fields are at the top level. The
`XHTML` or plain text will be found in the `X-TIKA:content` field. By
default the text is `XHTML`. This can be changed to plain text like
this: `output=c("jsonRecursive","text")` or `output=c("J","t")`. This
syntax is meant to mirror Tika's. Parse `json` with
[`jsonlite::fromJSON`](https://jeroen.r-universe.dev/jsonlite/reference/fromJSON.html).

If `output_dir` is specified, then the converted files will also be
saved to this directory. It's best to use an empty directory because
Tika may overwrite existing files. Tika seems to add an extra file
extension to each file to reduce the chance, but it's still best to use
an empty directory. The file locations within the `output_dir` maintain
the same general path structure as the input files. Downloaded files
have a path similar to the \`tempdir()\` that R uses. The original paths
are now relative to `output_dir`. Files are appended with `.txt` for the
default plain text, but can be `.json`, `.xml`, or `.html` depending on
the `output` setting. One way to get a list of the processed files is to
use `list.files` with `recursive=TRUE`. If `output_dir` is not
specified, files are saved to a volatile temp directory named by
[`tempdir()`](https://rdrr.io/r/base/tempfile.html) and will be deleted
when R shuts down. If this function will be run on very large batches
repeatedly, these temporary files can be cleaned up every time by adding
`cleanup=TRUE`.

## Background

Tika is a foundational library for several Apache projects such as the
Apache Solr search engine. It has been in development since at least
2007. The most efficient way I've found to process many thousands of
documents is Tika's 'batch' mode, which is the only mode used in
\`rtika\`. There are potentially more things that can be done, given
enough time and attention, because Apache Tika includes many libraries
and methods in its .jar file. The source is available at:
<https://tika.apache.org/>.

## Installation

Tika requires Java 11 or later.

Java installation instructions are at https://openjdk.org/install/ or
https://www.java.com/en/download/help/download_options.xml.

By default, this R package internally invokes Java by calling the `java`
command from the command line. To specify the path to a particular Java
version, set the path in the `java` attribute of the `tika` function.

## Examples

``` r
# \donttest{
#extract text
batch <- c(
  system.file("extdata", "jsonlite.pdf", package = "rtika"),
  system.file("extdata", "curl.pdf", package = "rtika"),
  system.file("extdata", "table.docx", package = "rtika"),
  system.file("extdata", "xml2.pdf", package = "rtika"),
  system.file("extdata", "R-FAQ.html", package = "rtika"),
  system.file("extdata", "calculator.jpg", package = "rtika"),
  system.file("extdata", "tika.apache.org.zip", package = "rtika")
)
text = tika(batch)
#> Error in tika(batch): !any(is.na(jar)) is not TRUE
cat(substr(text[1],45,450))
#> Error in text[1]: object of type 'closure' is not subsettable

#more complex metadata
if(requireNamespace('jsonlite')){

  json = tika(batch,c('J','t'))
  # 'J' is shortcut for jsonRecursive
  # 't' for text
  metadata = lapply(json, jsonlite::fromJSON )

  #embedded resources
  lapply(metadata, function(x){ as.character(x$'Content-Type') })

  lapply(metadata, function(x){ as.character(x$'Creation-Date') })

  lapply(metadata, function(x){  as.character(x$'X-TIKA:embedded_resource_path') })
}
#> Error in tika(batch, c("J", "t")): !any(is.na(jar)) is not TRUE
# }
```
