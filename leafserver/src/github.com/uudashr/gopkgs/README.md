[![Build Status](https://travis-ci.org/uudashr/gopkgs.svg?branch=master)](https://travis-ci.org/uudashr/gopkgs)
[![GoDoc](https://godoc.org/github.com/uudashr/gopkgs?status.svg)](https://godoc.org/github.com/uudashr/gopkgs)
# gopkgs

Gopkgs is tools that provide list of available Go packages that can be imported.

This are alternative to `go list all`, it just faster.

## Installation

`$ go get github.com/uudashr/gopkgs/cmd/gopkgs`

## Usage
```
$ gopkgs -help
Usage of gopkgs:
  -format string
    	custom output format (default "{{.ImportPath}}")
  -help
    	show this message


Use -format to custom the output using template syntax. The struct being passed to template is:
    type Pkg struct {
        Dir        string // directory containing package sources
        ImportPath string // import path of package in dir
        Name       string // package name
    }
```

### Example
Get package name along with the import path.
```
$ gopkgs -format "{{.Name}};{{.ImportPath}}"
testing;github.com/mattes/migrate/source/testing
http;github.com/stretchr/testify/http
ql;github.com/mattes/migrate/database/ql
pkgtree;github.com/golang/dep/internal/gps/pkgtree
sqlite3;github.com/mattes/migrate/database/sqlite3
gps;github.com/golang/dep/internal/gps
spanner;github.com/mattes/migrate/database/spanner
dep;github.com/golang/dep
shortener;github.com/uudashr/shortener
bindata;github.com/mattes/migrate/source/go-bindata
postgres;github.com/mattes/migrate/database/postgres
test;github.com/vektra/mockery/mockery/fixtures
awss3;github.com/mattes/migrate/source/aws-s3
```

## Related Project
This is based on https://github.com/haya14busa/gopkgs but taking slightly different path by simplifiying it's implementation.
