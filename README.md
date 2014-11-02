NOT YET IMPLEMENTED

# stats

Calculate statistics from lines

# Description

`stats` is a command line tool written in golang to calculate statistics from lines.

Example 1: 

```bash
$ echo "/me\t0.234\n/me\t1.234" | stats -f 2
max:1.234   min:0.234   count:2   mean:0.734  sum:1.468
```

Example 2: 

```bash
$ echo "/me\t0.234\n/me\t1.234\n/books\t1.111" | stats -k 1 -f 2
key:/me      count:2   max:1.234   min:0.234   mean:0.734  sum:1.468
key:/books   count:1   max:1.111   min:1.111   mean:1.111  sum:1.111
```

Example 3: 

```bash
$ echo "GET\t/me\t0.234\nPUT\t/me\t1.234\nGET\t/books\t1.111" | stats -k 1,2 -f 3
key:GET /me      count:1   max:0.234   min:0.234   mean:0.234  sum:0.234
key:PUT /me      count:1   max:1.234   min:1.234   mean:1.234  sum:1.234
key:GET /books   count:1   max:1.111   min:1.111   mean:1.111  sum:1.111
```

## Tips

[lltsv](https://github.com/sonots/lltsv) would be useful to parse LTSV format log:


```bash
$ echo "path:/me\treqtime:0.234\npath:/me\treqtime:1.234" | lltsv -k path,reqtime -K | stats -k 1 -f 2
max:1.234   min:0.234   count:2   mean:0.734  sum:1.468
```

## Installation

Executable binaries are available at [releases](https://github.com/sonots/stats/releases).

For example, for linux x86_64, 

```bash
$ wget https://github.com/sonots/stats/releases/download/v0.1.0/stats_linux_amd64 -O stats
$ chmod a+x stats
```

If you have the go runtime installed, you may use go get. 

```bash
$ go get github.com/sonots/stats
```

## ToDo

1. write tests

## Build

To build, use go get and make

```
$ go get -d github.com/sonots/stats
$ cd $GOPATH/src/github.com/sonots/stats
$ make
```

To release binaries, I use [gox](https://github.com/mitchellh/gox) and [ghr](https://github.com/tcnksm/ghr)

```
go get github.com/mitchellh/gox
gox -build-toolchain # only first time
go get github.com/tcnksm/ghr

cd $GOPATH/src/github.com/sonots/stats/pkg
gox ../...
ghr <tag> .
```

## Contribution

1. Fork (https://github.com/sonots/stats/fork)
2. Create a feature branch
3. Commit your changes
4. Rebase your local changes against the master branch
5. Run test suite with the go test ./... command and confirm that it passes
6. Run gofmt -s
7. Create new Pull Request

## Copyright

See [LICENSE](./LICENSE)
