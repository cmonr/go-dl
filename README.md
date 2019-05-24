# go-dl

`go-dl` is a small script that simplifies the installation of additional `go` executables.

The core idea is based off of the _Installing extra Go versions_ [https://golang.org/doc/install#extra_versions](docs).

For more information, run `go-dl --help`.


### Minor version symlinking

The `go<version> download` configures the system to be able to run `go` at a specific version with `go<version>`. However, users generally don't care for the patch granularity.

As a minor convenience, if the user-requested version and actually downlaoded version differ, `go-dl` will symlink the two for ease of use.

_TL;DR: If `1.11` is requested, `go1.11` will be smlinked to `go1.11.10`._


### `go<version> download` weirdness

An odd side effect of the way that the download flow works is that when `go<version> download` is executed, `go` downloads all archives to `${HOME}/sdk`, with no option to change the target directory.

This seems extremely silly since a `${GOPATH}` should already exist in order to run the download command.

To help mitigate Home Directory polution, the `go-dl` script renames the executables, and in their place creates small shell scripts that set `${HOME}` to `${GOPATH}`. Additionally, when a new version is downloaded, the `sdk` directory is forced to live in "${GOPATH}".

_TL:DR: When a new version is downloaded, it's contents are saved in `${GOPATH}/sdk` instead of `${HOME}/sdk`.
        `go<version>` executables are moved, hidden, and replaced with small shell scripts that perform the necessary fixes._
