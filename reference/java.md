# System Command to Run Java

Gets the system command needed to run Java from the command line, as a
string. Typically, this is the string: 'java'. However, if the R session
has the `JAVA_HOME` environmental variable set, it will use that to
locate java instead. This can be persisted over sessions (see the
Details below).

## Usage

``` r
java()
```

## Value

The system command needed to invoke Java, as a string.

## Details

This function is used by all of the
[`tika()`](https://docs.ropensci.org/rtika/reference/tika.md) functions
internally as the default value to its `java` parameter.

This function tries to find an environmental variable using
`Sys.getenv("JAVA_HOME")`. It looks for the `java` executable inside the
`bin` directory in the `JAVA_HOME` directory.

If you want to use a specific version of Java, set the `JAVA_HOME`
variable using `Sys.setenv(JAVA_HOME = 'my path')`, where 'my path' is
the path to a folder that has a `bin` directory with a `java`
executable.

For example, on Windows 11 `JAVA_HOME` might be
`C:/Program Files/Java/jdk-21`. On Ubuntu and macOS, it might be
something like `/usr/lib/jvm/temurin-21-jdk`.

The `JAVA_HOME` variable can also be set to persist over sessions. Add
the path to the `.Rprofile` by adding
`Sys.setenv(JAVA_HOME = 'my path')`, and it will use that every time R
is started.

## Examples

``` r
# \donttest{
# Typically, this function returns the string 'java'.
# If JAVA_HOME is set, it's a path to java in a 'bin' folder.
java()
#> [1] "java"
# }
```
