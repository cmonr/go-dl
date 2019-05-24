# go-dl

`go-dl` is a small script that simplifies the installation of additional `go` executables.

The core idea is based off of the [_Installing extra Go versions_ docs](https://golang.org/doc/install#extra_versions).

For more information, run `go-dl --help`.



### Minor version symlinking

`go<version> download` configures the system to be able to run `go` at a specific version with `go<version>`. However, users/I generally don't care for the addutional patch granularity.

As a minor convenience, if the user-requested version differs from the downloaded version, `go-dl` will symlink the two for ease of use.

_**TL;DR:** If `1.11` is requested, `go1.11` will be simlinked to `go1.11.10`._


### _`go<version> download`_ weirdness

An odd side effect of the way that the download flow works is that when `go<version> download` is executed, `go` downloads all archives to `${HOME}/sdk`, with no option to change the target directory.

This seems extremely silly since a `${GOPATH}` should already exist in order to run the download command.

To help mitigate Home Directory polution, the `go-dl` script renames the executables, and in their place creates small shell scripts that set `${HOME}` to `${GOPATH}`. Additionally, when a new version is downloaded, the `sdk` directory is forced to live in `${GOPATH}`.

_**TL:DR:**
When a new version is downloaded, it's contents are saved in `${GOPATH}/sdk` instead of `${HOME}/sdk`.
`go<version>` executables are moved, hidden, and replaced with small shell scripts that perform the necessary fixes._
