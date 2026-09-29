# Install or Update the Apache Tika `jar`

This downloads and installs the Tika App `jar` (~55 MB) into a user
directory, and verifies the integrity of the file using a checksum. The
default settings should work fine.

## Usage

``` r
install_tika(
  version = "3.2.3",
  digest = paste0("5908760c8506d6d1f2c37b59b21b513c2451960b471dde0b353d0ac825a3ea6a",
    "809714e0651de9883f8257444b2a8c56c6982a55fed74b5e5840261aa893b650"),
  mirrors = c("https://ftp.wayne.edu/apache/tika/",
    "http://mirrors.ocf.berkeley.edu/apache/tika/", "http://apache.cs.utah.edu/tika/",
    "http://mirror.cc.columbia.edu/pub/software/apache/tika/"),
  retries = 2,
  url = character()
)
```

## Arguments

- version:

  The declared Tika version

- digest:

  The sha512 checksum. Set to an empty string `""` to skip the check.

- mirrors:

  A vector of Apache mirror sites. One is picked randomly.

- retries:

  The number of times to try the download.

- url:

  Optional url to a particular location of the tika app. Setting this to
  any character string overrides downloading from random mirrors.

## Value

Logical if the installation was successful.

## Details

The default settings of `install_tika()` should typically be left as
they are.

This function will download the version of the Tika `jar` tested to work
with this package, and can verify file integrity using a checksum.

It will normally download from a random Apache mirror. If the mirror
fails, it tries the archive at `http://archive.apache.org/dist/tika/`.
You can also enter a value for `url` directly to override this.

It will download into a directory determined by
`tools::R_user_dir("rtika", which = "data")`, specific to the operating
system.

If [`tika()`](https://docs.ropensci.org/rtika/reference/tika.md) is
stopping with an error compalining about the `jar`, try running
`install_tika()` again.

## Uninstalling

If you are uninstalling the entire `rtika` package and want to remove
the Tika App `jar` also, run:

`unlink(tools::R_user_dir("rtika", which = "data"), recursive = TRUE)`

Alternately, navigate to the install folder and delete it manually. It
is the file path returned by
`tools::R_user_dir("rtika", which = "data")`. The path is OS specific.

## Distribution

Tika is distributed under the Apache License Version 2.0, which
generally permits distribution of the code "Object" without the
"Source". The master copy of the Apache Tika source code is held in GIT.
You can fetch (clone) the large source from GitHub (
https://github.com/apache/tika ).

## Examples

``` r
# \donttest{
if (interactive()) {
  install_tika()
}
# }
```
