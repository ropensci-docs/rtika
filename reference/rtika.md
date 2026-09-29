# rtika: R Interface to 'Apache Tika'

Extract text or metadata from over a thousand file types. Get either
plain text or structured XHTML content.

## Installing

If you have not done so already, finish installing rtika by typing in
the R console:

[`install_tika()`](https://docs.ropensci.org/rtika/reference/install_tika.md)

## Getting Started

The
[`tika_text`](https://docs.ropensci.org/rtika/reference/tika_text.md)
function will extract plain text from many types of documents. It is a
good place to start. Please read the Vignette also. Other main functions
include
[`tika_xml`](https://docs.ropensci.org/rtika/reference/tika_xml.md) and
[`tika_html`](https://docs.ropensci.org/rtika/reference/tika_html.md)
that get a structured XHMTL rendition. The
[`tika_json`](https://docs.ropensci.org/rtika/reference/tika_json.md)
function gets metadata as \`.json\`, with XHMTL content.

The
[`tika_json_text`](https://docs.ropensci.org/rtika/reference/tika_json_text.md)
function gets metadata as \`.json\`, with plain text content.

[`tika`](https://docs.ropensci.org/rtika/reference/tika.md) is the main
function the others above inherit from.

Use
[`tika_fetch`](https://docs.ropensci.org/rtika/reference/tika_fetch.md)
to download files with a file extension matching the Content-Type.

## See also

Useful links:

- <https://docs.ropensci.org/rtika/>

- <https://github.com/ropensci/rtika/>

- Report bugs at <https://github.com/ropensci/rtika/issues/>

## Author

**Maintainer**: Sasha Goodman <goodmansasha@gmail.com>

Authors:

- The Apache Software Foundation \[copyright holder\]

Other contributors:

- Julia Silge (Reviewed the package for rOpenSci, see
  https://github.com/ropensci/software-review/issues/191/) \[reviewer\]

- David Gohel (Reviewed the package for rOpenSci, see
  https://github.com/ropensci/software-review/issues/191/) \[reviewer\]
